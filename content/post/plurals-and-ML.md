---
title: "Plurals and ML"
date: 2020-01-24T16:39:07-06:00
draft: true
tags: ['Machine Learning', 'Natural Language']
---
# Plurals and Machine Learning

Using older machine learning models to conjugate English verbs produced rather silly results. These models performed at an acceptable level for many words, but when given nonsense words as an input these models would produce humorous conjugations. For [example](https://books.google.com/books?id=2cEuBgAAQBAJ&pg=PA144&lpg=PA144&dq=smeej+leefloag&source=bl&ots=y2F6Lge_uw&sig=ACfU3U0WPSRcA2Pwu8O0NqUm00dsExNyNw&hl=en&sa=X&ved=2ahUKEwiW4MbOqJ3nAhUDB50JHfvvB5wQ6AEwAHoECAsQAQ#v=onepage&q=smeej%20leefloag&f=false), we have:

|Verb | Human Generated Past-Tense | Machine Generated Past-Tense|
|-----|------------------|-------------------|
|mail|mailed|membled|
|conflict|conflicted|conflafted|
|wink|winked|wok|
|quiver|quivered|quess|
|satisfy|satisfied|sedderded|
|smairf|smairfed|sprurice|
|trilb|tribled|treelilt|
|smeej|smeejed|leefloag|
|frilg|frilged|freezled|

Naturally, my girlfriend and I found this hilarious. With the use of the [XTAG](https://www.cis.upenn.edu/~xtag/swrelease.html) database, we thought it would be fun to play around with a similar model to pluralize English nouns.

A jupyter notebook with all of the code from this investigation will be available on [github]()

### Setup

The XTAG database is written in a flat ascii format, which doesn't play nice with modern systems, so it needs some cleaning up.

```python
def isplnoun(*line):
    for entry in line:
        if str(entry)[0].isupper():
            if re.match('N 3pl$', str(entry)):
                return True
    return False
```

This is a simple function which takes an entry from the XTAG database and checks each cell for the noun, plural tag, not counting the Genitive nouns.

```python
raw = pd.read_csv('leefloag/morph_english.flat', sep='\t', lineterminator='\n',
                  names=['pl', 'blk', 'sg', 'pos1', 'pos2', 'pos3', 'pos4'])
raw = raw.values
clean = raw[[not x.startswith(';') for x in raw[:,0]], :]
clean = np.delete(clean, 1, axis=1)

mask = [isplnoun(*x) for x in clean]
clean = clean[mask,:]
clean = clean[:, :2]
clean = clean[~pd.isnull(clean).any(axis=1)]
clean = np.array([[re.sub('[^a-z]', '', x.strip().lower()), re.sub('[^a-z]','', y.strip().lower())] for x, y in clean])
```
This code uses pandas's super fast `read_csv()` function to import our file quickly and then just turn it into a numpy array for ease of generalization. We remove the comment lines from the beginning, and then turn our `isplnoun()` function into a boolean mask to remove all the lines that aren't plural non-genitive nouns. Then cut off the part-of-speech information since we don't need that anymore. Then we remove lines with null inputs.

### Vectorization

We're going to need a vector encoding of each of our words. We think that the vectorization ought to preserve order, so we are just going to cipher our text as integers. We'll scan through the whole corpus and get a set of all the characters used, and then we'll use that to create a simple mapping and inverse mapping. We'll use `'?'` as our end-of-frame character.

```python
charset = set()
for x in clean.flatten():
    for y in x:
        charset.add(y)
mapping = {c: i for i, c in enumerate(charset)}
mapping['?'] = len(mapping)
invmap = {i: c for c, i in mapping.items()}
```

Of course we'll also need functions to turn those lists of words into lists of vectors.

```python
def map_encode(*words, code=mapping):
    output = []
    lens = np.vectorize(len)(words)
    maxlen = max(lens)
    for word in words:
        xpand = list(word)
        padval = maxlen - len(xpand)
        xpand[len(xpand):] = ['?'] * padval
        mapped = [code[y] for y in xpand]
        output.append(mapped)
    return output

def map_decode(*ctext, code=invmap): # The ctest stands for 'ciphertext'
    output = []
    for word in ctext:
        dcoded = [code[x] for x in word]
        dcoded = ''.join(dcoded).strip('?')
        output.append(dcoded)
    return output
```

So running `map_encode(*['coen'])` returns something like: `[[16, 25, 3, 1]]` and `map_encode(*['coen', 'needell'])` returns something like : `[[16, 25, 3, 1, 26, 26, 26], [1, 3, 3, 10, 3, 24, 24]]`. You'll notice a lot of '5's because I have a boatload of 'e's in my name. Now, finally, we transform our inputs and outputs.

```python
invecs = map_encode(*clean.transpose()[0])
outvecs = map_encode(*clean.transpose()[1])
```


### Plurals and Simple Deep Networks

To start we'll put this dataset through a single-hidden-layer network.
