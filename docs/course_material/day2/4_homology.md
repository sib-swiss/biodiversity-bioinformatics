## Aim

Build a molecular species phylogeny using orthologues identified from an orthology database.

## Learning outcomes

* What is needed as input to build a molecular species phylogeny?
* How do we have confidence in such a species tree?

## Collecting input data from an orthology database

![](../../../assets/images/day2/session2/swiss_orthology.jpg){ style="float: right;" }

There are many publicly accessible orthology databases, or tools that can be used to delineate orthology with your own datasets. Today, we will use data from [OrthoDB](https://www.orthodb.org/). OrthoDB is part of the [SwissOrthology](https://swissorthology.ch/service/search) resource.

From your browser, search for orthodb.org or go to [https://www.orthodb.org/](https://www.orthodb.org/). We will use the OrthoDB website to select our species/clade of interest and query the database to retrieve orthologous groups that we can use to build a species tree.

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_home.jpg" align="center" width=600/>
  <figcaption>OrthoDB v11 homepage</figcaption>
</figure>

Because the beetles are wonderful, we will use them as the example group for exploring the orthology data and building our molecular species tree. We will therefore used the  navigation tool of OrthoDB to narrow our search to available beetle species (Coleoptera): Eukaryota ⇒ Metazoa ⇒ Arthropoda ⇒ Hexapoda ⇒ Insecta ⇒ Holometabola ⇒ Coleoptera.

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_nav1.jpg" align="center" width=600/>
</figure>

The `Search at:` and `Species to display:` boxes should be automatically updated now to show "Coleoptera" and "all 15 selected". Click `Submit` with no search terms to first retrieve all orthologous groups delineated across these 15 species of beetles.

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_search1.jpg" align="center" width=600/>
</figure>

For the orthologous groups returned by the query, summary information is displayed:

* Orthologous group names/descriptions (if available)
* Counts of genes and species per orthologous group

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_results1.jpg" align="center" width=600/>
</figure>

**Question: How many groups in total are returned? What kinds of orthologous groups would we need to find if we want to build a species tree, and why?**

??? done "Answer"
    **14753 groups** are returned. However, it is best to use **single-copy orthologues** to build a species tree, because they easily allow to calculate the exact evolutionary distance between sequences. Using multi-copy orthologues drastically complicates things as you cannot be sure of the homology relationships between all the genes (orthology vs paralogy).

We can use the `Advanced` navigation tool of OrthoDB to narrow our search for orthologous groups that will be useful for building a species phylogeny. Using the "Phyloprofile" filter we can ask the query to return only orthologous groups that are "Present in all species" and that are "Single-copy in all species". Click `Submit` with no search terms to retrieve all orthologous groups delineated across these 15 species of beetle, now with the phyloprofile filtered set.

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_search2.jpg" align="center" width=600/>
</figure>

!!! note
    [Direct URL](https://www.orthodb.org/?universal=1&level=7041&species=7041&singlecopy=1) in case the search with filters did not work properly for you.

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_results2.jpg" align="center" width=600/>
  <figcaption>Results of the filtered query</figcaption>
</figure>

**Question: Did the filtering work - how do you know? How many groups in total are now returned? Why are there so few groups compared to the last query that returned all orthologous 14’753 groups?**

??? done "Answer"
    The filtering worked: we now have only **1225 groups**, all composed of 1 gene per species. The previous query returned more results because a lot of groups contained genes in several but not all species, and these groups were filtered out during this search.

Explore some specific results of your query, e.g. the ones for group [10000at7041](https://www.orthodb.org/?level=7041&species=7041&query=10000at7041) described as "phosphatidylinositol 4-kinase beta".

* The **Group hierarchy** view allows navigating back up the tree of life to the metazoan last common ancestor

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_hierarchy.jpg" align="center" width=700/>
</figure>

* **Functional descriptions** list Gene Ontology (GO) terms and InterPro domains that have been mapped to genes belonging to this orthologous group. They provide clues as to the likely function of all genes in the orthologous group

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_results3.jpg" align="center" width=500/>
</figure>

* **Evolutionary descriptions** summarise the group’s phyletic profile, its relative rate of protein sequence divergence, and the "average" gene architecture (structure in terms of introns and exons and total length in amino acids)

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_results4.jpg" align="center" width=500/>
</figure>

Expand the **Orthologs by organism** table to view members of this orthologous group.

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_results5.jpg" align="center" width=600/>
</figure>

**Questions:**

* **What is the average length (AAs) of these proteins? Are there any substantially longer or shorter proteins than the average?**
* **Why might some be rather different from the average? What impacts could this have when it comes to using these sequences for building a phylogeny?**

??? done "Answer"
    The average length of these proteins is ~930 AAs. There are no substantially longer proteins, but we can notice much shorter proteins (349 AAs, 613 AAs...) that are displayed with one or two exclamation marks `!` depending on the length difference. These short proteins might be real but more likely, they indicate an annotation problem (for example a case of automatic annotation that did not pick-up the full length protein). These proteins can severely impact species tree creation because they will cause a bias in the multiple alignment step.

Additional information about each gene can be viewed by clicking on the chevron buttons `>` or `>>`, _e.g._ for the _Tribolium castaneum_ orthologue.

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_results6.jpg" align="center" width=600/>
</figure>

Before we download any genomics data, let’s create a working directory for this exercise, starting by opening a terminal on the Workspace if you’ve not already got one open. Then, from the `/workspace/biodivinfo/` directory, create a new directory (`mkdir`) and navigate into the new directory (`cd`):

```
cd /workspace/biodivinfo/
mkdir Session2
cd Session2/
```

<figure>
  <img src="../../../assets/images/day2/session2/term1.jpg" align="center"/>
</figure>

To build a phylogeny we need to download the sequences: on the top right of each orthologous group view you can access the protein sequences using "View Fasta".

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_download1.jpg" align="center" width=250/>
</figure>

A new tab will open displaying the protein sequences, copy the URL of the page so we can use it to download the sequences directly in the next step.

<figure>
  <img src="../../../assets/images/day2/session2/orthodb_download2.jpg" align="center"/>
</figure>

Now fetch the fasta formatted sequences from OrthoDB from the command line using `curl`, give the downloaded fasta data a filename (-o) using the orthologous group ID "10000at7041.fasta" and make sure that the URL is placed inside quotes:
```
curl -o 10000at7041.fasta "https://data.orthodb.org/v11/fasta?id=10000at7041&species=7041"
```

<figure>
  <img src="../../../assets/images/day2/session2/curl1.jpg" align="center" width=600/>
</figure>

If fetching from OrthoDB failed, you can get the file from the folder with data files for the practical instead:
```
cp /workspace/biodivinfo/data/Session2/10000at7041.fasta .
```

Use the file explorer on the Workspace to view the downloaded fasta file

<figure>
  <img src="../../../assets/images/day2/session2/fasta1.jpg" align="center"/>
</figure>

We need to replace the **colon** "\_0:" in the protein identifiers with an underscore "\_0\_" because some downstream tools do not accept colons in identifiers. We will perform such **replacement** using the command line function `sed`:
```
sed -i 's/_0:/_0_/g' 10000at7041.fasta
```

<figure>
  <img src="../../../assets/images/day2/session2/fasta2.jpg" align="center"/>
  <figcaption>Note how there are now no longer any colons in the identifiers</figcaption>
</figure>

## Building a tree from single-copy orthologues













Change bad quotes
