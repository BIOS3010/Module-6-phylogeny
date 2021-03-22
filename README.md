# Module 6 - Phylogeny

**UNDER CONSTRUCTION**

The purpose of these exercises is to show you ways to construct phylogenetic trees based on **multiple sequence alignments (MSA)**. To construct the phylogenetic trees we will use http://www.phylogeny.fr/ , a simple online solution suitable for relatively small phylogenetic analyses. For more complex situations with several hundred taxa and/or genes it is common to use a computer cluster for the calculations since they can be computationally very demanding. A computing cluster will be used later in the course, but for this exercise the web resource will be sufficient.

For visualization we will use FigTree (http://tree.bio.ed.ac.uk/software/figtree/). Online visualization tools also exists  but FigTree gives you some more flexibility.


First you will construct trees with _distance-based methods_, and then using _character based methods_ with an underlying evolutionary model. Finally, you’ll see how things can go wrong if paralogous sequences unwittingly are included in the MSA.

### Storing trees as text.
Trees are usually stored in simple text formats that describe the _branching patterns_, and the _branch lengths_. There are currently several text-based formats for storing trees (Nexus, treexml, treedyn etc). One of the simplest is the Newick format, which illustrates phylogenetic trees a series of nested parentheses. Branches sharing a common _node_ are within the same set of parentheses.
For instance, the following tree is described in the Newick format as : (((I,II),(III,IV)),V).


Trees in Newick format can in addition to sequence/taxon names have branch length specifying the distance between nodes, and support values for the branches. More on support values later.

The nexus format allows more information to be stored in the same file (trees, alignment, taxa tables with, simple formatting, colors etc.). But we will stick to Newick in this lab.  


## The pipeline
Fist we will constructing some trees using a few of the main construction approaches. We will use the pipeline offered under the "phylogenetic analysis" tab at http://www.phylogeny.fr/  This website has a convenient pipeline for the main parts of a phylogenetic analysis: i)  creating multiple sequence alignments, ii) remove non-homologous characters (in the pipeline this is called "curation") iii) phylogenetic tree inference and iv) simple tree visualization. All you need to provide as an input is sequences in fasta-format, and then choose what kind of analysis you want to perform.


Figure 2. Typical phylogenetic pipeline.


**Alignments:**
Constructing phylogenetic trees based on molecular data presupposes a good multiple sequence alignment (MSA) of the sequences (DNA or RNA). You should already be familiar with the concept of sequence alignments. There are several different algorithms to choose from with different strengths and weaknesses. Some are very fast, but less accurate. Some are good if the difference between sequences (or the evolutionary distance) to be aligned are large. Included in the http://www.phylogeny.fr/ are four commonly used algorithms. For this exercise we will use MUSCLE which performs well with amino acids sequences. If you have time you can explore other alignment algorithms, and see if the resulting MSA differs.

**Curation:**
Often regions of a multiple sequence alignment can be ambiguously aligned, or sometimes they are plainly wrong. One of the assumptions for making a phylogenetic tree is that the aligned characters in the alignment share the same evolutionary history. If wrongly aligned characters are used for tree inference there is a chance that the resulting tree is wrong as well. Luckily there are ways of computationally identify uncertain regions of an MSA and automatically remove them. The phylogeny.fr pipeline offers one of these programs called Gblocks. For the protein alignments in this exercise we will be using a less stringent setting than the (see figure, you want to tick of all three boxes under the "less stringent selection" header.

**Tree inference:**
The pipeline offers several ways to construct phylogenetic trees: 1) Maximum Likelihood (ML), 2) Parsimoy, 3) Distance based Neighbor joining and 4) Bayesian inference with MrBayes. Of these ML (with bootstrap) and Bayesian inference are more computational demanding than the other two, and usually take longer time to compute. Parsimony and Distance based methods for tree construction are seldom used in modern phylogenetic analyses, although they sometimes produce trees that are quite similar to those constructed with ML and Bayesian inference. In this exercise we will do both Neighbor joining and ML for comparison.



###

