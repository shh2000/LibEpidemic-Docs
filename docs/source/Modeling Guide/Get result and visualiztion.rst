Get result and visualiztion
=====
You can obtain the numerical results of the simulation of the model or visualization results in the following ways: 

Results
------------

Results can be obtained through function get_values in **compartment/Model.py**

.. code-block:: python
    
        def get_values(self):
            result = {}
            for name in self.name2compartments.keys():
                compartment = self.name2compartments[name]
                value = compartment.value
                result[name] = value
            return result


**Get_vlaues** returns a dictionary that records the mapping between the names and values of compartments.
You can easily get specific values of compartments by **get_value**. For example:

.. code-block:: python

    result = get_value()
    S = result['S']

Visualization
----------------

Visualization can be obtained through 4 functions in **visual/*.py**.

.. code-block:: python

    def visual_graph(graph: Graph):

**visual_graph** is in **visual/visual_graph.py**. It is used to get the structure of graph, like the image below:

.. code-block:: python

    def visual_model(graph: Graph):

**visual_model** is in **visual/visual_graph.py**. It is used to get the structure of model, like the image below:

.. code-block:: python

    def visual_compartment_values(model: Model):

**visual_model** is in **visual/visual_model_data.py**. It is used to print names and values of compartments, like the image below:

.. code-block:: python

    def plot_line(values,log=False):

**plot_line** is in **visual/visual_value_line.py**. It is used to draw the lines for the given values, like the image below: