# Graphs

 non-linear data structure

 collection of objects, nodes, connected by edges

 in graph no rules for connection between nodes

 tree = special kind of graph

 Graph: G = (V, E)
    g is an ordered pair of a set V of vertices and a set of E of edges

    (a,b) != (b, a) (ordered pair)

Edge representation of two end points

directed: edge is connected one way
undirected: edge is connected two ways

Digraph: graph with all directed edges

Graphs can be used to represent many types of data
    social networks
        facebook: undirected graph
    world wide web
        digraph to represent links

graphs can be used for webcrawling tp get info websites
    graph traversal

## Weighted Graph

some connections in graph more important than others  

associate cost/weight with edge
    edge labeled by weight

self-loop: if end point of edge is the same as the start position

multiedge: if edge appears more than once

simple graph has no self-loops or multiedges 

if |v| = n 
then,
    0 <= |E| <= n(n-1), if directed
    0 <= |E| <= n(n-1)/2, if undirected

graph is dense if # of edges approaching max, sparse otherwise

## Path

walk: sequence of vertices, where adjacent pair connected by edge

path: a walk if no vertices or edges are repeated

trail a walk in which no edges are repeated

graph is strongly connected if path from any vertex to any other vertex

closed walk: starts and ends at the same vertex

length of path is based upon number of edges

simple cycle: no repitition other than start and end vertices

acyclic graph: a graph with no cycle
    e.g. a tree

## Storing a Graph
Edge list rep
two lists
    vertex list O(|V|)
    edge list O(|E|)

vertex identified by value

edge identified by start vertex and end vertex, weight if it's relevent 

## Adjacency Matrix

store edges in matrix
good for dense graphs
efficient in terms of time, but no space

store whether edge attaches

## Adjacency List

only store if connected
linked list

## BFS and DFS for Graphs

### DFS

depth first

requires stack

takes first vertex and pushes onto stack
    visits it

    mark it as visited

take first adjacent vertex, push onto stack, and visits

    mark as visited

    etc

Graphs may have cycles unlike trees
    use boolean visited array

Time Complexity: O(V+E)
### BFS

breadth first

Queue instead of stack

visit first and mark as visited
    push adjacent nodes onto queue
    once visited finishes dequeue first on queue

    explore new first el of queue

Time Complexity: O(V+E) where V is number of vertices in the graph and E is number of edges

## Topological Sort

ordering of vertex
    edge going from u to v
    u comes before v

visited set has all vertexes

stack has vertices that are fully explored

Directed Acyclic Graphs (DAG)

the first vertex in topologicval sorting is always a vertex with in-degree as 0

Topological Sort vs DFS

In DFS, we print a vertex and then recursively call DFS for its adjacent vertices. In topological sorting, we need to print a vertex before its adjacent vertices. 

mod DFS to fit needs

# Dijkstar's Algorithm

find shortest path in graph

works on directed and undirected
    as long non negative number

we need a heap + map
    hash map + binary heap

distance map holds distance

path map holds path to every vertex

generate shortest path tree given root

two sets: 
    one contains vertices included in parth tree

    other includes vertices not yet included in shortest path tree

    at every step we find a vertex wich is in the other set and has a minimum distance from the source

## Steps

1. create a set sptSet (shortest path tree set)
    keeps track of vertices included in shortest path tree
        i.e. whose minimum distance from the source is caluculated and finalized

        starts out empty
2. Assign a distance value to all vertices in the input graph
    initialize all distance values as INFINITE

    Assign distance value as 0 for the source vertex
        so that it will be picked first

3. While sptSet doesn't include all vertices
    a. picka vertex u which is not there in sptSet and has minimum distance value

    b. include u to sptSet

    c. Update distance value of all adjaces vertices of u
        iterate through all adjacent vertices

        for every adjacent vertex v if sum of distance value of u and weight of edge u-v < distance value of v
            updatethe distance value of v

# Dynamic Programming

memoizing so that you don't have to re do work that we have already done
    top down

tabulation: bottom up

algorithic paradigm
    breaking down problems and solving sub problems

## Memoization

look up table for previous solutions

checks whether table is nil or not

!nil, returns val of table[i]

nil and i satisifies base condition, update the look up table with the basze value and return the same

nil and !i satisfies base case, i splits the problem i into subproblems and recursively calls itself to solve them

after recursive calls return, i combines the soultions to the subproblems, updates the lookuptable, and returns the solution for problem i

## Tabulation

initialize the base values of "i"

run a loop that iterates over the remainting values of i

at every iteration i, fn updates the ith entry in the lookuptable by combining the solutions to the previously solved subproblems

