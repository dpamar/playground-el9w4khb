# Welcome!

Welcome to this new playground about the BF language. Make sure you already read 
* [Getting started with BrainFuck](https://tech.io/playgrounds/50426/getting-started-with-brainfuck/welcome)
* [BrainFuck part 2 - Working with arrays](https://tech.io/playgrounds/50443/brainfuck-part-2---working-with-arrays/welcome)
* [BrainFuck part 3 - Write a BF interpreter in BF](https://www.codingame.com/playgrounds/50446/brainfuck-part-3---write-a-bf-interpreter-in-bf/welcome)
* [BrainFuck part 4 - Advanced maths](https://www.codingame.com/playgrounds/50446/brainfuck-part-3---write-a-bf-interpreter-in-bf/welcome)
* [BrainFuck part 5 - Math sequences](https://www.codingame.com/playgrounds/50478/brainfuck-part-5---math-sequences/welcome)
* [BrainFuck part 6 - 16-bit integers](https://www.codingame.com/playgrounds/50482/brainfuck-part-6---16-bit-integers/be-smart)
* [BrainFuck part 7 - Quine (+ some non-BF quine theory)](https://www.codingame.com/playgrounds/50485/brainfuck-part-7---quine-some-non-bf-quine-theory/welcome)
* [BrainFuck part 8 - JS/C#/BF Multi quine](https://www.codingame.com/playgrounds/50499/brainfuck-part-8---jscbf-multi-quine/welcome)

playgrounds if you didn't already !

The goal of this playground is to implement different sort algorithms on arrays.

Sorting is a very popular problem in computer science : how to find the best sorting algorithm for a given case?

In order to compare these codes efficiently, let's have a common template to compare executions.
In this playground, we will use arrays of non-null values, to focus on sorts and not on "possibly-null 2-cell-long arrays"

# Char template

```
>>>>>>               leave as many cells as needed (for sorting algorithm)
,[>,]                read a list of chars
        __ do the sort __
[.>]                 print sorted list of chars
```
