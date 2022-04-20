Quick Start
=====

Init
------------

To use LibEpidemic to build a model, first initialize a directory under **examples/** by using following commands:

::

    cd Epidemic-Modeling-survey
    cd examples
    mkdir LibEpidemicTest

Then you can create a new python file to write the code:

::

    touch test.py

If you only need to experience the most basic functions, such as building a basic SEIR model to familiarize yourself with the usage of LibEpidemic, you can also simply create a single file with the following command:

::

    cd Epidemic-Modeling-survey
    cd examples
    touch test.py

However, doing so will clutter the file structure and interfere with your subsequent use. Therefore, we do not recommend this.

Import env
----------------


First make sure you have successfully installed the environment dependencies in requirements, then enter the following command in test.py:

.. code-block:: python

    from compartment.Graph import Graph
    from compartment.Model import Model
    from executor.Executor import Executor
    from compartment.Descriptor import vertical_divide
    from compartment.Transfer import init_compartment, set_path_exp, set_path_parameters
    from visual.visual_graph import visual_model
    from visual.visual_model_data import visual_compartment_values

To make sure the environment is ok, you can type:

.. code-block:: python

    print('Welcome to LibEpidemic!')

Then you will see following response:

::

    D:\softwares\python\python.exe D:/ncov/Epidemic-Modeling-survey/examples/test-copy/hello.py
    Welcome to LibEpidemic!

    Process finished with exit code 0

This means that your environment is configured correctly and you can start building infectious disease models using APIs!

The above code can be seen at **examples/test-copy/hello.py**.

Create Structure
----------------

Here you will quickly build a SEIR model using the API provided by LibEpidemic:

.. code-block:: python

    graph = Graph('basic_SEIR', 'S')
    vertical_divide(graph, 'S', ['E', 'I', 'R'])
    model = Model('basic_SEIR', graph)
    visual_model(model)


* The first line initializes a graph containing the S compartment and names it basic_SEIR. 
* The second line uses **vertical_divide** to subdivide the initial S into S, E, I and R, which corresponds to the SEIR model. 
* The third line converts the diagram used to describe the abstract structure into a model in LibEpidemic after determining the structure of the compartment model, providing support for subsequent work. 
* The last line calls the visualization API and prints the structure diagram that builds this model. 

You can see the following image through the output of pyplot after running the above code:


.. figure:: /_static/seir.png
    :width: 500


The above code can be seen at **examples/test-copy/struct.py**.

Formula and Parameters
----------------

Here you need to assign a formula to each edge in the struct to implement the dynamics in the infectious disease model:

.. code-block:: python

    beta = 0.5
    epsilon = 0.1
    gamma = 0.1
    population = 10000
    set_path_exp(model, 'S', 'E', 'beta*S*I*popu')
    set_path_parameters(model, 'S', 'E', 'beta', beta)
    set_path_parameters(model, 'S', 'E', 'popu', 1.0 / population)
    set_path_exp(model, 'E', 'I', 'epsilon*E')
    set_path_parameters(model, 'E', 'I', 'epsilon', epsilon)
    set_path_exp(model, 'I', 'R', 'gamma*I')
    set_path_parameters(model, 'I', 'R', 'gamma', gamma)


This code formally transforms the previously established SEIR model structure into a complete SEIR model, 
including kinetic mechanisms and parameters. 
First, compare the differential equation form of the SEIR model

.. math:: \frac{dS}{dt} = -\frac{\beta \cdot S \cdot I}{N}
.. math:: \frac{dE}{dt} = \frac{\beta \cdot S \cdot I}{N} - \alpha \cdot E
.. math:: \frac{dI}{dt} = \alpha \cdot E - \gamma \cdot I
.. math:: \frac{dR}{dt} = \gamma \cdot I
.. math:: S + E + I + R \equiv N

Lines 5, 8, and 10 in the above code define the dynamic equations between the compartments in the form of expressions. LibEpidemic's engine and compilation system support arbitrary expressions consisting of multiplication and addition. This can cover the vast majority of scenarios in infectious disease models.

Lines 1-4 set the specific value of the parameter, and lines 6, 7, 9, and 11 fill in these four parameters into the expression.

The above code can be seen at **examples/test-copy/param.py**.

Execute
----------------

A complete SEIR has been built, and you can finally use LibEpidemic's engine to execute the model and finish your work!

.. code-block:: python

    init_value = {'S': 9995, 'E': 2, 'I': 3, 'R': 0}
    init_compartment(model, init_value)
    executor = Executor(model)
    for index in range(5):
        executor.simulate_step(index)
        print('_______________________________________')
        print('day {}'.format(index + 1))
        visual_compartment_values(model)

If things go well, you'll get the following results from standard output:

::

    D:\softwares\python\python.exe D:/ncov/Epidemic-Modeling-survey/examples/test-copy/exec.py
    _______________________________________
    day 1
    S : 9993.50075
    E : 3.29925
    I : 2.9000000000000004
    R : 0.30000000000000004
    _______________________________________
    day 2
    S : 9992.05169239125
    E : 4.41838260875
    I : 2.9399250000000006
    R : 0.5900000000000001
    _______________________________________
    day 3
    S : 9990.58289826266
    E : 5.445338476462667
    I : 3.0877707608750007
    R : 0.8839925000000002
    _______________________________________
    day 4
    S : 9989.040466774793
    E : 6.443236116684064
    I : 3.3235275324337676
    R : 1.1927695760875003
    _______________________________________
    day 5
    S : 9987.380524224098
    E : 7.4588550557117115
    I : 3.6354983908587974
    R : 1.525122329330877

    Process finished with exit code 0

This concludes LibEpidemic's Quick Start, you can find the complete code above at **examples/test-copy/exec.py**. You can further experience LibEpidemic by changing the parameter values inside!