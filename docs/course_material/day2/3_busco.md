## Aim

Use BUSCO to assess the quality of different types of genomic data.

## Learning outcomes

* What are the different BUSCO modes and when should you use them?
* What are the BUSCO outputs and where to find them?

In 2013 I was working on producing genome assemblies for 16 Anopheles mosquitoes, back then we only had short-read technologies and we needed to find a way to assess the quality of the genomes we were producing. I therefore started developing what eventually became BUSCO, now one of the most widely used tools in genomics for assessing the quality of genome assemblies and annotations in terms of gene completeness.

### Assessing genome assemblies for completeness

Before we download any genomics data, let’s create a working directory for this exercise, starting by opening a terminal on the Workspace if you’ve not already got one open. Then, from the `/workspace/biodivinfo/` directory, create a new directory (`mkdir`) and navigate into the new directory (`cd`):

```
cd /workspace/biodivinfo/
mkdir Session1
cd Session1/
```

<figure>
  <img src="../../../assets/images/day2/term1.jpg" align="center"/>
</figure>

Now we can fetch some genome data that we wish to assess. We will work on a small genome so that it does not take too long to run the analyses, hence I have chosen _Saccharomyces jurei_, a newly discovered fungal species with a small genome of 12 Mbps that can be found on the NCBI [https://www.ncbi.nlm.nih.gov/datasets/genome/GCA_900290405.1/](https://www.ncbi.nlm.nih.gov/datasets/genome/GCA_900290405.1/).

The summary statistics are already provided by the NCBI, but not the BUSCO evaluations

<figure>
  <img src="../../../assets/images/day2/asmb_stats.jpg" align="center" width=250/>
</figure>

<figure>
  <img src="../../../assets/images/day2/asmb_chrms.jpg" align="center"/>
</figure>

**Questions:**

* **What is the “Scaffold N50” and what does it mean?**
* **What is the “Scaffold L50” and what does it mean?**

??? done "Answer"
    The N50 is the shortest contig length that needs to be included for covering 50% of the genome. The L50 is the count of smallest number of contigs whose length sum makes up half of a genome size. [More here](https://en.wikipedia.org/wiki/N50,_L50,_and_related_statistics).

We will use the `curl` command and the NCBI Datasets framework to fetch the genome assembly in FASTA format and then unzip the downloaded file:
```
curl -OJX GET "https://api.ncbi.nlm.nih.gov/datasets/v2alpha/genome/accession/GCA_900290405.1/download?include_annotation_type=GENOME_FASTA&filename=GCA_900290405.1.zip" -H "Accept: application/zip"
unzip GCA_900290405.1.zip
```

<figure>
  <img src="../../../assets/images/day2/curl1.jpg" align="center" width=600/>
</figure>

We will take a look at the first few lines of the FASTA file:
```
head ncbi_dataset/data/GCA_900290405.1/GCA_900290405.1_SacJureiUoM1_genomic.fna
```

<figure>
  <img src="../../../assets/images/day2/head1.jpg" align="center" width=600/>
</figure>

Now we have the genome, we can [run BUSCO assessments](https://busco.ezlab.org/busco_userguide.html#running-busco) in the genome mode to quantify gene completeness of this genome assembly.

<figure>
  <img src="../../../assets/images/day2/running_busco.jpg" align="center" width=600/>
</figure>

The four main required input options for us therefore are:

* `-i ncbi_dataset/data/GCA_900290405.1/GCA_900290405.1_SacJureiUoM1_genomic.fna`
* `-o SacJurei`
* `-m genome`
* `-l eukaryota_odb10`

We will also specify the job to use 4 CPUs in order to speed up the task: `-c 4`

The whole command will thus be:
```
busco -i ncbi_dataset/data/GCA_900290405.1/GCA_900290405.1_SacJureiUoM1_genomic.fna -o SacJurei -m genome -l eukaryota_odb10 -c 4
```

On the terminal you can see which steps BUSCO is executing:

* Configuration
* Dataset download
* Metaeuk: this is the default “gene finding” approach

<figure>
  <img src="../../../assets/images/day2/busco_start1.jpg" align="center" width=625/>
</figure>

**Question: What other “gene finding” approaches are possible to use with BUSCO?**

??? done "Answer"
    2 other gene finding approaches are implemented in BUSCO: [Augustus](https://academic.oup.com/bioinformatics/article/24/5/637/202844) (`--augustus` flag) and [Miniprot](https://academic.oup.com/bioinformatics/article/39/1/btad014/6989621) (`--miniprot` flag).

!!! note "Which [BUSCO lineage](https://busco.ezlab.org/list_of_lineages.html) to choose?"
    We used the “eukaryota” dataset:

	* eukaryota_odb10: 255 BUSCOs
		* fungi_odb10: 758 BUSCOs
			* ascomycota_odb10: 1706 BUSCOs
				* saccharomycetes_odb10: 2137 BUSCOs

**Question: Why would you want to use a more specific or a less specific lineage dataset for your BUSCO evaluations?**

??? done "Answer"
    Testing a genome with a more specific lineage dataset will make BUSCO look for clade-specific genes and thus will find more genes. Testing with a less specific lineage dataset will make BUSCO look for genes that are present in a lot of species, thus restricting the number of genes. These genes usually have key functions such as transcription, translation...

The analysis continues with the following steps being printed to the terminal:

* Once metaeuk (first round) is completed, then
* The hmmsearch step follows

<figure>
  <img src="../../../assets/images/day2/busco_hmm_search1.jpg" align="center" width=600/>
</figure>

**Question: What is the hmmsearch step doing?**

??? done "Answer"
    It searches for sequence homologs between the BUSCO database and the genome to evaluate.

The analysis continues with the following steps being printed to the terminal:

* The extraction of missing and fragmented buscos
* A second round of metaeuk predictions
* Then a second round of hmmsearch follows
* To finally give the results

<figure>
  <img src="../../../assets/images/day2/busco_hmm_search2.jpg" align="center" width=600/>
</figure>

The analysis should take about 8 minutes to complete.

<figure>
  <img src="../../../assets/images/day2/busco_end1.jpg" align="center" width=600/>
</figure>

If BUSCO failed, you can get the file from the folder with data files for the practical instead:
```
cp /workspace/biodivinfo/data/Session1/SacJurei.zip .
unzip SacJurei.zip
```

Let’s explore the results of a typical genome assembly assessment run:
```
ls -l SacJurei/
```

<figure>
  <img src="../../../assets/images/day2/ls_results1.jpg" align="center" width=600/>
</figure>

Here's a short summary of the files created by BUSCO:

* **logs**: useful if something went wrong
* **short_summary.specific.eukaryota_odb10.SacJurei.txt**: open the file in the text editor (pink, explorer)
	* Indicates the lineage dataset that was used (blue)
	* Summarises the main results (green)
	* Provides some assembly statistics (yellow)
	* Lists the versions of all the tools used during this run (orange)

<figure>
  <img src="../../../assets/images/day2/busco_results1.jpg" align="center" width=600/>
</figure>

* **short_summary.specific.eukaryota_odb10.SacJurei.json**: JSON version of the previous file
* **run_eukaryota_odb10**: folder with the full results from the run

	<figure>
	  <img src="../../../assets/images/day2/busco_run_eukaryota1.jpg" align="center" width=250/>
	</figure>

	* **busco_sequences:**: PROTEIN and DNA sequences provided
		* **fragmented_busco_sequences**
		* **multi_copy_busco_sequences**
		* **single_copy_busco_sequences**
  * **full_table.tsv**: details of status (Complete, Duplicated, Fragmented, or Missing), genomic locations, scores, and lengths of all searched BUSCOs

	<figure>
	  <img src="../../../assets/images/day2/busco_full_table1.jpg" align="center" width=500/>
	</figure>

	* **hmmer_output**: searching predicted proteins against BUSCO profiles
		* initial_run_results
		* Rerun_results
	* **metaeuk_output**: the gene prediction results
		* combined_nucl_seqs.fas
		* combined_pred_proteins.fas
		* initial_results
		* refseq_db_rerun.faa
		* Rerun_results
	* **missing_busco_list.tsv**: the BUSCOs that were never found

Let’s plot the results of a typical genome assembly assessment run. BUSCO provides [R scripts](https://busco.ezlab.org/busco_userguide.html#companion-scripts) to produce basic plots that summarise the results. Normally you would want to summarise the results from several assessments, _e.g._ the same genome with different lineage datasets, or different versions of your genome assembly build with different workflows/parameters, or the assessments of the genome assemblies of several species side-by-side.

Therefore we need to copy our short summary file into a new folder:

<figure>
  <img src="../../../assets/images/day2/busco_rscript1.jpg" align="center" width=600/>
</figure>

```
mkdir BUSCO_summaries
cp SacJurei/short_summary.specific.eukaryota_odb10.SacJurei.txt BUSCO_summaries/
```

* Make sure you are still in the `Session1` directory! You can use the command `pwd` to check where you are located

Run the python script to plot the summary:
```
python3 /workspace/mambaforge/envs/course/bin/generate_plot.py -wd BUSCO_summaries
```

* This command will produce some warnings and errors but you can ignore them - they are caused by an argument deprecation in the `ggplot2` R package

<figure>
  <img src="../../../assets/images/day2/busco_plots1.jpg" align="center" width=600/>
</figure>

Open the resulting plot file (`busco_figure.png`) using the explorer (left panel of the window) - you can zoom in/out by using Ctrl + scroll up/down (mousewheel) on the figure.

<figure>
  <img src="../../../assets/images/day2/busco_plots2.jpg" align="center" width=600/>
</figure>

Let’s check some of these apparently missing BUSCOs

<!-- AT. Finished page 12 included -->
