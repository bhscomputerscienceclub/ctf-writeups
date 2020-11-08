---
author: kaiz
---

# 2309

### Solution
When we open up the x.txt file we get a lot of `i` and `d` characters with a few `s` and `o` characters. 

We then look at the [2309 xkcd photo](https://xkcd.com/2309/) and it mentions font based/variable width variables and creating a new programing language (esolang). 

When we search up xkcd esolang, the first result is [Deadfish x](https://esolangs.org/wiki/Deadfish_x) which looks similar to what the x.txt file is written in but some of the commands are different letters.

We then replace the all the `i` letters in the x.txt file with `x` (add 1 to x), `o` with `K` (output x as ASCII), and `s` with `c` (sqaure x) . We can then copy the interpreter and run the file and we get the flag. 
