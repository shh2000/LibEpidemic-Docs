Graph and Model
=====

The graph and model integrate the various parts of the compartment model. Graph integrates node and path at the level of directed graph, 
while model integrates compartment and transmission at the level of infectious disease.

Graph
------------

Graph is modeled by class Graph in **compartment/Graph.py**

.. code-block:: python

    class Graph:
        name = ''
        name2node = {}

The Graph class has 2 properties: name and name2node.

Model
----------------

Model is modeled by class Model in **compartment/Model.py**

.. code-block:: python

    class Model:
        name = ''
        name2compartments = {}
        name2paths = {}

The Model class has 3 properties: name, name2compartments and name2paths.

