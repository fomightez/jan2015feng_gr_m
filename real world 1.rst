Real World Examples I: Running Other’s Python code
==================================================

Methods sections are good for finding what others used and then now you
can use

NGS Analysis with Python
~~~~~~~~~~~~~~~~~~~~~~~~

-  `Miles et al. 2013. Xbp1 Directs Global Repression of Budding Yeast
   Transcription during the Transition to Quiescence and Is Important
   for the Longevity and Reversibility of the Quiescent State. PMID:
   24204289`_

    The W303 reference genome in FASTA format and gene annotations in
    GFF were obtained from the Wellcome Trust Sanger Institute’s SGRP
    group. Sequences from each read were mapped to the Saccharomyces
    cerevisiae W303 reference genome using the Tophat application, a
    fast splice junction mapper for RNA-Seq reads [75]. Representation
    of RNA from annotated genes were assessed using HTSeq, a Python
    package developed by Simon Anders at EMBL Heidelberg, with
    quantitative expression calculated proportional to the number of
    reads per length of the modeled exon (MRPKBME). Finally,
    differential gene representation between treatments were assessed
    using the R/Bioconductor package DESeq [76].

-`HTSeq`_ see manuscript at
http://biorxiv.org/content/biorxiv/early/2014/02/20/002824.full.pdf
Simon Anders, Paul Theodor Pyl, Wolfgang Huber HTSeq — A Python
framework to work with high-throughput sequencing data Bioinformatics
(2014), in print, online at doi:10.1093/bioinformatics/btu638

    While the main purpose of HTSeq is to allow you to write your own
    analysis scripts, customized to your needs, there are also a couple
    of stand-alone scripts for common tasks that can be used without any
    Python knowledge. See the Scripts section in the overview below for
    what is available.

-  `RSeQC: An RNA-seq Quality Control Package`_ Example:

    geneBody\_coverage.py

    Read coverage over gene body. This module is used to check if reads
    coverage is uniform and if there is any 5’/3’ bias. This module
    scales all transcripts to 100 nt and calculates the number of reads
    covering each nucleotide position. Finally, it generates a plot
    illustrating the coverage profile along the gene body. NOTE: this
    module requires lots of memory for large BAM files, because it load
    the entire BAM file into memory. We add another script
    “geneBody\_coverage2.py” into v2.3.1 which takes bigwig (instead of
    BAM) as input. It only use 200M RAM, but users need to convert BAM
    into WIG, and then WIG into BigWig.

.. _`Miles et al. 2013. Xbp1 Directs Global Repression of Budding Yeast Transcription during the Transition to Quiescence and Is Important for the Longevity and Reversibility of the Quiescent State. PMID: 24204289`: http://www.plosgenetics.org/article/info%3Adoi%2F10.1371%2Fjournal.pgen.1003854
.. _HTSeq: http://www-huber.embl.de/users/anders/HTSeq/doc/overview.html
.. _`RSeQC: An RNA-seq Quality Control Package`: http://dldcc-web.brc.bcm.edu/lilab/liguow/CGI/rseqc/_build/html/

-  `PyCrac`_ Example from `Webb et al 2014. PAR-CLIP data indicate that
   Nrd1-Nab3-dependent transcription termination regulates expression of
   hundreds of protein coding genes in yeast. PMID: 24393166.`_ Use of
   several scripts illustrated in `Figure 1`_

-  NGS analysis using `The Eel Pond mRNAseq Protocol`_

Once you can run Python, you can user others’ code
==================================================

Github and materials and methods are great resources as well.

Example 1
~~~~~~~~~

`Annotate: Annotation of single-nucleotide variants in the yeast
genome`_

Alright let’s see if we can run this

What so we need?

.. _PyCrac: http://sandergranneman.bio.ed.ac.uk/Granneman_Lab/pyCRAC_software.html
.. _`Webb et al 2014. PAR-CLIP data indicate that Nrd1-Nab3-dependent transcription termination regulates expression of hundreds of protein coding genes in yeast. PMID: 24393166.`: http://www.ncbi.nlm.nih.gov/pubmed/24393166
.. _Figure 1: http://genomebiology.com/2014/15/1/R8/figure/F1
.. _The Eel Pond mRNAseq Protocol: https://khmer-protocols.readthedocs.org/en/v0.8.4/mrnaseq/
.. _`Annotate: Annotation of single-nucleotide variants in the yeast genome`: http://depts.washington.edu/sfields/software/annotate/

