Compartment and Transmission
=====

In order to move from node-edge to a real compartment model, 
a higher-level class containing node-edge and additional information is needed to model the "node" and "edge" in compartment models. 

In the compartment model, the node function is carried by the compartment, and the edge function is carried by the transmission.

Compartment
------------

Compartment is modeled by class Compartment in **compartment/Compartment.py**

.. code-block:: python

    class Compartment:
        node = None
        value = -1.0

The Compartment class has 2 properties: node and value.

**Node** identifies the compartment. It is a part of the basic graph that models the compartment.

**Value** is the compartment value, which represents the number of people in the comparment.

The constructor of the Compartment class is as follows:

.. code-block:: python

    def __init__(self, node: Node, value: float):
        self.node = node
        self.value = value

The node and value are set by the given parameters during initialization.The node cannot be changed once it is set, while the value varies when the model is executing.

Transmission
----------------

Transmission is modeled by class Path in **compartment/Path.py**

.. code-block:: python

    class Path:
        pre_name = ''
        next_name = ''
        expression = ''
        name2parameters = {}

The Path class has 4 properties: pre_name, next_name, expression and name2parameters.
