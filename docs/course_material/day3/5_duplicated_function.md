## Aim

In this exercise, we will do something similar to what we did in the exercise 2 but for a quite different set of genes.

## Learning outcome

Compare and understand the differences between different kinds of input data and the results.

## Exercise

We have used the [OHNOLOGS database](http://ohnologs.curie.fr/) in which you can find lists of genes retained from different Whole Genome Duplications (WGD) in several vertebrate genomes. In this case, we have downloaded the list of **zebrafish** genes that were retained after the teleost-specific WGD (3R). Moreover, we have retrieved the orthologs of these zebrafish 3R retained genes in **mouse**. As mice are not teleosts, their genome hasn't duplicated genes resulting from the 3R WGD, but we can retrieve the ortholog genes of those that were retained in the 3R in zebrafish.

In the `/data` folder of the Gitpod workspace, you can find two files:
`Drerio3Rohnologs_7955.tsv`: zebrafish genes retained after the 3R
`Drerio3Rohnologs_10090.tsv`: mouse orthologs of these genes

Check the number of genes in each list. You can do this with:
```
wc -l Drerio3Rohnologs_*
```

**Questions:**

* **Why do you think they have a different number of genes?**
* **Why does the zebrafish file have roughly twice the number of genes in the mouse file?**
* **Why doesn't it have exactly twice as many genes?**

??? done "Answer"
	* It is perfectly expected since they are genes that were retained after whole genome duplication that happened in the teleost branch and mouse are not teleosts
	* Precisely because these genes are all product of that whole genome duplication, they are all duplicated in zebrafish but not in mouse
	* Because small-scale duplications that happened in both lineages slightly affect the number of genes in each set

Do a GO enrichment analysis with [PANTHER](https://www.pantherdb.org/) of the zebrafish genes as we did in exercise 2.

**Questions:**

* **What kind of GO terms do we see enriched in this list?**
* **What does it tell us about the function of these genes?**
* **Is it different from what we found with the one-to-one orthologs list on exercise 2?**

??? done "Answer"
	* A lot of transport and regulation GO terms, some fish specific GO terms
	* They had a role in important but not essential function in the evolution of teleosts
	* Yes, they are different because we are now looking at genes that were retained after a branch specific whole genome duplication. Effectively, they are expected to be enriched in less essential processes and branch specific processes

Do it again with the mouse orthologs.

**Question: Do we get similar results? Why?**

??? done "Answer"
	All the fish specific terms disappear, as expected given that we are checking mouse genes. Besides that, the results are quite similar in general.

To further explore the function of these genes, do a [TopAnat](https://www.bgee.org/analysis/top-anat/) for the zebrafish and the mouse lists.

**Questions:**

* **What kind of anatomical entities do we see enriched in the zebrafish TopAnat?**
* **Do they make sense given what we saw in the GO enrichment?**
* **What can we say about the function of this set of genes?**
* **Do we see the same in the mouse list? Why?**

??? done "Answer"
	* We see an overrepresentation in larva and tissue related to cognitive function and vision such as brain, eyes, central nervous system, sensory system, photoreceptor array
	* The GO enrichment analysis told us that the gene list were enriched in genes involved in transport and regulation, both of which are essential for the correct functioning of the nervous system, so it does make sense (even if such broad terms could also be associated with other tissues)
	* TopAnat tells us that those genes play an important role in brain response and vision
	* Yes, nearly all top terms are brain tissues. We therefore see similar results as for zebrafish except that for mice eyes are not found to be enriched while they are clearly enriched in zebrafish

We arrived at the end of this course. Now, we would like to invite you to debate about what we just learned and about whatever question you may have. You can also ask us about specific questions related to your work if you are interested.
