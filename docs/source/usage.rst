Usage
=====


Creating a Graph object
-----------------------

.. code-block:: python

  from mjcgraph import graph
  G = graph.Graph('data/mediumG.txt')

  fig = draw.Draw()
  fig.node_attr(label='')
  fig.draw(G)

.. image:: images/graph.png
  :width: 300


Breadth-first search
--------------------

.. code-block:: python

  from mjcgraph import graph
  from mjcgraph import bfs
  from mjcgraph import draw

  G = graph.Graph('data/mediumG.txt')

  bfs = bfs.BFSearch(G, 0)  # make tree with root on vertex 0
  bfpath = bfs.path_to(200) # find path to vertex 200 from 0

  fig = draw.Draw()
  fig.node_attr(label='')
  fig.draw(G, bfpath)

.. image:: images/short.png
  :width: 300


Depth-first search
--------------------

.. code-block:: python

  from mjcgraph import graph
  from mjcgraph import dfs
  from mjcgraph import draw

  G = graph.Graph('data/mediumG.txt')

  dfs = dfs.DFSearch(G, 0)
  dfpath = dfs.path_to(200)

  fig = draw.Draw()
  fig.node_attr(label='')
  fig.draw(G, dfpath)

.. image:: images/long.png
  :width: 300


SymbolGraph
-----------

.. code-block:: python

  from mjcgraph import symbolgraph
  from mjcgraph import draw

  SG = symbolgraph.SymbolGraph('data/routes.txt')

  fig = draw.Draw()
  fig.set_names(SG.node_names())
  fig.node_attr(width='0.3', height='0.3', shape='circle', style='filled',
                color='gray', fontcolor='black', fontsize='8')
  fig.draw(SG.graph())

.. image:: images/symbolg.png
  :width: 300



When plotting you can manually add node name

.. code-block:: python

  node_names = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M']

  G = graph.Graph('data/tinyG.txt')

  fig = draw.Draw()
  fig.set_names(node_names)
  fig.node_attr(style='', fontcolor='black', fontsize='10')
  fig.draw(G)

.. image:: images/node_names.png
  :width: 300


And you can do breadth first search on SymbolGraph

.. code-block:: python

  SG = symbolgraph.SymbolGraph('data/routes.txt')

  b = bfs.BFSearch(SG.graph(), SG.ST['LAX'])
  path = b.path_to(SG.ST['HOU'])

  fig = draw.Draw()
  fig.set_names(SG.node_names())
  fig.node_attr(width='0.3', height='0.3', shape='circle', style='filled',
                color='gray', fontcolor='black', fontsize='8')
  fig.draw(SG.graph(), path)

.. image:: images/symbol_graph_bfs.png
  :width: 300


Digraph
-------

.. code-block:: python

  from mjcgraph import digraph
  from mjcgraph import draw

  DG = digraph.Digraph('../data/tinyDG.txt')

  fig = draw.Draw(digraph=True)
  fig.node_attr(fontsize='8')
  fig.draw(DG, [11, 12, 9, 11])

.. image:: images/digraph_loop.png
  :width: 300
