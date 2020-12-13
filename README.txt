###################################################################README###################################################################

BRIEF INTRODUCTION:
To further explore trait evolution among groups of species, the computer package BayesTraits performs two analyses. The model of evolution
is MultiState, but the analyses of trait evolution can either be Markov chain Monte Carlo (MCMC) or Maximum Likelihood. However, a known and 
supported phylogeny is required beforehand. Those phylogenies can be generated via a phylogenetic analysis such as BEAST. We will use the
Multistate model of evolution to reconstruct how traits that adopt several discrete states evolve. For analysis we will use MCMC to 
approximate the posterior distribution of the parameter of interest.

A tree and data file are required for each analysis, with the option of a command file. This analysis will examine trait evolution across the
clade Artiodactyla. The character trait is denoted by the different character states "D" and "G", where "D" represents ruminant gut and "G" 
represents a non-ruminant gut. Furthermore, this will test if the two binary traits are correlated. This feature is absence/presence:
(ruminant vs non-ruminant gut). 


HOW TO DOWNLOAD BAYESTRAITS:
Visit the Mark Pagel home page (http://www.evolution.rdg.ac.uk/BayesTraitsV3.0.1/BayesTraitsV3.0.1.html)

Download the 'Windows 64 Alternative Builds -- BayesTraits V3.0.1 - Linux 64'
BayesTraits linux edition is run through a terminal
Make sure the program, data file, tree file, and command file are all saved in the same directory

HOW TO RUN BAYESTRAITS: 
****Copy the following line into the terminal****

./BayesTraitsV3 Artiodactyl.trees Artiodactyl.txt < Command_artio.txt
 (program)	(tree file)	 (date file)	    (command file)



OUTPUT FILES:
~~~(a)LOG TEXT
Artiodactyl.Log.txt - contains the model options and output
The multiple columns exported are explained below:
Iterations: 1,000 iterations of the chain
Lh: the likelihood of the chain
Tree No: the tree number
qDG: transition rate from D to G; q is transition rate and D and G are the character states
qGD: transition rate from G to D
Root P(D): probability the root is in the state of D
Root P(G): probability the root is in the state of G
CetaceaNode P(D): probability this node is in the state of D
CetaceaNode P(G): probability this node is in the state of G

NOTE: Named Cetacea node for the aquatic mammals it is defined by (Porpoise Dolphin FKWhale Whale)
NOTE: Character states are D and G for Artiodactyls (Even-toed Ungulates):
		D--ruminating stomach
		G--no ruminating stomach

~~~(b)SCHEDULE TEXT
Artiodactyl.Schedule.txt - schedule from the MCMC chain contains information about mixing
Mixing is the proportion of proposed changes to a chain that is accepted, and the MCMC model offers changes to parameters.
The multiple columns are used to show how many times an operator was tried and the acceptance rate of each. In addition, if auto tune was used
the rate deviation values, the acceptance rate for that parameter, the average acceptance rate for that iteration, and the mean acceptance
rate were all recorded.

NOTE: This file is used to make sure the chain is mixing correctly


TROUBLESHOOTING:
Those two output files will be uploaded to the same directory. They will be overwritten if not saved under another name, if the same files are
ran again. The command "column -t" does not work to organize the output files, because it separates the headers into multiple columns if there is
a space; i.e., splits "Tree No" into two columns "Tree" and "No" (so the values below do not align correctly). Use Microsoft Excel to view the data. 
These output files are tab separated, thus designed to be used in programs like Microsoft Excel (which has a '.csv' extension [comma separated]).
After running the analysis it will say "Aborted: core dumped" after it is done, but this is due to the annotation after the commands. The program
wants to apply the annotation as a command. If the two output files are exported, the software successfully ran.

Occasionally the output files do not export. I had an issue where the job did not run. To correct this or check if a job had stopped, type "jobs"
to see active and inactive jobs. If there are stopped jobs then type "fg" to complete that working job in the terminal.


TO TEST OTHER ANALYSES AND INCLUDE/EXCLUDE COMMANDS:
Command file used:
1							(line 1)
2							(line 2)
AddTag AquaTag Porpoise Dolphin FKWhale Whale		(line 3)
AddNode CetaceaNode AquaTag				(line 4)
ScaleTrees						(line 5)	
Run							(line 6)

You can switch up the command file by changing the integer in line 2 to "1". This will choose the Maximum Likelihood analysis instead of MCMC.
Maximum Likelihood analysis output files are similar to MCMC however 500 trees are run instead of 1,000 iterations.
WARNING: This will overwrite the previous log and schedule files from the MCMC analysis! To avoid this, copy and paste the tree and text files
and rename them. Run those newly named files and it will create a new log and schedule file.

You can also remove the "ScaleTrees" command in line 5 to incorporate branch lengths into the analysis. Without branch lengths, parsimony is
favored instead of Bayesian parameters

