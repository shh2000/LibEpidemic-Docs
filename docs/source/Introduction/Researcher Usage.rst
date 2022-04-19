Researcher Usage
=====

Researchers can use the framework to build any warehouse model simply and quickly, and execute it with arbitrary parameters to obtain results.

Learning List
------------

Researchers need to learn the whole engine-model-application three-level framework. Including:

* engine
    * node/path: Modeling a directed graph with no multiple edges and no self-loops
    * compartment/transmission: Give node and path epidemiological significance: compartment values and dynamic differential equations
    * graph/model: Integrate node/path and compartment/transmission to build models
* engine-model
    * compiler: Compile the model built by the engine into a scipy method for fitting the default parameters
    * executor: execute a model
* model(parameters)
    * static parameter: That is, the parameters in the traditional compartment model
    * dynamic parameters: Parameter dynamization with time series instead of single value
    * parameter reload: Change any parameter value at any time to model social externalities
* model(strctures)
    * subdivide:
    * add-path:
    * meta-population model

All of the above content will be explained in detail with reference to the api and examples at  :ref:`ModelingGuideStart` .

Function List
----------------

By finishing the Learning list and using it, researchers can use this framework to:

* Build a epidemic model with arbitrary compartment and arbitrary parameter values
* Visualize the structure of the above model
* Simulate the model and get the results as a file or as a visual image
* See how existing research frontier models are constructed
* Use a unified, widely used authoritative dataset to evaluate all models built by yourself and at the forefront of scientific research!

All of the above work can be done with only a few APIs, without programming the principles of infectious disease dynamics models, and without manually writing complex model extensions!