rn returns table[n]

## Optimal Substructure Property

dynamic programming:
    overlapping subprohlems
    optimal substructure

problem has optimal substructure property if
    optimal solution can be obtained by using optimal solutions of its sub problems

## Solving a Dynamic Programming Problem

faster than exponential brute methods

easily proved

### Step 1: Classifying a DP Problem

typically, all problems that require maximization or minimization of certain quantities or counting problems that say to count arrangements under certain conditions
    certain probability problems

All satisfy overlapping subproblems property 

most classic DP problems satisfy the optimal substructure property

### Step 2: Decide the State

DP problems about state and their transition

state transition depends on choice of state definition

State: set of params that uniquely identify a certain position or standing in the given problem
    params should be as small as possible to reduce state space

### Step 3: Formulating a Relation among States

hardest part

### Step 4: Adding Memoization or Tabulation for State

store the state answer
    directly access it from memory when needed

## Memoization vs. Tabulation

### Tabulation

bottom up

start at f(0) and go to f(n)

iterative usually

state transition relation is difficult to conceptualize

code gets complex with a lot of conditions

fast bc direct access to previous states from table

if all subproblems must be solved at least once
    bottom up will outperform top-down

all entries in table filled one by one

### Memoization

start at f(n) asking for answers from subproblems down to f(0)

recursive usually

state transition easy to conceptualize

clearer code

slow due to recursion and return statements

if not all subproblems need to be solved
    this will outperform tabulation

all entries in lookup table not necessarily filled

# Heap

## Constraints

heap is a binary tree 
    must have all its nodes in a specific order

    shape must be complete

Complete tree
    all levels of tree must be completely filled
        except last

        last level must have the left most noedes filled

    root node must have all of its children be wither greater than or less than or equal to its children

max heap 
    every node is greater than or equal to parent

min heap is opposite of max heap
    heap order property

    every single node is less than parent

left nodes don't have to be smaller than right nodes

## Growing a Heap

can only ever add node to the left most available spot in the tree

must swap until val doens't violate heap order property

## Removing Node

most heaps remove root node, since usually concerned with min or max value

to maintain shape/structure
    remove and replace root node with left most, lowest-level leaf node

    swap until heap order is satisfied
        swapping with larger of two children

        bubble down

## Queueing Heaps

heaps partially sorted
    there's an order

    max or min is always root

if we know the index of the root node
    manipulate that index to determine where its child nodes live in the array
        2i + 1
        2i + 2

root node always at index 0

heaps implemented as arrays because they are super effienient ways of representing priority queues
    a queue data structure with some additional properties


## Binary Heap

binary heap one data structure to model Priority Queue Abstract Data Structure

In PQ, each el has a priority

el with higher priority served before an el with lower

Complete Binary Tree: every level in the binary tree, except the lowest is completely filled
    all vertices in last level are as far left as possible

Binary Max Heap Property: 
    parent of each vertex, except root, contains value > value of that vertex

If we have binary heap of N elements, its height will not be taller than O(log N)

## Heap Sort

heap is nothin more than a binary tree with some additional rules
    heap structure
        left to right
    ordered as max or min heap

heap sort alg is a sorting technique that is based exclusively upon a binary heap data structure
    find largest el and sort it at the end of an unsorted collection

select root node of a heap and add to end of array

Process:
    1. Build a heap from all of the data

    2. swap root with furthest value and pop

    3. heapify

# Merge Sort

sorts collection by breaking it into half

then sorts those two halves and then merges them together to form one, sorted collection
    recursion

divide and conquer
    breaks down problem into simpler version of self

# Counting Sort

technique based on keys between a specific range

counting num of objs having disting key values

1. take a count array to store the count of each unique object.

2. Modify the count array such that each element at  each index stores the sum of previous counts
    modified count array indicates the position of each object in the output sequence

3. Output each object from the input sequence followd by decreasin its count by 1

O(n+k)
    n is num of els in array

    k is range of input

efficient if the range of input data is not significantly greater than the number of objects

not comparison based sorting
    O(n) run time

often used as a sub-routine to another sorting alg like radix sort

uses partial hashing to count the occurentces of the data object in O(1)

# Radix Sort

lower bound of comparison sort is O(nlogn)

counting sort does it in O(n+k)

do digit by digit sort starting from least significant digit to most significant
    uses counting sort as subroutine

O(d *(n+b))
    d being number of digits

constant factors hidden in asymptotic notation higher for radix sort

quicksort uses hardware caches more effectively

counting sort takes extra space

# Binary Search Trees

allow for fast insertion

binary tree

everything in left sub tree less than root

everything in right sub tree greater than root