[beta_globin.fa](https://github.com/BIOS3010/Module-5-multiple-alignment/blob/main/beta_globin.fa)  
[divergent_globins.fa](https://github.com/BIOS3010/Module-5-multiple-alignment/blob/main/divergent_globins.fa)  



**Warm-up exercise**

```diff
! Draw manually (e.g. with pen an paper) a phylogenetic tree corresponding to the tree described as follows in the Newick format:
! ((((A,B),C),(D,E)),F).
```

# Individual exercises:
## Exercise 1
For the first exercise we will use the sequences of hemoglobin in Ex_1_hemoglobin.fasta (you can read about hemoglobin here https://en.wikipedia.org/wiki/Hemoglobin).  :

The abbreviations used in the file are
_Hbb_ = hemoglobin beta chain;  
_Hba_ = hemoglobin alpha chain;  
_Glb5_Petma_  = globin V from Petromyzon marinus = nineeye;  
_Lgb2_Luplu_ = leghemoglobin II from Lupinus luteus = lupines  
_Myg_Phyca_ = myoglobin from Physeter catodon = sperm whale  



There are three different choices under the "phylogenetic analysis" tab on http://www.phylogeny.fr/:
- **One Click**: Here you can paste your set of sequences and let the software make decisions on your behalf (Each step is optimized for your data).
 - **Advanced**: Allows you to Manually set parameters for the various steps.
 - **A la Carte**: Create your own phylogeny workflow using more programs available.

We will use the **"A la Carte" option for these exercises, that way we will have full control of all the steps in the pipeline.

Lets get started. First, we will make an Neighbor Joining tree.
You can set up the pipeline after choosing the "A la Carte" option (see figure):


 - For Multiple alignment Choose **MUSCLE**
 - Make sure **Gblocks** is chosen
 - Choose **ProtDist/FastDist + Neighbor** as the tree inference method
 - **TreeDyn** as tree visualization.  
 - If you click _step by step_ you will get an output for each step of the pipeline. This allows you to inspect the result for each step of the pipeline as well as make adjustments (if necessary) and save intermediate files for later use.
 - Finally click **create workflow**.


This will take you to a new page where you can paste the hemoglobin sequences (or use the file Ex1_globin.fasta). Hit **submit** and the sequence alignment will be constructed. The graphical output shows you how conserved the characters in the alignment are compare to the BLOSUM62 score:  Max: 3.0      Mid: 1.5      Low: 0.5 . Higher scoring regions are more conserved. You are given the option to save the **MSA** in several formats if you want to. This is not strictly necessary for this exercise since the alignment was done quite quickly. But if it had taken a long time (for larger alignments this step can take hours!) you probably would have wanted to save the result for safekeeping.

Click "next step".
Then: Make sure all three boxes under the "less stringent selection" is marked. Hit "submit". Now you will have a graphical representation of the curation process. Colored residues are considered conserved (corresponding to the high BLOSUM62 score). The blue line underneath the alignment shows which regions that have passed the curation process. If you remembered to mark all three "less stringet" options it should also say something along these lines:

	"New number of positions in input.fasta-gb:  142  (85% of the original 167 positions)"

Which means that 15% of the alignment has been removed since it might be ambiguously aligned. If you inspect the alignment, you will see that the parts that have been excluded are the beginning and end, as well as a region in the middle of the alignment. All of these contains large gaps, which are notoriously hard to align. Once again you can save the result if you want. Then go to the next page (i.e. click "next step")

In the phylogeny settings sett bootstraps to 100, the substitution model to "Jones-Taylor-Thornton matrix" (often abbreviated JTT). Click "submit", wait for a few seconds and the first tree is ready! Save it to your computer in the newick format. You can now inspect it uisng use the (limited) tree viewing option in the pipeline OR:
To visualize the trees properly I recommend to use FigTree (http://tree.bio.ed.ac.uk/software/figtree/). This program offers ways to rearrange the tree, change fonts, color branches etc. It also allows you to export the trees in commonly used graphic formats (jpg, png, pdf, bmp). I highly recommend PDF or SVG as these are vector graphics which can be easily processes and "made pretty" in other graphics programs (e.g. Inkscaped, Illustrator etc). .

Download, install and run FigTree. Open the tree you just saved (click "file" and "open"). Click OK when you are asked for a name for the nodes/branches. Now you are looking at an unrooted tree without bootstrap values printed. First, we should add the bootrap values. You will have to go to the menu option "Branch Lables" and set the labels to be displayed to "label" to see the bootstrap values.

Now lets fix the root. For this particular tree we can choose to set the root between the hemoglobin sequences and the other version of globin. To achieve this, mark the branch leading to the tips called HBA_xxx and HBB_xxx. Then Click "Reroot" (see figure 3).


Figure 3: unrooted NJ tree, with bootstrap


How do you interpret the boostrap values and how are these computed? What does the tree tell you about the evolution of globin and in particular the evolution of the two chains of hemoglobin?

Now repeat the process, that is run the pipeline one more time, but this time choose PhyML (which is a Maximum Likelihood algorithm) in the phylogeny-step and set the number of bootstraps to 100. Run the analysis. You will now be asked for an email address, since this process will take some time. It’s still a relatively small dataset, so the running time should be about ten minutes (you can have a break if you need one). This shows that ML with the same number of bootraps takes quite some time compared to NJ, even for such a small dataset. Just imagine how long it will take for a dataset with a much longer genes and hundreds of taxa!

When it is finished, save the tree and look at the result in FigTree. Compare to the NJ result. Do you see any differences?

If you want to proceed before this tree is finished, just open a new tab in your browser and set up a new pipeline, proceed to the next exercise.


## Exercise 2. Studying Evolution using Protein Sequences  

The vertebrate eye lens is an organ that is already present in the embryo in early stages of development. One remarkable feature of the lens is that is consists of cell layers, like the layers of an onion. Growth takes place at the outside; the inner part of the lens is therefore just as old as its carrier is! This also means that old cells will not be replaced by new ones contrary to what happens in other parts of the body. This imposes high demands in terms of stability to the constituting parts of these cells. Moreover, it has to be transparent for light - something that comes in quite handy for a lens...
 The alpha-crystallin protein is one of the most important constituents of the eye lens. This protein fulfills a key role in maintaining stability and structure of the lens. Its precise working is not completely known, but we know that the protein is a member of the widely occurring small heat shock protein (HSP20) family. The 3-dimensional structure of a distant relative of the protein has be elucidated some time ago. Since alpha-crystallin plays such an important role, it evolves at a very slow rate.

Calculation of the alpha-crystalline tree
Use these protein sequences in the file Ex2_alphacrystalline.fasta_:


Calculate the tree with _Muscle_, _"less stringent"_ curation setting and _ML_, this time choose "Approximate Likelihood-Ratio Test (aLRT)" instead of bootstrap since it is much faster. Look at the tree in FigTree. Any surprises?

## Exercise 3
**A tree with an "error"?**
Calculate a tree using Muscle and ML with Approximate Likelihood-Ratio Test (aLRT) with sequences (Ex3_alphacrystaline_v2.fasta).  :

Place the root on the most logical branch. What is strange about this tree? Can you explain this?

## Exercise 4
The complete picture
Finally we use all the alpha crystallins (Ex4_alphacrystaline_v3.fasta)

Calculate the tree using Muscle and ML with Approximate Likelihood-Ratio Test (aLRT) .  :


Where do you place the root? How would you describe this tree?
This should clarify the picture that we got in the previous exercise? Comment!  
