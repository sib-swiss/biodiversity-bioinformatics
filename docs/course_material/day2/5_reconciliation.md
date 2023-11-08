## Aim

Convert the molecular species phylogeny into an ultrametric time-calibrated species tree and use this for gene-tree-species-tree reconciliation.

## Learning outcomes

* What is the difference between a molecular and a time-calibrated phylogeny?
* What are gene-tree-species-tree reconciliation algorithms trying to achieve and how?

## Building an ultrametric time-calibrated species tree

![](../../../assets/images/day2/session3/ape_logo.jpg){ style="float: right;" }

There are several tools available for converting molecular phylogenies to ultrametric time-calibrated trees. They usually require as input your molecular phylogeny as well as calibration points (estimates usually from fossils about the ranges of likely divergence times) for one or more nodes on the tree. We will use the **chronos** function of the [ape](http://ape-package.ird.fr/) package in R.

Before we download any genomics data, let’s create a working directory for this exercise, starting by opening a terminal on the Workspace if you’ve not already got one open. Then, from the `/workspace/biodivinfo/` directory, create a new directory (`mkdir`) and navigate into the new directory (`cd`):

```
cd /workspace/biodivinfo/
mkdir Session3
cd Session3/
```

Using the same set of 15 beetle species, but now applying the concatenation approach to be able to use alignments from 1’000 single-copy orthologous groups:

* Aligned each orthogroup
* Filtered/trimmed each orthogroup
* Concatenated the trimmed alignments into a superalignment
* Used RAxML to compute, with bootstraps, the molecular species phylogeny

This took several hours to run, therefore we are not going to try this in the class. Instead, the results are provided for you [here](https://gitlab.com/evogenlab/teaching-repos/biodivinfo/-/blob/main/data/Session3/OGs-1000-moltree-names-rooted.tre) and also pasted below, where the tree has been rooted based on the known outgroup species (`7054_0` & `224129_0`) and where internal labels and species names have been added to make it easier to interpret and compare with the current understanding of beetle phylogeny.

Here is the molecular species tree in Newick format:
```
((((((((50390_0_Diabrotica_virgifera:0.15666,7539_0_Leptinotarsa_decemlineata:0.15804)100:0.05974,217634_0_Anoplophora_glabripennis:0.11339)Chrysomeloidea[100]:0.04091,(7048_0_Sitophilus_oryzae:0.12494,77166_0_Dendroctonus_ponderosae:0.13601)Curculionoidea[100]:0.13858)100:0.02727,116153_0_Aethina_tumida:0.24260)100:0.03487,(115357_0_Harmonia_axyridis:0.06618,41139_0_Coccinella_septempunctata:0.07128)Coccinelloidea[100]:0.17882)88:0.01976,(41895_0_Tribolium_madens:0.02321,7070_0_Tribolium_castaneum:0.02060)Tenebrionoidea[100]:0.28640)100:0.09637,(110193_0_Nicrophorus_vespilloides:0.33251,(1629725_0_Oryctes_borbonicus:0.22252,166361_0_Onthophagus_taurus:0.24064)Scarabaeoidea[100]:0.07437)100:0.05341):0.00483,(224129_0_Agrilus_planipennis:0.31846,7054_0_Photinus_pyralis:0.29250):0.09174)100;
```

Newick format - [Wikipedia](https://en.wikipedia.org/wiki/Newick_format):

* Parentheses indicate hierarchical relationships amongst species
* Branches can be labelled with bootstrap values, e.g. 100
* Branches can also be labelled with names, e.g. Tenebrionoidea
* Notice the semicolon at the end of the tree - it is often forgotten but most tools won’t recognize a file as Newick format if it’s missing!

You can also copy the file from the provided data folder:
```
cp /workspace/biodivinfo/data/Session3/Step1/OGs-1000-moltree-names-rooted.tre .
```

Now to visualise the tree we will, as before, copy and paste this molecular species phylogeny to upload it to [iTOL](https://itol.embl.de/).

<figure>
  <img src="../../../assets/images/day2/session3/itol_form1.jpg" align="center" width=600/>
</figure>

Use the iTOL `Control Panel (Advanced)` to turn on `Display` of `Node IDs` and turn on `Display` as `Text` the `Bootstraps`.

<figure>
  <img src="../../../assets/images/day2/session3/itol_settings1.jpg" align="center" width=250/>
</figure>

Notice that now there is only one node that did not converge to 100% bootstrap support - regarding the placement of the groups of **Tenebrionoidea** & **Coccinelloidea**.

<figure>
  <img src="../../../assets/images/day2/session3/itol_tree1.jpg" align="center" width=600/>
</figure>

If you did not manage to visualise the tree, you can find it on gitpod at:
```
/workspace/biodivinfo/data/Session3/Step1/tree_1000_OGs.jpg
```
Or you can directly see it [here](https://gitlab.com/evogenlab/teaching-repos/biodivinfo/-/blob/main/data/Session3/Step1/tree_1000_OGs.jpg).

We now need to compare our tree to the literature to see if it is in agreement with the current thinking regarding the relations amongst beetle lineages.

**For comparison with the latest beetle phylogeny from the literature (see below):**

<figure>
  <img src="../../../assets/images/day2/session3/itol_tree2.jpg" align="center" width=600/>
</figure>

You should be able to find the internal node labels, provided for you on the tree you have just uploaded on iToL:

<figure>
  <img src="../../../assets/images/day2/session3/beetle_clades.jpg" align="center" width=250/>
</figure>

**Question: Does our 1’000-orthogroup molecular species phylogeny agree with the current understanding of species relationships (see phylogeny below)?**

??? done "Answer"
    Yes! Remember you can invert two branches of a node to facilitate the comparison between the two trees!

<figure>
  <img src="../../../assets/images/day2/session3/beetle_tree.jpg" align="center" width=600/>
  <figcaption>Recent reference on Coleoptera phylogeny: Integrated phylogenomics and fossil data illuminate the evolution of beetles, Cai et al. 2022 </figcaption>
</figure>

!!! note
	Link to [Cai et al. 2022](https://doi.org/10.1098/rsos.211771)




## Building a tree for a dynamic gene family







## Reconciling the gene and species trees
