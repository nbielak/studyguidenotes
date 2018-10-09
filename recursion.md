# Intro to Recursion

function calls itself directly or indirectly

solution to base case is provided and solution of bigger problem expressed in terms of smaller problems

if base case not reached   
    stack overflow problem may arise

## Direct, Indirect, Tail Recursion

direct if function calls itself

indirect if fn1 calls fn2 and fn2 calls fn1

tail recursion: recursive call is the last thing executed by the function
    can be optimized by compiler

## Memory allocation

in main(), memory is allocated to the stack

different copies of local variables called for each level

when base case called
    memory is de-allocated and the process continues

## Disadvantages

same problem solving powers
    every iterive function could be recursive and vice versa

greater time and space requirements
    all functions remain on stack until base case

    number of function calls and overhead

## Advantages

clean and simple way to write code

tree traversals inherently recursive