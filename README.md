# Module 6 - Phylogeny

The purpose of these exercises is to show you ways to construct phylogenetic trees based on **multiple sequence alignments (MSA)**. To construct the phylogenetic trees, we will use https://ngphylogeny.fr/analysis , a simple online solution suitable for relatively small phylogenetic analyses. For more complex situations with several hundred taxa and/or genes it is common to use a computer cluster for the calculations since they can be computationally very demanding.

For visualization of the inferred tree there are also several options. In this lab we will use the visualisation provided by the ngphylogeny.fr. You can also use iTol (https://itol.embl.de/) which is a good online solution. Or, if you prefer to have a program local on your computer I recommend FigTree (http://tree.bio.ed.ac.uk/software/figtree/). 


### The pipeline

There are three different way of running the pipeline on  https://ngphylogeny.fr/analysis:
- **One Click**: Here you can paste your set of sequences and let the software make decisions on your behalf, the only part you need to decide is what kind of tree you want to build (FastME, PhyML, FastTree etc.). 
- **Advanced**: Allows you to Manually set parameters for the various steps.
- **A la Carte**: Create your own workflow.

We will use the **Advanced** option for these exercises, that way we can modify the steps in the pipeline. The steps are 
i) Multiple Alignment,ii) remove non-homologous characters (in the pipeline this is called "Alignment Curation" iii) phylogenetic tree inference and iv) tree visualization.

Typical phylogenetic pipeline, from  https://ngphylogeny.fr/analysis:  
![](data/pipeline_v2.png)

**Alignments:**
Constructing phylogenetic trees based on molecular data presupposes a good multiple sequence alignment (MSA) of the sequences (DNA or RNA).  There are several different algorithms to choose from with different strengths and weaknesses. Some are very fast, but less accurate. Some are good if the difference between sequences (or the evolutionary distance) to be aligned are large. ncluded in the online pipeline are three commonly used algorithms. For amino acids *muscle* and *MAFFT* are good options.

**Curation:**
Often regions of a multiple sequence alignment can be ambiguously aligned, or sometimes they are plainly wrong. One of the assumptions for making a phylogenetic tree is that the aligned characters in the alignment share the same evolutionary history. If wrongly aligned characters are used for tree inference, there is a chance that the resulting tree is wrong as well. Luckily there are ways of computationally identify uncertain regions of an MSA and automatically remove them. The ngphylogeny.fr pipeline offers a selection of four  of these programs all with slightly different approaches for removing unaligned characters. For this exercise we will use BMGE.

**Tree inference**
The pipeline offers several ways to construct phylogenetic trees: 
  1) FastME 
  2) TNT 
  3) PhyML+SMS 
  4) PhyML 
  5) FastTree 
  6) MrBayes


Of these PhyML and Bayesian (MrBayes) inference are more computational demanding usually take longer time to compute. Parsimony and Distance based methods for tree construction are seldom used in modern phylogenetic analyses, although they sometimes produce trees that are quite similar to those constructed with ML and Bayesian inference.


**Storing trees as text**:
Trees are usually stored in simple text formats that describe the _branching patterns_, and the _branch lengths_. There are currently several text-based formats for storing trees (Nexus, treexml, treedyn etc). One of the simplest is the Newick format, which illustrates phylogenetic trees a series of nested parentheses. Branches sharing a common _node_ are within the same set of parentheses.

For instance, the following tree is described in the Newick format as: (((I,II),(III,IV)),V).

![Simple Tree](data/Fig_newick.png)

Trees in Newick format can in addition to sequence/taxon names have branch length specifying the distance between nodes, and support values for the branches.

The nexus format allows more information to be stored in the same file (trees, alignment, taxa tables with, simple formatting, colors etc.). But we will stick to Newick in this lab.  


