# wc-gpu
A GPU accelerated version of the Unix util `wc`

## Why?
I got [nerdsniped](https://xkcd.com/356/) by
[wc2](https://github.com/robertdavidgraham/wc2), when it got posed to
[HN](https://news.ycombinator.com/item?id=40738833) and though, hey, y'know
what would be excessive and unecessary and stupid, but might be faster? Running
wc on a GPU. So here we are.

## The code
ChatGPT wrote the core Cuda kernels, and some other parts as well, but it has
its limitations. I've been programming for decades but my career hasn't needed
me to do GPU programming before, so this was a fun way to get my feet wet.

I don't even currently have an Nvidia card of my own to test this out on, so I
used a T4 on Google Colab to prove it works.

## The benchmark

After [embarrasing myself](https://github.com/robertdavidgraham/wc2/issues/10)
because I can't read, I generated a set of test files, and got the following
results with timeit in [Python on
Colab](https://github.com/fragmede/wc-gpu/blob/main/wc_gpu.ipynb).

| Input File    | Time                        |
|---------------|-----------------------------|
|ascii.txt      | 0.1808300140000938 seconds  |
|pocorgtfo18.pdf| 0.17899091699973724 seconds |
|space.txt      | 0.18513659300015206 seconds |
|utf8.txt       | 0.17958779099990352 seconds |
|word.txt       | 0.17560361200003172 seconds |

The Cuda accelerated kernel is thus faster than wc2's times:

| Program | Input File   | macOS | Linux |
|---------|--------------|------:|------:|
| wc2.c   | (all)        |0.206  | 0.278 |
| wc2.js  | (all)        |0.281  | 0.488 |

Haven't tested the overhead from running this at the command line.
