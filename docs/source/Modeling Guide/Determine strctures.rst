Determine strctures
=====

From here, you can use the previous 6 classes, along with other APIs, to build the model incrementally. There are 3 APIs for building the compartment model structure 
which can be seen at **compartment/Descriptor.py**.

vertical_divide
------------

.. code-block:: python

    def vertical_divide(graph: Graph, target_node_name: str, divide_name_list: list):

horizontal_divide
------------

.. code-block:: python

    def horizontal_divide(graph: Graph, target_node_name: str, divide_name_list: list):

add_path
------------

.. code-block:: python

    def add_path(graph: Graph, from_name: str, to_name: str):
