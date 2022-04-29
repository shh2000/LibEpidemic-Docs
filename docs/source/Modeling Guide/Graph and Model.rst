Graph and Model
=====

The graph and model integrate the various parts of the compartment model. Graph integrates node and path at the level of directed graph, 
while model integrates compartment and transmission at the level of infectious disease.

Graph
------------

Graph is modeled by class Graph in **compartment/Graph.py**

.. code-block:: python

    class Graph:
        name = ''
        name2node = {}

The Graph class has 2 properties: name and name2node.

**Name** is

**Name2node** is

The constructor of the Graph class is as follows:

.. code-block:: python

    def __init__(self, model_name:str, init_compartment_name:str):
        self.name2node = {}
        self.name = model_name
        init_node = Node(init_compartment_name)
        self.name2node[init_compartment_name] = init_node

The graph class has three other functions:

.. code-block:: python

    def add_single_node(self,node_name:str):
        if node_name in self.name2node.keys():
            return ERRCODE['DUPLICATED_NAME']
        new_node = Node(node_name)
        self.name2node[node_name] = new_node
        return ERRCODE['SUCCEED']


 .. code-block:: python

    def add_next(self, pre_node_name:str, new_node_name:str):
        if pre_node_name not in self.name2node.keys():
            return ERRCODE['NODE_NAME_NOT_FOUND']
        if new_node_name in self.name2node.keys():
            return ERRCODE['DUPLICATED_NAME']
        self.name2node[pre_node_name].add_next(new_node_name)
        new_node = Node(new_node_name)
        self.name2node[new_node_name] = new_node
        return ERRCODE['SUCCEED']

 .. code-block:: python

    def add_edge(self, from_name:str, to_name:str):
        if from_name not in self.name2node.keys() or to_name not in self.name2node.keys():
            return ERRCODE['NODE_NAME_NOT_FOUND']
        if from_name == to_name:
            return ERRCODE['NO_SELF_CIRCLE']
        return self.name2node[from_name].add_next(to_name)


Model
----------------

Model is modeled by class Model in **compartment/Model.py**

.. code-block:: python

    class Model:
        name = ''
        name2compartments = {}
        name2paths = {}

The Model class has 3 properties: name, name2compartments and name2paths.

**Name** is

**Name2compartments** is

**Name2paths** is

The constructor of the Graph class is as follows:

.. code-block:: python

    def __init__(self, name: str, graph: Graph):
        self.name2compartments = {}
        self.name2paths = {}
        self.name = name
        for node_name in graph.name2node.keys():
            compartment = Compartment(graph.name2node[node_name], 0.0)
            self.name2compartments[node_name] = compartment
        for compartment_name in self.name2compartments.keys():
            pre_name = compartment_name
            for next_name in self.name2compartments[compartment_name].node.next_name_list.keys():
                path = Path(pre_name, next_name)
                path_name = pre_name + '->' + next_name
                self.name2paths[path_name] = path


The model class has five other functions:

.. code-block:: python

    def set_compartment(self, name: str, value: float):
        if name not in self.name2compartments.keys():
            return ERRCODE['COMPARTMENT_NAME_NOT_FOUND']
        self.name2compartments[name].value = value
        return ERRCODE['SUCCEED']


.. code-block:: python

    def set_path_exp(self, pre_name: str, next_name: str, exp: str):
        if pre_name not in self.name2compartments.keys() or next_name not in self.name2compartments.keys():
            return ERRCODE['COMPARTMENT_NAME_NOT_FOUND']
        path_name = pre_name + '->' + next_name
        if path_name not in self.name2paths.keys():
            return ERRCODE['PATH_NAME_NOT_FOUND']
        path = self.name2paths[path_name]
        return path.set_exp(exp)


.. code-block:: python

    def set_path_parameters(self, pre_name: str, next_name: str, parameter_name: str, parameter: float = None,
                            embedding: list = None):
        if pre_name not in self.name2compartments.keys() or next_name not in self.name2compartments.keys():
            return ERRCODE['COMPARTMENT_NAME_NOT_FOUND']
        path_name = pre_name + '->' + next_name
        if path_name not in self.name2paths.keys():
            return ERRCODE['PATH_NAME_NOT_FOUND']
        path = self.name2paths[path_name]
        return path.set_parameters(parameter_name, parameter, embedding)


.. code-block:: python

    def get_values(self):
        result = {}
        for name in self.name2compartments.keys():
            compartment = self.name2compartments[name]
            value = compartment.value
            result[name] = value
        return result


.. code-block:: python

    def reset_parameters(self, parameter_name: str, parameter: float):
        for name in self.name2paths.keys():
            path = self.name2paths[name]
            r = path.reset_parameters(parameter_name, parameter)
            if r == ERRCODE['SUCCEED']:
                return r
        return ERRCODE['NO_SUCH_PARAMETER']