Classes
=======

Graph
-----

.. py:class:: Graph(init)

  Creates a Graph object

  :param init: if integer (V) initialize empty Graph with V vertices. If string (filename) load and populate from file.


  .. py:method:: add_edge(v, w)

    Connects vertices v and w, both must be smaller than V

    :param v: vertice id
    :param w: vertice id


  .. py:method:: adj(v)

     Return a list of vertices adjacent to v

     :param v: vertice id
     :rtype: array of vertice ids


  .. py:method:: to_string()

    Create a string representation of the Graph

    :rtype: string


Digraph
-------

.. py:class:: Digraph(init)

  Creates a Digraph object

  :param init: if integer (V) initialize empty Digraph with V vertices. If string (filename) load and populate from file.


  .. py:method:: add_edge(v, w)

    Connects vertices v and w, both must be smaller than V

    :param v: vertice id
    :param w: vertice id


  .. py:method:: adj(v)

    Return a list of vertices adjacent to v

    :param v: vertice id
    :rtype: array of vertice ids


  .. py:method:: reverse()

    Return the reversed Digraph

    :rtype: Digraph


  .. py:method:: to_string()

    Create a string representation of the Digraph

    :rtype: string



SymbolGraph
-----------
Support Graph objects with named edges.

.. py:class:: SymbolGraph(filename)

    :param filename: file to read


    .. py:method:: graph()

      :rtype: Graph object


    .. py:method:: node_names()

      List of node names corresponding to vertice ids

      :rtype: array of node names



BFSearch
--------

.. py:class:: BFSearch(G, s)

  Does a breadth first search of *G* from *s*.

  :param G: Graph object created by Graph or SymbolGraph
  :param s: Vertex id of the starting point for search


  .. py:method:: bfs(G, s)

    Performs the breadth first search - called from constructor, should *not* be called directly

    :param G: Graph object created by Graph or SymbolGraph
    :param s: Vertex id of the starting point for search


  .. py:method:: has_path_to(v)

    Does (G,s) have a path to vertex v?

    :param v: Vertex id
    :rtype: Boolean


  .. py:method:: path_to(v)

    Make one path to v from s

    :param v: Vertex id
    :rtype: array of vertex ids connecting v to s


  .. py:method:: count()

    Number of visited nodes when exploring (G, s)

    :rtype: number of visited nodes


DFSearch
--------

.. py:class:: DFSearch(G, s)

  Does a depth first search of *G* from *s*.

  :param G: Graph object created by Graph or SymbolGraph
  :param s: Vertex id of the starting point for search


  .. py:method:: dfs(G, v)

    Performs the depth first search - called from constructor, should *not* be called directly

    :param G: Graph object created by Graph or SymbolGraph
    :param v: Vertex id of the starting point for search

  .. py:method:: has_path_to(v)

    Does (G,s) have a path to vertex v?

    :param v: Vertex id
    :rtype: Boolean


  .. py:method:: path_to(v)

    Make one path to v from s

    :param v: Vertex id
    :rtype: array of vertex ids connecting v to s

  .. py:method:: count()

    Number of visited nodes when exploring (G, s)

    :rtype: number of visited nodes


Draw
----

.. py:class:: Draw(digraph=False)

  Prepares for drawing a graph/digraph. Creates a graphviz object and sets the initial graph attributes


  .. py:method:: set_names(names)

    Provide figure with names (from SymbolGraph) instead of ids

    :param names: array [] of names for each vertex id


  .. py:method:: get_name(v)

    Use when drawing the figure, should not normally be called direcctly.

    :param v: vertex id
    :rtype: string


  .. py:method:: node_attr(\*\*kwargs)

    Set graphviz attributes for nodes

    :param \*\*kwargs: List of graphviz keywords (e.g. color='black')


  .. py:method:: edge_attr(\*\*kwargs)

    Set graphviz attributes for edges

    :param \*\*kwargs: List of graphviz keywords (e.g. penwidth='0.75')


  .. py:method:: draw(G, path=[])

    Draws the graph using the configured attributes and, optionally, showing the provided path

    :param G: Graph object
    :param path: list of vertices on the path
