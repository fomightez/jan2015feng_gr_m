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

-  `PyCrac`_ Example from `Webb et al 2014. PAR-CLIP data indicate that
   Nrd1-Nab3-dependent transcription termination regulates expression of
   hundreds of protein coding genes in yeast. PMID: 24393166.`_ Use of
   several scripts illustrated in [Figure 1](http://genomebiolo

.. _`Miles et al. 2013. Xbp1 Directs Global Repression of Budding Yeast Transcription during the Transition to Quiescence and Is Important for the Longevity and Reversibility of the Quiescent State. PMID: 24204289`: http://www.plosgenetics.org/article/info%3Adoi%2F10.1371%2Fjournal.pgen.1003854
.. _HTSeq: http://www-huber.embl.de/users/anders/HTSeq/doc/overview.html
.. _`RSeQC: An RNA-seq Quality Control Package`: http://dldcc-web.brc.bcm.edu/lilab/liguow/CGI/rseqc/_build/html/
.. _PyCrac: http://sandergranneman.bio.ed.ac.uk/Granneman_Lab/pyCRAC_software.html
.. _`Webb et al 2014. PAR-CLIP data indicate that Nrd1-Nab3-dependent transcription termination regulates expression of hundreds of protein coding genes in yeast. PMID: 24393166.`: http://www.ncbi.nlm.nih.gov/pubmed/24393166
