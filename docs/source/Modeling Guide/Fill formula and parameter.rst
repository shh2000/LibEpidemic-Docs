Fill formula and parameter
=====

This part of the API is used to fill the dynamic formula and parameters into the compartment model. There are 4 APIs for building the formula and parameters, 
which can be seen at **compartment/Transfer.py**.

init_compartment
------------

.. code-block:: python

    def init_compartment(model: Model, name2value: dict):

**Init_compartment** is used to initialize values of compartments. It calls **set_compartment** in the model class for each compartment.

set_path_exp
------------

.. code-block:: python

    def set_path_exp(model: Model, pre_name: str, next_name: str, exp: str):

**Set_path_exp** is used to define the principal with a simple string like "beta*S*I*popu" (popu = 1/N). Here are some examples:

.. code-block:: python

    set_path_exp(model, 'S', 'E', 'beta*S*I*popu')
    set_path_exp(model, 'E', 'I', 'alpha*E')
    set_path_exp(model, 'I', 'R', 'gamma*I')

set_path_parameters
------------

.. code-block:: python

    def set_path_parameters(model: Model, pre_name: str, next_name: str, parameter_name: str, parameter: float = None, embedding: list = None):

**Set_path_parameters** is used to fill those parameters with exact figures. Here are some examples:

.. code-block:: python

    set_path_parameters(model, 'S', 'E', 'beta', embedding = [0.3,0.5,0.3,0.3,0.1])
    set_path_parameters(model, 'S', 'E', 'popu', 1.0 / 1000000)
    set_path_parameters(model, 'E', 'I', 'alpha', 0.14)
    set_path_parameters(model, 'I', 'R', 'gamma', 0.2)


reset_parameters
------------

.. code-block:: python

    def reset_parameters(model: Model, parameter_name: str, parameter: float):

**Reset_parameters is used to help researchers build this type of epidemic models:

* Parameters are not static
* Parameters varies with time
* The exact figure of each parameter cannot be determined before simulation

That is, researchers need results from previously simulation of the model to determine the value of parameters afterwards.

Here is an example: researcher use an index calculated by the number of death and infectious individuals called "awareness",
to modify transmission parameter "beta" afterwards.

.. code-block:: python

    for index in range(days):
        tmp_value = model.get_values()
        Dday = gamma*tmp_value['I']*frac_D
        Iday = beta*tmp_value['S']*tmp_value['I']/(1+(Dday/Dcrit)**awareness)
        Ddays.append(Dday*N)
        Dq.append(N*Dcrit*(R0**(1/awareness)-1)*2)
        Idays.append(Iday*N)
        Iq.append(N*Dcrit*(R0**(1/awareness)-1)*2/frac_D)
        reset_parameters(model, 'beta', beta/(1+(Dday/Dcrit)**awareness))
        executor.simulate_step(index)