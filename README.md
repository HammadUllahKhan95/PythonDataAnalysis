# Classification of the trajectories obtained from mechanistic model of the genetic disease

## Author: Hammad Ullah

**Background**

Metabolism is one of the main requirements for a system in a living organism to be considered alive. The metabolic network itself is the center of the molecular layer of life. In other words, it drives the living cells by providing energy and essential materials needed to survive. Metabolites are intermediate or product of metabolism that are transformed by reactions and activated by genes. The metabolic network is a very complex network consisting of such metabolites and cyclic processes. However, it can be simplified into a toy model with conditional gates AND and OR

**Experimental Design Setup**
The experiment is set up in such a way where we have two copies of the same metabolic network: one is healthy whereas the other one is damaged. Both the networks are fed with the same output and the outputs are being read and classified into one of the four categories i.e. A, B, C and D. In order to obtain the timeseries of the experiment, the initial inputs are randomized a
little and fed into the networks. The following figure shows us the experimental setup as well as what each category signifies.

**Task at hand**
We have been provided a total of 20,000 files with 1000 rows each. There are many parameters provided in the file itself as well as in the filename. The parameters and inputs of interests are:
* L – system’s length
* H – system’s height
* Bool – concentration of ANDs
* b – branching
* n – number of damaged genes
* p – clustering parameter of damage
* switch_upp – average input strength
* inputs_fraction – effective input strength
* outputs_fraction_hlt – effective output strength of the healthy system
* outputs_fraction_dis – effective output strength of the damaged system

Based on the parameters and inputs, each row in a file is assigned a state from one of the A, B, C or D states. The conditions for assigning these states are as such:
* If outputs_fraction_hlt = outputs_fraction_dis and both are nonzero then the state is A
* If outputs_fraction_hlt =/= outputs_fraction_dis and both are nonzero then the state is B
* If outputs_fraction_hlt =/= outputs_fraction_dis and only outputs_fraction_hlt is nonzero then the state is C
* If both are zero then the state is D

After assigning states to each row, the 1000 rows are compacted into 1 row where averages of the parameters and inputs are taken as well as one trajectory class is assigned to that row.

Trajectory classes are based on the presence or absence of a given state in the trajectory of interest. For example, trajectory containing all the states would be ABCD, while containing only A state would be just A, and oscillation between A and B will belong to class AB. There are a total of 15 trajectory classes possible, which are:
* A
* B
* C
* D
* AB
* AC
* AD
* BC
* BD
* CD
* ABC
* ACD
* BCD
* ABD
* ABCD
Once, the trajectory class has been assigned to that row, we move to another file. This way, 20,000 rows are created, each being assigned to one of the 15 trajectory classes. These 20 thousand rows are then stored in a new compacted file which is used to visualize and analyze the results.

