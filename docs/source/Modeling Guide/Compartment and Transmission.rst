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

The **node** and **value** are set by the given parameters during initialization.The **node** cannot be changed once it is set, while the **value** may varies when the model is executing.

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

**Pre_name** is the start of the path which models the transmission.

**Next_name** is the end of the path which models the transmission.

Pre_name and next_name form the unique identifier that marks a path or transmission, and only form one path or transmission.
In other words, the path or transmission cannot be duplicated.

**Expression** is the expression of the transmission, a formula with multiple parameters that indicates the transmission of the path.

**Name2parameters** is a dictionary that contains the key-value of the parameters.
The name of the parameter is the key and the value of the parameter is the value.
The value may change in the future and can get the value of the parameter by it's name.

The constructor of the Path class is as follows:

.. code-block:: python

    def __init__(self, pre_name: str, next_name: str):
        self.expression = ''
        self.name2parameters = {}
        self.pre_name = pre_name
        self.next_name = next_name

The **pre_name** and **next_name** are set by the given parameters during initialization.
Once the **pre_name** and **next_name** are set, they cannot be changed.
The **expression** and **name2parameters** are empty during initialization.

The path class has three other functions:

.. code-block:: python

    def set_exp(self, exp: str):
        self.expression = exp
        return ERRCODE['SUCCEED']

Set the **expression** with the the given string.

.. code-block:: python

    def set_parameters(self, name: str, parameter: float = None, embedding: list = None):
        if name in self.name2parameters.keys():
            return ERRCODE['DUPLICATED_PARAMETER_NAME']
        if parameter is None and embedding is None:
            return ERRCODE['NOT_SINGLE_NOR_EMBEDDING']
        if parameter is None:
            self.name2parameters[name] = ['embedding', embedding]
            return ERRCODE['SUCCEED']
        elif embedding is None:
            self.name2parameters[name] = ['single', parameter]
            return ERRCODE['SUCCEED']
        else:
            return ERRCODE['BOTH_SINGLE_AND_EMBEDDING']

When setting the parameters and embeddings, due to the uniqueness of parameter names, if duplicates are found,
an exception of duplicated parameter name will be returned to the caller.

If the parameter and embedding are both none, an exception of not single nor embedding will be returned to the caller.

If the parameter is none, the embedding will be added to the name2parameters.

if the embedding is none, the parameter will be added to the name2parameters.

Otherwise, an exception of both single and embedding will be returned to the caller.

.. code-block:: python

    def reset_parameters(self, name: str, parameter: float):
        if name not in self.name2parameters.keys():
            return ERRCODE['NO_SUCH_PARAMETER']
        else:
            self.name2parameters[name] = ['single', parameter]
            return ERRCODE['SUCCEED']

When resetting the parameters by given name,
if there is no such name, an exception of no such parameter will be returned to the caller.