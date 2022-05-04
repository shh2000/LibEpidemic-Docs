Determine strctures
=====

From here, you can use the previous 6 classes, along with other APIs, to build the model incrementally. There are 3 APIs for building the compartment model structure 
which can be seen at **compartment/Descriptor.py**.

vertical_divide
------------

.. code-block:: python

    def vertical_divide(graph: Graph, target_node_name: str, divide_name_list: list):

Vertical Divide can subdivide compartments by information relevant to the epidemiological process,
such as asymptomatic, pre-symptomatic, confirmed, isolated, etc.
And such subdivide supports the modeling of individual differences within the same compartment

The following image is a general view of vertical divide:

.. figure:: /_static/vertical_divide.png
    :width: 500

From a local perspective, vertical divide subdivides a compartment into three new compartments.

From a global perspective, vertical divide adds stages in the epidemiological process.

horizontal_divide
------------

.. code-block:: python

    def horizontal_divide(graph: Graph, target_node_name: str, divide_name_list: list):

Horizontal Divide can subdivide compartments by information not relevant to the epidemiological process,
such as age, gender, country, etc.
And such subdivide supports the modeling of individual differences within the same compartment.

The following image is a general view of horizontal divide:

.. figure:: /_static/horizontal_divide.png
    :width: 500

From a local perspective, vertical divide subdivides a compartment into three new compartments.

From a global perspective, vertical divide subdivides different compartments in one stage of the epidemiological process.

add_path
------------

.. code-block:: python

    def add_path(graph: Graph, from_name: str, to_name: str):

Add Path can add an transmission, give it formula and parameters.
It is usually used in combination with the two methods above.

The following image is a general view of horizontal divide:

.. figure:: /_static/add_path.png
    :width: 500

From a local perspective, add path connects two compartments

From a global perspective, add path adds transmission in the model.