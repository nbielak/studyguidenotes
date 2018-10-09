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