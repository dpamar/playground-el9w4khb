# Quicksort

Now, let's implement QuickSort. This sorting solution is known as one of the most efficient ones in general case.

The principle is:
* Select a pivot value P
* Move any value lower than P on an array A
* Move any value higher than P on an array B
* Sort A and B
* Merge [A, P, B]

The problem is that we never did something like recursion in BF. Let's try it now

# Let's start

* Memory: 0 _array_ 0 0 0 0
* Cursor: after last array value 
* Input: some chars to sort

# Process

* _Note: we will read chars from the input and compute array length on the fly_
* There will be on the right of the array a processing queue with pairs [startIndex, length]
* Initialize algorithm with startIndex and length
  * _Note: indexes will be 1-based and from the end of the array. Array[1] = last cell_
  * _Memory :  0 [array] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 [queue]_
* Get current start index and length
  * Move array cells from first to start index - 1 on the far right
  * Then move the next _length_ cells to the right, only one cell
  * Select pivot : let's pick last value and isolate it
  * for each array value, except pivot, compare with pivot:
    * if less than pivot:
      * move to beginning of array1 (easier than end)
      * increase array1 length
    * if greater:
      * move to begining of array2
      * increase array2 length and move to the left
      * move array1, array 1 length and pivot to the left
  * _Memory :  0 [out of range array] 0 [array to sort] 0 [array 1] 0 [array 1 length] [pivot value] 0 0 0 0 0 [array 2 length] 0 [array 2] 0 [out of range] 0 0 0 [queue]_
  * if array2 length is not null add at end of queue values [start index, array2 length]
  * if array1 length is not null add at end of queue values [start index + array2 length + 1, array1 length]
  * Move arrays back to the original memory configuration
  * remove queue first entries
  * move queue on the left
* loop

# Code
```
>,[>+[->+<],]                                  read chars and build array length
>[->>>>>>>>>>>>>>>+<<<<<<<<<<<<<<<]            move length
>>>>>>>>>>>>>>+                                set first queue pair : 1 and length
[                                               for each queue pair
  [-<+<+>>]<[->+<]                             copy start index
  <-[-<<[<]<<<<<<<<<<<<[->>>>>>>>>>            move first out of range array
  >>+<<<<<<<<<<<<]>>>>>>>>>>>>[>]>]              ** part 2 **
  >>>[-<<+<+>>>]<<[->>+<<]<                    copy length
  [-<<[<]<<<<<<<<<+>>>>>>>>>>[>]>]             move length before next array block
  <<[<]<<<<<<<<<                               go to copied length
  [-<<[<]<[->+<]>[>]>]                         move next "length" cells
  <<[->>>>+<<<<]                               isolate pivot
  <[                                           for each value in array to sort
    [->+>+<<]>>[-<<+>>]<                       copy
    [->>[>]>>>>+<<<<<[<]<]                     move copy besides pivot
    >>[>]>>[->+<<<+>>]>[-<+>]>[-<+>]<<         copy pivot and move value
    >>+<<[->[->]>[<<[-]>>->>]                  compare cell and pivot
    <<+<<]>[[-]<+>]<[->+<]<<[->>+<<]>>>          ** part 2 ** and restore pivot copy
     [->-<                                      value greater than pivot
      <<<<[<]<<[->>>[>]>>>>>>>>+<<<<<<<<<[<]<<]move value to array 2
      >>>[>]>>>>>>>+[-<+>]                     increase length 2
      <<<<<<<<[<]>[[-<+>]>]>[-<+>]>[-<+>]      move array 1 and length and pivot to the left
    ]>[-                                       or pivot greater than value
      <<<+<<[<]<<[->>+<<]>>[>]>>>>             or move value to array 1 and increase its length
    ]<<<<<[<]<<                                got to sorting array last cell
  ]                                            loop on array cell
  >>>[>]>>>>>>>                                go to array2 length
  [                                            if not null
    [-<+<+>>]<[->+<]>                          copy length
    [->>[>]>[>]>>+<<<[<]<<[<]<]                move beside queue
    >>[>]>[>]>>                                go to copy
    >[-<<<+>>>]<<<[->>>+[>]>+<<[<]<]           copy start index at end of queue
    >>[-<+>]<[->>[>]>>+<<<[<]<]                move array 2 length at end of queue
    >>[>]>[[-<+>]>]<<[<]<<<[<]<[<]<            enqueue items and go back to length 2 location
  ]<<<<<<[                                     go to array length 1; if not null
    [->>>>>>>>[>]>[>]>>>[>]>>+                 move after queue
    <<<[<]<<<[<]<[<]<<<<<<<]                     ** part 2 **
    >>>>[->>>>[>]>[>]>+<<[<]<[<]<<<]           copy length 2 if not null from a copy
    >>>>[>]>[>]>>>[-<+<+>>]<[->+<]<+           compute length 2 plus start index plus 1 (array1 start index)
    [->>[>]>+<<[<]<]                           move new startindex after queue
    >>[>]>[[-<+>]>]<<[<]<<<[<]<[<]<<<<<<<      enqueue items and go back to length 1 location
  ]                                            end of enqueuing
  <<[<]>[[-<<<+>>>]>]                          move array1 to its leftmost position
  >>[-<<<<<+>>>>>]                             move pivot
  >>>[-]                                       clear array2 length copy that might be there
  >>>>[[-<<<<<<<<<<<+>>>>>>>>>>>]>]            move array2 to its leftmost position
  >[[-<<<<<<<<<<<<+>>>>>>>>>>>>]>]             move out of range array to its leftmost position
  >>>[-]>[-]>[[-<<+>>]>]<<<[<]>                move queue to the left
]                                              loop on queued ranges
```

