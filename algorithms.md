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

