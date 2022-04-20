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


Visualization
----------------

Visualization can be obtained through 4 functions in **visual/*.py**. 


