Fill formula and parameter
=====

This part of the API is used to fill the dynamic formula and parameters into the compartment model. There are 4 APIs for building the formula and parameters, 
which can be seen at **compartment/Transfer.py**.

init_compartment
------------

.. code-block:: python

    def init_compartment(model: Model, name2value: dict):

set_path_exp
------------

.. code-block:: python

    def set_path_exp(model: Model, pre_name: str, next_name: str, exp: str):

set_path_parameters
------------

.. code-block:: python

    def set_path_parameters(model: Model, pre_name: str, next_name: str, parameter_name: str, parameter: float = None, embedding: list = None):

reset_parameters
------------

.. code-block:: python

    def reset_parameters(model: Model, parameter_name: str, parameter: float):  