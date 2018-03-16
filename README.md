# Word2Bits - Quantized Word Vectors

  Word2Bits extends the Word2Vec algorithm to output high quality
  quantized word vectors that take 8x-16x less storage/memory than
  regular word vectors. Read the details at [https://arxiv.org/abs/1803.05651](https://arxiv.org/abs/1803.05651).

## What are Quantized Word Vectors?

  Quantized word vectors are word vectors where each parameter
  is one of `2^bitlevel` values.

  For example, the 1-bit quantized vector for "king" looks something
  like

  ```
  0.33333334 0.33333334 0.33333334 -0.33333334 -0.33333334 -0.33333334 0.33333334 0.33333334 -0.33333334 0.33333334 0.33333334 ...
  ```

  Since parameters are limited to 1 of `2^bitlevel` values, each one
  takes only `bitlevel` bits to represent; this drastically reduces
  the amount of storage that word vectors take.

## Download Pretrained Word Vectors
  TODO

## Visualizing Quantized Word Vectors

Here are examples of 800 dimensional 1 bit word vectors and their nearest and furthest neighbors:

<img src="images/visualize_nearest_man.png?raw=true" width="400" height="300"/> <img src="images/visualize_nearest_science.png?raw=true" width="400" height="300"/>

(Note: every 5 word vectors are labelled; turquoise line boundary between nearest and furthest word vectors from target.)

## Using the Code

### Quickstart

Compile with
```
make word2bits
```

Run with
```
./word2bits -train input -bitlevel 1 -size 200 -window 10 -negative 12 -threads 2 -iter 5 -min-count 5  -output 1bit_800d_vectors -binary 0
```
Description of the most common flags
```
- train                       Input corpus text file
- quantization_level          Number of bits for each parameter. 0 is full precision (or 32 bits).
- size                        Word vector dimension
- window                      Window size
- negative                    Negative sample size
- threads                     Number of threads to use to train
- iter                        Number of epochs to train
- min-count                   Minimum count value. Words appearing less than value are removed from corpus.
- output                      Path to write output word vectors
- binary                      0 to write in Glove format; 1 to write in binary format.
```

### Tutorial - text8