tree has pointers
    parent and child

O(n) insertion

# AVL Trees

way to keep binary trees balanced

height of node = level of node
    longest path of node to leaf

    max(height left child, height of right child) + 1

depth from root to node

store heights and when too large, fix

null left/right = -1

require heights of left and right of every node to differ by at most 1

worst case when right subtree has height +1 over left of every node

## AVL Insert

simple BST insertion

fix AVL property from changed node up
    suppose x is lowest node violating AVC

    assume x.right higher

    if x right child is right-heavy or balanced
        RightRotation(x)
    else 
        RightRotation(z)
        LeftRotation(x)

Rotations
    O(1)

    left-rotate - root moves left
    right ^ but right

## AVL Sort

insert n items - O(nlogn)

in-order traversal - O(n)

# Hash Tables

combine array and linked list
    random access

data should tell where it should go

bad at ordering or sorting

use only the data using hashed
    and all the data being ha=shed

deterministic
    reliable

uniformly distribute data

generate very different hash codes for similar data

## Collision

when two pieces of data yield same hash code

want to store both pieices of data 
    shouldn't overwrite data that was there first

## Linear Probing

place in next consecutive element in the array
    wrapping if necessary

hopefully el is somewhere nearby

clustering
    once there's a miss, two adjacent cells will have data

    more likely that cluster will grow

## Chaining

el in array head of linked list

# Linked Lists

data structure consisting of a collection of nodes that represent a sequence

contain a datum and ref to the next el in the list

In Ruby, best to use arrays for built in methods

able to insert/remove els without reallocating or reorganizing data structure

performing operations requiring access to particular els of LL can be cumberome
    e.g. finding last el

## LL Pros

Dynamic
    allocate the needed mem when the program is initialized

    can expand in real time without mem overload

Insertion and deletion easy

easy to build linear data structres such as stacks or queues

## LL Cons

bc of value and point, more mem intensive

have to access nodes sequentially

not stored continuously so takes longe to access el

terrible to reverse traverse single linked list

doubly linked lists with two pointers more memory intensive


# Binary Search

given sorted array, find a given el in array

split in half
    left if smaller

    right if bigger


# Interpolation Search

given a sorted array of n uniformly distributed values in an array

improvement over binary search

bserach always goes to the middle

interpolation goes to different locations according to the value of key being searched
    if val of key is closer to last el
        likely to start toward end side

1. Calculate the val of pos using probe pos formula

2. if it is a match return idx of the item

3. if less, calc the probe pos of the left sub array. otherwise calc the same in the right sub array

4. repeat until a match is found or sub array reduces to zero

O(log log n) -> O(n)

# Quick Sort

Divide and conquer algorithm

picks an el as pivot and partitions the given array around the pivot

various pivot positions:
    first el

    last el

    random el

    median

# Detect Cycle In Graph

disjoint-set data structure
    keeps track of a set  of els partitioned into a number of non-overlapping subsets

union algorithm
    performs two useful operations on such a data structure
        find: determine which subset a particular element is in
            used to determine if two els are in the same subset

        Union: join two subsets into a single subset

Union-Fine Algorithm can be used to check whether an undirected graph contains a cycle or not

# Floyd Warshall

for solving all pairs shortest path

find shortes distanecs between every pair of vertices in a given edge weighted directed graph

initialize the solution matrix as the same as the input graph matrix

update the solution matrix by considering all vertices as an intermediate vertex

one by one pick all vertices

update all shortest paths which include the chosen vertices

# Prim's Minimum Spanning Tree

starts with an empty spanning tree

maintain two sets of vertices

    first set contains vertices already inclued in MST

    second set contains vertices not yet included

considers all the edges that connect the two sets and picks the minimum weight edge from the edges

after picket the edge, moves end point of the edge to the set containing MST

a group of edges connecting two sets of vertices in a graph
    cut in graph theory

    in every step of Prim's alg, we find a cut

    pick the min weight edge from the cut and include in MST set

a spanning tree means all vertices must be connected
    two disjoin subsets of vertices must be connected to make a Spanning Tree

## Algorithm

create a set mstSet tracking the seen vertices

assign a key value to all vertices in the input graph
    
while mstSet doesn't include all vertices
    pick a vertex u which in not in mstSet and has min key value

    include u in mstSet

    update key alue of all adjacent vertices u
        to update, iterate through all adjacent vertices
            for every vertex v, if weight of edge u-v is less than the pervious key value of v, update the key value as weight of u-v

use key values to pick the minimum weight edge from cut
    only used for vertices not included in MST

    key value for these vertices indicate the minimum weight edges connecting them