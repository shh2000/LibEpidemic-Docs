Epidemiologist Usage
=====

Epidemiologists need to use the existing mature infectious disease models, make a small amount of expansion according to the actual situation, and then complete the model execution by adjusting the no-code method of the configuration file, and obtain the visualization results

Modeling NPI
------------

Epidemiologists are very concerned about the process by which infectious diseases spread. In the era of COVID-19 outbreak, the SEPIAR mechanism can completely describe the transmission process. With the subdivided extension, the modeling of most scenes can be completed.

Based on this model, epidemiologists can:
* Introduce a subdivided model to model any factors that may affect the spread of the epidemic, such as age, income, country, population mobility, etc.
* Review or deduce the effects of arbitrary policies(More than 20 categories in total, covering the vast majority of specific policies for all countries) by writing code-free configuration files
    * social control policy
    * Case handling policy
    * vaccine policy
* Obtain the model's review(history) or deduction(future) results for the epidemic without using code 

All of the above content will be explained in detail with reference to the api and examples at  :ref:`NPIGuideStart` .

Predicting the need of Medical Resources
----------------

Epidemiologists are very concerned about the occupation of medical resources by infectious diseases and want to predict them in advance. In the era of COVID-19 outbreak, the SPIAHDR mechanism can completely describe the occupancy of medical resources.

As of April 2022, this module functionality is still under development
