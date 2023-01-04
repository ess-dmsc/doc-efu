File formats
============

This section describes the formats used for loading graphs from file.

Graph/Digraph
-------------
The format consist of two lines with number of vertives (V) and edges (E)
followed by E lines of edges between vertices. The format is the same for
Graph and Digraph.

.. code-block:: console

    $ cat tinyG.txt
    13
    13
    0 5
    4 3
    0 1
    9 12
    6 4
    5 4
    0 2
    11 12
    9 10
    0 6
    7 8
    9 11
    5 3

SymbolGraph
-----------
This format simply consists of lines containing named edges.

.. code-block:: console

    $ cat routes.txt
    JFK MCO
    ORD DEN
    ORD HOU
    DFW PHX
    JFK ATL
    ORD DFW
    ORD PHX
    ATL HOU
    DEN PHX
    PHX LAX
    JFK ORD
    DEN LAS
    DFW HOU
    ORD ATL
    LAS LAX
    ATL MCO
    HOU MCO
    LAS PHX
