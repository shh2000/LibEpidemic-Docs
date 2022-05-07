Execute
=====

Executor can use the model and all the methods of each class, and use the expression analysis system to complete the simulation of the compartment model. 
Executor is modeled by class Executor in **Executor/Executor.py**

.. code-block:: python
    
    class Executor:
        model = None

.. figure:: /_static/execute.png
    :width: 500

Executor has 2 functions:
    * parse the expression like the string 'beta*S*I*popu'.
    * calculate the expression to simulate the model.

Executing the SEIR model can be done with only 2 APIs, without programming the principles of infectious disease dynamics models, and without manually writing complex model extensions.
In fact, executing steps is the same to every model, not only SEIR.
    * Use init_compartment to set the init value of each compartment.
    * Use simulate_step to finish all parsing and calculating.

.. code-block:: python
    init_value = {'S': 9995, 'E': 2, 'I': 3, 'R': 0}
    init_compartment(model, init_value)
    executor = Executor(model)
    for index in range(5):
    executor.simulate_step(index)
    visual_compartment_values(model)