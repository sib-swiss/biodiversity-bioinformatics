## Aim

Learn to explore the function of a set of genes as a group using GO enrichment, TopAnat and Bgee expression values.

## Learning outcomes

* What can a GO enrichment analysis tell us about the function of a set of genes of interest?
* What can TopAnat tell us about it?
* What can we learn on gene expression evolution by clustering expression values?

## GO enrichment

The first thing we can do to study the function of these genes as a set is a GO enrichment analysis. It will show us which GO terms are statistically over-represented in the list.

We will do the GO enrichment species per species, for some species, and then we will be able to compare the results. In the file of our list of orthologs we have all the species Ensembl IDs. We will need to select only one species IDs at a time. To do so, download the file and open it in Excel or similar.

Go to the [PANTHER knowledgebase website](https://www.pantherdb.org/).

Let's start with **human**. Paste the complete list of **human IDs** in the box `Enter IDs`, select the species, `Statistical overrepresentation test` and `GO biological processes complete` as shown in the image below. Submit.

<figure>
  <img src="../../../assets/images/day3/session2/go_BP.jpg" align="center"/>
</figure>

!!! note
    The `Statistical overrepresentation test`, compares a test gene list to a reference gene list, and determines whether a particular GO term is overrepresented or not in this list. It is the GO enrichment that we have been referring to. The `Statistical enrichment test` option requires a list of genes with associated numerical values for each gene. It is also an enrichment analysis for another type of data, not the case we are doing here.

Another page will appear asking which reference set of genes to use as the universe for the overrepresentation test. Select the human whole genome list of genes on the right panel as in the image.

<figure>
  <img src="../../../assets/images/day3/session2/panther_form1.jpg" align="center"/>
</figure>

Then, another page will appear with a summary of what you just selected and asking for details on the statistical tests. Make sure the Fischer's exact test and the False Discovery Rate options are selected and launch the analysis.

<figure>
  <img src="../../../assets/images/day3/session2/panther_form2.jpg" align="center"/>
</figure>

Great, we have done the GO enrichment analysis for the human genes in our list. Take a look at the results. The columns that give us the most information are the `Fold Enrichment` that quantifies how much a given GO term is overrepresented in the gene list, and the `Fdr (False Discovery Rate)` that will let us know if a given enrichment is statistically significant.

**Questions:**

* What kind of GO terms do you see enriched?
* Is it what you expected?

??? done "Answer"


Repeat the same analysis for the opossum and the chicken gene lists in new browser tabs. Keep the results of the human gene list open and compare them.

**Questions:**

* Are the results consistent among species?
* How do annotations differ between species?

??? done "Answer"


### Extra question if time permits

Do a GO enrichment analysis with the list of human genes but this time select the `GO molecular function complete` list of GO terms. Check the results.

<figure>
  <img src="../../../assets/images/day3/session2/go_MF.jpg" align="center"/>
</figure>


**Questions:**

* **What has changed?**
* **Are these GO terms more meaningful for understanding the gene function?**

??? done "Answer"


### Tools to visually represent GO enrichment results

* [GO-Figure!](https://gitlab.com/evogenlab/GO-Figure)
    * [Publication](https://www.frontiersin.org/articles/10.3389/fbinf.2021.638255/)
* [ReviGO](http://revigo.irb.hr/)
    * [Publication](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0021800)

## TopAnat

To further investigate the function of the list of orthologous genes, we are now going to go back to [Bgee website](https://www.bgee.org/) and use the TopAnat tool.

TopAnat is an anatomical entity enrichment analysis tool based on the `topGO` R package. It is really similar in methodology to the GO enrichment that you just did but instead of using Gene Ontology terms, it is based on Anatomical entities or, in other words, on tissues or organs (more specifically, on [Uberon](http://obophenotype.github.io/uberon/) identifiers). This tool will be able to tell us in which anatomical entities the genes in our set are being more expressed compared to a background set of genes.

To access the tool in Bgee's website, please go to the top `Analysis` section of the top toolbar and click on `TopAnat: Expression enrichment analysis` (or just click on the red button `Expression enrichment analysis` on the homepage). Then, fill the gene list box with the list of **human genes** in our gene set list. We will not change the background genes for now, so you can directly press the `Submit your job` button after optionally putting your email address and a name to the job. The results may take a bit to appear.

<figure>
  <img src="../../../assets/images/day3/session2/topanat_tool.gif" align="center"/>
</figure>

After a bit, you should get results in the following format at the bottom of the page:

<figure>
  <img src="../../../assets/images/day3/session2/topanat_results.jpg" align="center"/>
</figure>

You can filter the result table based on any column by clicking on the column header (try it with `Fold Enrichment` or with `Fdr` in order to sort results from more significant to least significant).

**Questions**

* **In which anatomical entities do we have more expression than expected compared to the background genes?**
* **Why do you think there is a difference if we compare the results sorting by `Fold enrichment` or by `Fdr`?**

??? done "Answer"


You can open in another tab the results of the first (1) example case proposed by TopAnat (click on the number `1` next to `Examples` on the top of the page). `y`ou will see the kind of results you would get if you tested a gene list linked to the autism spectrum instead. You can always go back to the results from the last job by clicking on the `Recent jobs` button and then the name you gave to the job ID.

**Question: Do you think genes related to autism are more tissue specific than our list of one-to-one orthologs?**

??? done "Answer"


Try to do the same steps for other species such as Macaque or Opossum.

**Questions:**

* **Do you get similar results?**
* **Do you get more similar results between species than when comparing with autism spectrum results?**

??? done "Answer"


## Clustering of homologous organ expression in several species

For this step, we are going to do a principal component analysis of the expression values for the multiple conditions and species. We will be using the `pca_dataset` found in the `/data` folder of Gitpod. In this dataset, each row represents the TPM value of a set of conditions (such as mouse, liver, male, adult) and each column represents a gene from the previously obtained orthologous gene list for the given species.

To launch the analysis, you need to run the `pca_generation.R` script found in the `/scripts` folder using the following command:

```
Rscript pca_generation.R
```

Two figures will be generated in the `/figure` folder, one that colors the points based on species and one based on anatomical entities.

For the first one colored by species, you obtain this graph:

<figure>
  <img src="../../../assets/images/day3/session2/pca_species.jpg" align="center" width=600/>
</figure>

And here is the second one that is colored based on anatomical entities:

<figure>
  <img src="../../../assets/images/day3/session2/pca_anatomy.jpg" align="center" width=600/>
</figure>

**Question: According to the PCA figures, is it the organs or the species that cluster more strongly together?**

??? done "Answer"

