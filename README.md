# wc-gpu

GPU accelerated unix util `wc`.

## Why?
I got [nerdsniped](https://xkcd.com/356/) by
[wc2](https://github.com/robertdavidgraham/wc2), when it got posed to
[HN](https://news.ycombinator.com/item?id=40738833) and though, hey, y'know
what would be excessive and unecessary and stupid, but might be faster? Running
wc on a GPU. So here we are.

## The code
I'll be honest, ChatGPT wrote this thing. I don't know how to Cuda. I could
eventually figure it out but we live in the future.

I don't currently have an Nvidia card of my own to test this out on, so I used
a T4 on Google Colab to get it working.

## The benchmark

After [embarrasing myself](https://github.com/robertdavidgraham/wc2/issues/10)
because I can't read, I generated a set of test files, and got the following
results with timeit in Python on Colab.

| Input File    | Time                        |
|---------------|-----------------------------|
|ascii.txt      | 0.1808300140000938 seconds  |
|pocorgtfo18.pdf| 0.17899091699973724 seconds |
|space.txt      | 0.18513659300015206 seconds |
|utf8.txt       | 0.17958779099990352 seconds |
|word.txt       | 0.17560361200003172 seconds |

The Cuda accelerated kernel is faster than wc2's times:

| Program | Input File   | macOS | Linux |
|---------|--------------|------:|------:|
| wc2.c   | (all)        |0.206  | 0.278 |
| wc2.js  | (all)        |0.281  | 0.488 |

However, invoking the python interpreter slows us down here. I don't think I'm
going to write a wc-gpu.cpp, so this is as far as we're going to go.

