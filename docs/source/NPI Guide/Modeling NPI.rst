Modeling NPI
=====
.. _NPIGuideStart:

NPI Guide Start
------------

Non-pharmaceutical interventions (NPIs) are the factors by which humans, mainly governments or rulers, proactively propose measures to intervene in epidemic.

LibEpidemic use SEPIAR model and the deduction library to help you modeling NPI. 
The deduction library consists of several items, each of which contains a policy, a 0/1 flag, several data and several parameters. 
Among them, the policy is described by a natural language string, and the 0/1 mark indicates whether the policy participates in the deduction. 
The data includes the settings of the policy itself and other data that need to affect the parameters. 
The parameters are the parameters corresponding to this deduction item. 

For example, the policy of "deduce the effect of vaccines" has a 0/1 mark. 
The data are divided into 4 categories: VEI (infection protection rate), VES (symptomatic protection rate), correction of vaccination shots, and vaccination coverage. 
The first two categories are the settings of the policy itself, usually constants or epidemiological characteristic numbers, 
and the last two categories are other data affecting parameters. The parameters corresponding to this deduction item are β(S->E) and trans_PA(P->A).