::

    =Required Files=
    Four files are required by Annotate:

    1) A BED-formatted file containing mutations. The first five columns of this file must be

    chr start   stop    ref obs

    which are the chromosome of the mutation, the start and stop positions (which can be the same number, for a single-base mutation), the reference allele at that position, and the observed allele (i.e., the mutation). Mutations are then listed one per line. Extra information can be included in the columns to the right of these. Mutation start and stop positions are 1-indexed.

    2) A FASTA file containing the reference genome sequence, in which each chromosome is its own sequence.

    3) A FASTA file containing the reference coding sequences, in which each gene is its own sequence. Currently, the positional information for each gene is parsed from the headers of this file. As such, it is very important to use the same file as is provided by SGD or with this software.

    4) A .GFF-formatted file containing functional non-coding genomic regions.

    Files 2-4 are supplied with Annotate. The most up-to-date versions of these files can be found at the Saccharomyces Genome Database (http://www.yeastgenome.org/download-data/sequence). These files are also based on the most recent S.cerevisiae genome sequence (Saccer3). As such, mutations in the file 1 should be based on Saccer3; mutations called in reference to Saccer2 or a different genome assembly will yield incorrect results.


    ==Running Annotate==
    Annotate is run by executing the annotate.py script (as below), which includes passing some required options that direct the script to the files listed above.

    python annotate.py --mutations FILE1 --genome FILE2 --coding FILE3 --non-coding FILE4

    Depending on the processing speed of your system, Annotate takes about 60 seconds to process 1000 mutations.


    ==Required Options==
    -m, --mutations : BED file containing mutations
    -g, --genome : FASTA file containing genome sequence
    -c, --coding: FASTA file of coding sequences
    -n, --non-coding: GFF file containing non-coding regions


    ==Optional Options==
    -h, --help : Print all options, usage information
    --upstream : Distance (in bp) upstream of gene start codons to include in 5'-upstream annotation (default=500)

I’ll supply a BED file containing mutations, called
`mutation\_data.bed`_.

Looks like the command would then be….

``python annotate.py --mutations mutation_data.bed --genome S288C_reference_sequence_R64-1-1_20110203.fsa --coding orf_coding_all_R64-1-1_20110203.fasta --non-coding saccharomyces_cerevisiae_R64-1-1_20110208.gff.filtered``

FAILS?!?!?!

Looks good according to documentation. What is going on?

Look at ``annotate.py`` file some.

hmmm….
``python annotate.py --input mutation_data.bed --genome S288C_reference_sequence_R64-1-1_20110203.fsa --sequences orf_coding_all_R64-1-1_20110203.fasta --non-coding saccharomyces_cerevisiae_R64-1-1_20110208.gff.filtered``

Hooray!!!

Example 2
~~~~~~~~~

This one will be non-interactive.

`HTSeq`_ see manuscript at
http://biorxiv.org/content/biorxiv/early/2014/02/20/002824.full.pdf
Simon Anders, Paul Theodor Pyl, Wolfgang Huber HTSeq — A Python
framework to work with high-throughput sequencing data Bioinformatics
(2014), in print, online at doi:10.1093/bioinformatics/btu638

    While the main purpose of HTSeq is to allow you to write your own
    analysis scripts, customized to your needs, there are also a couple
    of stand-alone scripts for common tasks that can be used without any
    Python knowledge. See the Scripts section in the overview below for
    what is available.

.. _mutation\_data.bed: https://gist.githubusercontent.com/fomightez/9c435b0f18bf659a4669/raw/54d514b1fa9ce57ec46c5527fbd1eaf3236943e0/mutation_data.bed
.. _HTSeq: http://www-huber.embl.de/users/anders/HTSeq/doc/install.html#installation-on-macos-x