# Minified version
```
>,[>+[->+<],]>[->>>>>>>>>>>>>>>+<<<<<<<<<<<<<<<]>>>>>>>>>>>>>>+[[-<
+<+>>]<[->+<]<-[-<<[<]<<<<<<<<<<<<[->>>>>>>>>>>>+<<<<<<<<<<<<]>>>>>
>>>>>>>[>]>]>>>[-<<+<+>>>]<<[->>+<<]<[-<<[<]<<<<<<<<<+>>>>>>>>>>[>]
>]<<[<]<<<<<<<<<[-<<[<]<[->+<]>[>]>]<<[->>>>+<<<<]<[[->+>+<<]>>[-<<
+>>]<[->>[>]>>>>+<<<<<[<]<]>>[>]>>[->+<<<+>>]>[-<+>]>[-<+>]<<>>+<<[
->[->]>[<<[-]>>->>]<<+<<]>[[-]<+>]<[->+<]<<[->>+<<]>>>[->-<<<<<[<]<
<[->>>[>]>>>>>>>>+<<<<<<<<<[<]<<]>>>[>]>>>>>>>+[-<+>]<<<<<<<<[<]>[[
-<+>]>]>[-<+>]>[-<+>]]>[-<<<+<<[<]<<[->>+<<]>>[>]>>>>]<<<<<[<]<<]>>
>[>]>>>>>>>[[-<+<+>>]<[->+<]>[->>[>]>[>]>>+<<<[<]<<[<]<]>>[>]>[>]>>
>[-<<<+>>>]<<<[->>>+[>]>+<<[<]<]>>[-<+>]<[->>[>]>>+<<<[<]<]>>[>]>[[
-<+>]>]<<[<]<<<[<]<[<]<]<<<<<<[[->>>>>>>>[>]>[>]>>>[>]>>+<<<[<]<<<[
<]<[<]<<<<<<<]>>>>[->>>>[>]>[>]>+<<[<]<[<]<<<]>>>>[>]>[>]>>>[-<+<+>
>]<[->+<]<+[->>[>]>+<<[<]<]>>[>]>[[-<+>]>]<<[<]<<<[<]<[<]<<<<<<<]<<
[<]>[[-<<<+>>>]>]>>[-<<<<<+>>>>>]>>>[-]>>>>[[-<<<<<<<<<<<+>>>>>>>>>
>>]>]>[[-<<<<<<<<<<<<+>>>>>>>>>>>>]>]>>>[-]>[-]>[[-<<+>>]>]<<<[<]>]
```

# Final state

* Memory: 0 _sorted array_ 0 0 0 0 0 0 0 0 0 0
* Cursor: 16 cells after array end
* Input: empty (read)
* Output: unchanged


_Note : the first lines need to be modified in order to compute length from the array if not read from the input_

This algorithm, performed on one hundred chars, takes about 53% operations less than the bubble sort !

**But** due to the nature of the recursion engine we implemented, the array size is limited to 255 items.

# Test programm

This program does the same but also print chars at the end

```
>,[>+[->+<],]>[->>>>>>>>>>>>>>>+<<<<<<<<<<<<<<<]>>>>>>>>>>>>>>+[[-<
+<+>>]<[->+<]<-[-<<[<]<<<<<<<<<<<<[->>>>>>>>>>>>+<<<<<<<<<<<<]>>>>>
>>>>>>>[>]>]>>>[-<<+<+>>>]<<[->>+<<]<[-<<[<]<<<<<<<<<+>>>>>>>>>>[>]
>]<<[<]<<<<<<<<<[-<<[<]<[->+<]>[>]>]<<[->>>>+<<<<]<[[->+>+<<]>>[-<<
+>>]<[->>[>]>>>>+<<<<<[<]<]>>[>]>>[->+<<<+>>]>[-<+>]>[-<+>]<<>>+<<[
->[->]>[<<[-]>>->>]<<+<<]>[[-]<+>]<[->+<]<<[->>+<<]>>>[->-<<<<<[<]<
<[->>>[>]>>>>>>>>+<<<<<<<<<[<]<<]>>>[>]>>>>>>>+[-<+>]<<<<<<<<[<]>[[
-<+>]>]>[-<+>]>[-<+>]]>[-<<<+<<[<]<<[->>+<<]>>[>]>>>>]<<<<<[<]<<]>>
>[>]>>>>>>>[[-<+<+>>]<[->+<]>[->>[>]>[>]>>+<<<[<]<<[<]<]>>[>]>[>]>>
>[-<<<+>>>]<<<[->>>+[>]>+<<[<]<]>>[-<+>]<[->>[>]>>+<<<[<]<]>>[>]>[[
-<+>]>]<<[<]<<<[<]<[<]<]<<<<<<[[->>>>>>>>[>]>[>]>>>[>]>>+<<<[<]<<<[
<]<[<]<<<<<<<]>>>>[->>>>[>]>[>]>+<<[<]<[<]<<<]>>>>[>]>[>]>>>[-<+<+>
>]<[->+<]<+[->>[>]>+<<[<]<]>>[>]>[[-<+>]>]<<[<]<<<[<]<[<]<<<<<<<]<<
[<]>[[-<<<+>>>]>]>>[-<<<<<+>>>>>]>>>[-]>>>>[[-<<<<<<<<<<<+>>>>>>>>>
>>]>]>[[-<<<<<<<<<<<<+>>>>>>>>>>>>]>]>>>[-]>[-]>[[-<<+>>]>]<<<[<]>]
<<<<<<<<<<<<<<<<[<]>[.>]
```