###
## Exercise 6.1 Group exercises
For this exercise each group is supposed to provide an answer on:
- Draw  a phylogenetic tree manually (for instance with pen and paper) corresponding to a tree described in the Newick format for your group on Canvas.
- Make a tree based on the sequences of hemoglobin in [Ex1_hemoglobin.fasta](Ex1_hemoglobin.fasta) (you can read about hemoglobin here https://en.wikipedia.org/wiki/Hemoglobin). The abbreviations used in the file are *Hbb* = hemoglobin beta chain; *Hba* = hemoglobin alpha chain; *Glb5_Petma* = globin V from Petromyzon marinus (sea lamprey); *Lgb2_Luplu* = leghemoglobin II from Lupinus luteus (lupines); *Myg_Phyca* = myoglobin from Physeter catodon (sperm whale).

You can set up the pipeline by choosing the **Advancede workflow** option. Use the setting for your group as specified on Canvas.

After setting up the pipeline you will be taken to the next page where you can paste or upload the hemoglobin sequences ([Ex1_hemoglobin.fasta](Ex1_hemoglobin.fasta)). Set the number of bootraps by expanding the menu for the tree inference method under "Configure your workflow". Click the **"+"** sign to exapnd the menu. 

Finally hit **submit** and the sequences will be aligned and the tree constructed automatically. The pipeline will run for a minute or so (depending on the the queueu, the tree construction method, and the number of boostraps). When it is done look for the green button marked "Viewer". 

![Figtree example](data/Tree_Viewer.png)  
_Figure of unrooted tree, with support values_


If you click one of the nodes on the tree a menu appears that allows you to do some simple manipulation of the tree. For instance you can choose where to place the root, by selecting "Reroot on this node". 

Each group should provide the manually drawn tree, and a screenshot (or "proper" figure file) of the tree they generated with the pipeline. Finally answer these questions related to your tree:

```diff
! How do you interpret the bootstrap values and how are these computed?
! Where did you place the root, and why?
! What does the tree tell you about the evolution of globin?
! and in particular the evolution of the two chains of hemoglobin?
! Do you trust your tree? Why or why not?
````

**The rest of the exercises you can do individually or continue working in groups if you prefer. You don't have to upload answers to Canvas**

## Exercise 6.2. Studying Evolution using Protein Sequences  

The vertebrate eye lens is an organ that is already present in the embryo in early stages of development. One remarkable feature of the lens is that is consists of cell layers, like the layers of an onion. Growth takes place at the outside; the inner part of the lens is therefore just as old as its carrier is! This also means that old cells will not be replaced by new ones contrary to what happens in other parts of the body. This imposes high demands in terms of stability to the constituting parts of these cells. Moreover, it must be transparent for light - something that comes in quite handy for a lens. The alpha-crystallin protein is one of the most important constituents of the eye lens. This protein fulfils a key role in maintaining stability and structure of the lens. Its precise working is not completely known, but we know that the protein is a member of the widely occurring small heat shock protein (HSP20) family. The 3-dimensional structure of a distant relative of the protein has been elucidated some time ago. Since alpha-crystallin plays such an important role, it evolves at a very slow rate.

**Calculation of the alpha-crystalline tree**:
Use the protein sequences in the file [Ex2_alphacrystalline.fasta](Ex2_alphacrystalline.fasta) :

Setup the pipeline with the **Advanced workflow** option and calculate a tree with _MAFFT_, _BMGE_ curation, and _PhyML_. Choose _bootstrap_ under Statistical test for branch support in the advanced settings, and set it to 100 .

```diff
! Look at the tree and decide where to place the root. Any surprises?
```
## Exercise 6.3
**A tree with an "error"?**
Calculate a tree using MAFFT and PhyML with 100 bootstrap replicates using the sequences in [Ex3_alphacrystaline.fasta](Ex3_alphacrystaline.fasta).  :

```diff
! Place the root on the most logical branch.
! What is strange about this tree?
! Can you explain this?
```

## Exercise 6.4
**The complete picture**
Finally we use all the alpha crystallins [Ex4_alphacrystaline.fasta](Ex4_alphacrystaline.fasta)

Calculate the tree using MAFFT and PhyML with 100 bootstrap:

```diff
! Where do you place the root?
! How would you describe this tree?
! This should clarify the picture that we got in the previous exercise!
```
