# node-fasttext

Nodejs binding for fasttext representation and classification.

[![MIT License](https://img.shields.io/badge/license-MIT_License-green.svg?style=flat-square)](./LICENSE)
[![npm version](https://img.shields.io/npm/v/fasttext.svg?style=flat)](https://www.npmjs.com/package/fasttext)
[![downloads](https://img.shields.io/npm/dm/fasttext.svg)](https://www.npmjs.com/package/fasttext)
[![Travis](https://travis-ci.org/vunb/node-fasttext.svg?branch=master)](https://travis-ci.org/vunb/node-fasttext)
[![Appveyor](https://ci.appveyor.com/api/projects/status/9gd460vxd6jbel14/branch/master?svg=true)](https://ci.appveyor.com/project/vunb/node-fasttext/branch/master)

> This is a link to the Facebook [fastText](https://github.com/facebookresearch/fastText). A Library for efficient text classification and representation learning.

* FASTTEXT_VERSION = 12;
* FASTTEXT_FILEFORMAT_MAGIC_INT32 = 793712314;

# Installation

Using npm:

> npm install fasttext --save

# fastText Classifier

According to [fasttext.cc](https://fasttext.cc/docs/en/supervised-tutorial.html). We have a simple classifier for executing prediction models about `cooking` from stackexchange questions:

```js
const path = require('path');
const fastText = require('fasttext');

const model = path.resolve(__dirname, './model_cooking.bin');
const classifier = new fastText.Classifier(model);

classifier.predict('Why not put knives in the dishwasher?', 5, (err, res) => {
    if (err) {
        console.error(err);
    } else if (res.length > 0) {
        let tag = res[0].label; // __label__knives
        let confidence = res[0].value // 0.8787146210670471
        console.log('classify', tag, confidence, res);
    } else {
        console.log('No matches');
    }
});
```

Before we haved trained model to use the followings params:

```bash
# Training
~/fastText/data$ ./fasttext supervised -input cooking.train -output model_cooking -lr 1.0 -epoch 25 -wordNgrams 2 -bucket 200000 -dim 50 -loss hs
Read 0M words
Number of words:  8952
Number of labels: 735
Progress: 100.0%  words/sec/thread: 1687554  lr: 0.000000  loss: 5.247591  eta: 0h0m 4m

# Testing
~/fastText/data$ ./fasttext test model_cooking.bin cooking.valid
N       3000
P@1     0.587
R@1     0.254
Number of examples: 3000
```

# Contributing

Pull requests and stars are highly welcome.

For bugs and feature requests, please [create an issue](https://github.com/vunb/node-crfsuite/issues/new).
