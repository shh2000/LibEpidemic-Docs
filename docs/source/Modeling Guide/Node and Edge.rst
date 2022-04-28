Node and Edge
=====
.. _ModelingGuideStart:

Modeling Guide Start
------------

In compartment models, the "dynamic" part is the process by which a certain number of individuals move from one group to another. 
This process can be modeled using a directed graph. Therefore, the bottom layer of this engine is the nodes and edges of the directed graph. 
Each node models a compartment, and each edge models a term of a differential equation.

Node
------------

Node is modeled by class Node in **compartment/Node.py**

.. code-block:: python

    class Node:
        name = ''
        next_name_list = {}

The node class has 2 properties: name and next_name_list.

**Name** is throughout LibEpidemic, is the unique identifier that marks a node or compartment, and cannot be duplicated.

The **next_name_list** records the subsequent node of this node, the name of the subsequent node is the key, and the fixed value 0 is the value. 
The value may change in the future and is used to mark some properties of the node.


The constructor of the Node class is as follows:


.. code-block:: python

        def __init__(self, name: str):
            self.name = name
            self.next_name_list = {}

Once the **name** is set during initialization, it cannot be changed. The **next_name_list** is empty when initialized.

The Node class has one and only one other function:

.. code-block:: python

        def add_next(self, name: str):
            if name in self.next_name_list.keys():
                return ERRCODE['NO_DUPLICATED_EDGE']
            self.next_name_list[name] = 0
            return ERRCODE['SUCCEED']

When adding subsequent nodes, due to the uniqueness of node names, if duplicates are found, an exception will be returned to the caller.

Edge
----------------

In node-edge level modeling, edges do not contain any properties such as dynamic equations or 
parameter values. Considering that the **next_name_list** in the node class already covers all the information of the graph structure, 
the edge itself does not need to create a class.
