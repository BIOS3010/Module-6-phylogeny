# Module 6 - Phylogeny

The purpose of these exercises is to show you of some ways to construct phylogenetic trees based on **multiple sequence alignments (MSA)** which you already should master. To construct the phylogenetic trees we will use http://www.phylogeny.fr/ , a simple online solution suitable for relatively small phylogenetic analyses. For more complex situations with several hundred taxa and/or genes it is common to use a computer cluster for the calculations since they can be computationally very demanding. A computing cluster will be used later in the course, but for this exercise the web resource will be sufficient.

For visualization we will use FigTree (http://tree.bio.ed.ac.uk/software/figtree/). Online visualization tools also exists  but FigTree gives you some more flexibility.



First you will construct trees with distance-based methods, and then using character based methods with an underlying evolutionary model. Finally, you’ll see how things can go wrong if paralogous sequences unwittingly are included in the MSA.

### Storing trees as text.
Trees are usually stored in simple text formats that describe the branching patterns, and the branch lengths. There are currently several text-based formats for storing trees (Nexus, treexml, treedyn etc). One of the simplest is the Newick format, which illustrates phylogenetic trees and guide trees in a series of nested parentheses. Branches sharing a common node are within the same set of parentheses.
For instance, the following tree is described in the Newick format as : (((I,II),(III,IV)),V).


First you will construct trees with distance-based methods, and then using character based methods with an underlying evolutionary model. Finally, you’ll see how things can go wrong if paralogous sequences unwittingly are included in the MSA.

### Storing trees as text.
Trees are usually stored in simple text formats that describe the branching patterns, and the branch lengths. There are currently several text-based formats for storing trees (Nexus, treexml, treedyn etc). One of the simplest is the Newick format, which illustrates phylogenetic trees and guide trees in a series of nested parentheses. Branches sharing a common node are within the same set of parentheses.
For instance, the following tree is described in the Newick format as : (((I,II),(III,IV)),V).

[beta_globin.fa](https://github.com/BIOS3010/Module-5-multiple-alignment/blob/main/beta_globin.fa)  
[divergent_globins.fa](https://github.com/BIOS3010/Module-5-multiple-alignment/blob/main/divergent_globins.fa)  
