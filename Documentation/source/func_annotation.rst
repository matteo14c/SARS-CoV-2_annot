Functional annotation
=====================

The ``annotate.pl`` utility is used to perform functional annotation of SARS-CoV-2 variants. The program can be executed very easily, by running:

::

  perl annotate.pl consolidated_variant_calls > <funct_annot_output_file.csv>

Similar to ``consolidate.pl`` the output is printed directly to your screen (standard output).

.. warning::

   Again, to save everything into a file you need to redirect (*>* symbol). My personal suggestion is to add a *.csv* or a *.tsv* extension to the name of the output file. So that it can be opened directly by a spreadsheet editor software, like for example MS excel or OpenOffice Calc. 

.. warning::

   If/when the docker or Galaxy version of this software are used, the output can be visualized directly in your browser.

The output consists in a simple table, delineated by <tab> (tabulations) and formatted as follows:

================ ========== ========== ============================================================== ================ ======================== ================================ ======================
Genomic position Ref allele Alt allele Funct Elem annot                                               Allele Frequency Epitopes annot           Selection annot                  MFE annot 
================ ========== ========== ============================================================== ================ ======================== ================================ ======================
376              G          T          nsp1:c.111G>T,p.E37D,missense;orf1ab:c.111G>T,p.E37D,missense; 0.166            FGDSVEEVL,1,HLA-C\*08:01 fel:true;meme:true;kind:positive NAi
29742            G          T          3'UTR:nc.G68T,NA,NA,NA;sl5:nc.G15T,NA,NA,N;                    0.735            NA                       NA                               mfe:-5.6;-4.76;-10.93;
================ ========== ========== ============================================================== ================ ======================== ================================ ======================

Annotation of functional genomic elements, consists of 4 fields, separated by commas (**,**):

#. name of the element, followed by ":"

#. relative position (c.= coding, nc.=non coding)

#. amino acid change (NA if a non coding element)

#. predicted effect on protein (NA if a non coding element)

When a variant is overlapped by more than one element, multiple annotations are reported, separated by semicolumns (**;**)

Annotation of epitopes is according to XX et al. The sequence of the epitope/epitopes is reported followed by the number and by the names of the HLAs that are predicted to recognize the epitope. Multiple annotations are separated by semicolumns (**;**). 

For example in *FGDSVEEVL,1,HLA-C\*08:01*, **FGDSVEEVL** is the sequence of the predicted epitope/epitopes, **1** and **HLA-C\*08:01** indicate that the sequence is recognized by just 1 HLA, that is **HLA-C\*08:01**.

Annotation of sites under selection is very simple: **fel:** is used to indicate if the site is under selection according to fel. Possible values are *true* or *false*. **meme** is the equivalent, but for the meme method. The **kind:** field indicates the type of selection: *positive* or *negative*.

The MFE annot column reports **predicted changes** in MFE (minimum free energy) for variants associated with secondary structure elements. Please notice that this annotation does not report the predicted MFE, but the **difference** between the MFE of the element based on the reference genome sequence, with the MFE calculated on the alternative sequence. Negative values indicate a descrease in MFE (a more stable structure). Positive values are suggestive of a less stable structure (increase in MFE). Three values are reported, representing respectively MFE of: *optimal secondary structure*, *the thermodynamic ensemble* and *the centroid secondary structure*. Obviusly there is no absolute cut-off for interpreting these results, however high shifts (>1 or <-1) in MFE might be suggestive of functional implications.

Functional annotation: Important!
---------------------------------

Please notice, that to work properly ``annotate.pl`` needs to have access (read) several annotation files which provide the different types of functional annotations. If these files are not available, the program will exit with an error, complaining that one or more of the files are missing.

These files that are **strictly required** and can be downloaded from the current github repository. The repository itself is updated on a 2 week basis. So it is **highly advised** that the latest version of the files should be downloaded **before** you perform functional annotation.

.. warning::

   In the Galaxy and docker version, these files are updated automatically. All the files need to be (and normally are) in the **same folder** from which ``annotate.pl`` is executed.

The annotation files, all in simple text format include:
#. *genetic_code* -> 3 column file with the standard genetic code

#. *GCA_009858895.3_ASM985889v3_genomic.fna* -> the reference SARS-CoV-2 genome assembly sequence

#. *annot_table.pl* -> a 4 column tabular file with genomic coordinates of functional genomic elements

#. *af_data_new.csv* -> tabular file with allele frequency data

#. *MFE_annot.csv* -> tabular file with Mininum Free Energy predictions for all the possible Single Nucleotide substitutions in secondary structure elements

#. *epitopes_annot.csv* -> tabular file with annotation of predicted epitopes

#. *hyphy.csv* -> tabular file with aa residues under selection according to meme/fel

Please see below for a brief guide that will help you to define additional functional elements in ``annot_table.pl``.

Functional annotation: adding functional elements!
--------------------------------------------------

Functional genomic elements in the genome of SARS-CoV-2 are specified by a four columns tabular format file called ``annot_table.pl``. This file can be used to specify additional functional elements and/or use a personalized annotation. The file has a very simple format: for every element, the first two columns specify the start and end coordinate on the genome. The third column defines the functional class. At the moment 2 different classes are supported: protein coding sequence (CDS) and non-coding (nc). The fourth column is optional and contains an additional comment/name for the functional elements.
Currently the Galaxy/dockerized versions do not allow the specification of additional annotations.