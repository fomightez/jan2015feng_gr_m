.. contents::
   :depth: 3.0
..

Real World Examples I: Running Other's Python code
==================================================

Methods sections are good for finding what others used and then now you
can use

NGS Analysis with Python
~~~~~~~~~~~~~~~~~~~~~~~~

-  `Miles et al. 2013. Xbp1 Directs Global Repression of Budding Yeast
   Transcription during the Transition to Quiescence and Is Important
   for the Longevity and Reversibility of the Quiescent State. PMID:
   24204289 <http://www.plosgenetics.org/article/info%3Adoi%2F10.1371%2Fjournal.pgen.1003854>`__

    The W303 reference genome in FASTA format and gene annotations in
    GFF were obtained from the Wellcome Trust Sanger Institute's SGRP
    group. Sequences from each read were mapped to the Saccharomyces
    cerevisiae W303 reference genome using the Tophat application, a
    fast splice junction mapper for RNA-Seq reads [75]. Representation
    of RNA from annotated genes were assessed using HTSeq, a Python
    package developed by Simon Anders at EMBL Heidelberg, with
    quantitative expression calculated proportional to the number of
    reads per length of the modeled exon (MRPKBME). Finally,
    differential gene representation between treatments were assessed
    using the R/Bioconductor package DESeq [76].

-  HTSeq](http://www-huber.embl.de/users/anders/HTSeq/doc/overview.html)
   see manuscript at
   http://biorxiv.org/content/biorxiv/early/2014/02/20/002824.full.pdf
   Simon Anders, Paul Theodor Pyl, Wolfgang Huber HTSeq — A Python
   framework to work with high-throughput sequencing data Bioinformatics
   (2014), in print, online at doi:10.1093/bioinformatics/btu638

    While the main purpose of HTSeq is to allow you to write your own
    analysis scripts, customized to your needs, there are also a couple
    of stand-alone scripts for common tasks that can be used without any
    Python knowledge. See the Scripts section in the overview below for
    what is available.

-  `RSeQC: An RNA-seq Quality Control
   Package <http://dldcc-web.brc.bcm.edu/lilab/liguow/CGI/rseqc/_build/html/>`__
   Example:

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

-  `PyCrac <http://sandergranneman.bio.ed.ac.uk/Granneman_Lab/pyCRAC_software.html>`__
   Example from `Webb et al 2014. PAR-CLIP data indicate that
   Nrd1-Nab3-dependent transcription termination regulates expression of
   hundreds of protein coding genes in yeast. PMID:
   24393166. <http://www.ncbi.nlm.nih.gov/pubmed/24393166>`__ Use of
   several scripts illustrated in `Figure
   1 <http://genomebiology.com/2014/15/1/R8/figure/F1>`__

-  NGS analysis using `The Eel Pond mRNAseq
   Protocol <https://khmer-protocols.readthedocs.org/en/v0.8.4/mrnaseq/>`__

Once you can run Python, you can use others' code
-------------------------------------------------

Github and materials and methods are great resources as well.

Example 1
~~~~~~~~~

`Annotate: Annotation of single-nucleotide variants in the yeast
genome <http://depts.washington.edu/sfields/software/annotate/>`__

Alright let's see if we can run this.

What so we need?

Looking at the excerpt from the documentation below starts to give you a
feel for what you need.

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

Download the source file package and unpack it
''''''''''''''''''''''''''''''''''''''''''''''

The limit of dragging and dropping from a local file system up to
SourceLair is file size up to 5 Mb, therefor use the terminal within
SourceLair to directly download the archived files to SourceLair.

There are two popular commands to do this, ``curl`` and ``wget``. Both
are illustrated, but you just need to do one. Additionally the command
to unpack the arcvhive is included with each. Note that despite the
extension indicating it is a ``tar.gz`` or gzipped tarball, it appears
to only be a ``.tar`` archive and so you just need the ``tar`` command
to extract.

::

    curl http://depts.washington.edu/sfields/software/annotate/src/Annotate-0.1.tar.gz > Annotate.tar
    tar -xf Annotate.tar

-OR-

::

    wget http://depts.washington.edu/sfields/software/annotate/src/Annotate-0.1.tar.gz
    tar -xf Annotate-0.1.tar.gz

Navigate into the unpacked directory now.

::

    cd Annotate-0.1

You'll see from the documentation that 3 of the four files needed to run
this script on the yeast genome are included in the archive with the
original source. Now that you have the script and the accompanying files
unpacked, you just need some data listing mutations.

I am supplying a BED file containing mutations, called
`mutation\_data.bed <https://gist.githubusercontent.com/fomightez/9c435b0f18bf659a4669/raw/54d514b1fa9ce57ec46c5527fbd1eaf3236943e0/mutation_data.bed>`__.

The wget command you need to run on the SourceLair command line terminal
to download the file is given below. You could of course use ``curl`` if
you prefer and can use the above command where it was used as a guide to
writing it. It is important here that the resulting file have the name
``mutation_data.bed`` or be prepared to modify the commands illustrated
below accordingly. (Alternatively you could click the name above and
download it locally and then drag into the SoureLair file pane since it
is a small file.)

::

    wget https://gist.githubusercontent.com/fomightez/9c435b0f18bf659a4669/raw/54d514b1fa9ce57ec46c5527fbd1eaf3236943e0/mutation_data.bed

Unless you have previously installed the Biopython package in your
current SourceLair project, you'll get an error if you try to run the
``annotate.py`` script at this point.

::

    wayne461@scripts:/mnt/project/Annotate-0.1$ python annotate.py
    Traceback (most recent call last):
      File "annotate.py", line 242, in <module>
        from Bio import SeqIO
    ImportError: No module named Bio

You simply need to install the needed package to your SourceLair
project. (Packages or modules (sometimes called ``libraries``) are
simply code by others that provide useful functions and abilities that
go beyond the bare bones Python and are generally specific for certain
sorts of tasks. Not having them as part of bare bones Python cuts down
on use of unnecessary resources. They generally need to be installed or
put some place Python will look for them, and then you can import them
at any time to use them. Many Python distributions include several
packages are common. For example you can see all the modules/packages
that come standard with PythonAnywhere
`here <https://www.pythonanywhere.com/batteries_included/>`__. Any
distribution of Python will include a way of installing additional
packages. For example, PythonAnywhere's instructions are
`here <https://www.pythonanywhere.com/wiki/InstallingNewModules>`__.
SourceLair's are
`here <https://www.sourcelair.com/guides/start/python#install-packages-tools-libraries-etc->`__.)

At the command line terminal of your SourceLair project, type the
following to install the Biopython package.

::

    pip install biopython

Now we should be set to run the ``annotate.py`` script.

Looks like from the documentation the command would be....

::

    python annotate.py --mutations mutation_data.bed --genome S288C_reference_sequence_R64-1-1_20110203.fsa --coding orf_coding_all_R64-1-1_20110203.fasta --non-coding saccharomyces_cerevisiae_R64-1-1_20110208.gff.filtered`

Running that unexpectedly FAILS?!?!?!

Looks good according to documentation. What is going on?

Look at ``annotate.py`` file some. Specifically the docstring at the top
and the text about arguments at the very end. Two of the arguments don't
match what the documentation says are the flags signalling them. The
code is going to run what is in the code; it doesn't know about the
documentation page.

Let's try that command again modifying it to match what the script
itself says.

::

    python annotate.py --input mutation_data.bed --genome S288C_reference_sequence_R64-1-1_20110203.fsa --sequences orf_coding_all_R64-1-1_20110203.fasta --non-coding saccharomyces_cerevisiae_R64-1-1_20110208.gff.filtered

To view the result you can type the following. (Alternatively you can
double-click on the file ``mutation_data.bed.annotated`` in SourceLair's
file navigation panel. You may first need to reload the browser page to
even see it listed in the file navigation pane though.)

::

    head mutation_data.bed.annotated

You should see a breakdown of the possible impacts of each of the
mutations listed in the provided input file.

*Additional Note*
                 

*Note the example mutation data seems unrelated to yeast*

Example data listed as:

::

    chr1   213941196  213941196  A  G
    chr10  942363     942363     C  G

Although the example data included with source and discussed in the
documentation is for yeast S. cerevisiae, the example data listed on the
documentation cannot be yeast. Chromosome 1 of S. cerevisiae is only
230218 bp http://www.genome.jp/dbget-bin/www\_bget?refseq+NC\_001133

Chromsome X of S. cerevisiae is only 745751 bp
http://www.ncbi.nlm.nih.gov/nuccore/BK006943

So both are out of the size range for the chromosomes listed and throws
errors if you try to use those values with the data that comes with the
download of the source file. The specific error is
``IndexError: list assignment index out of range``.

Example 2
~~~~~~~~~

This one will be non-interactive.

`HTSeq <http://www-huber.embl.de/users/anders/HTSeq/doc/install.html#installation-on-macos-x>`__

see manuscript at
http://biorxiv.org/content/biorxiv/early/2014/02/20/002824.full.pdf

Simon Anders, Paul Theodor Pyl, Wolfgang Huber HTSeq — A Python
framework to work with high-throughput sequencing data Bioinformatics
(2014), in print, online at doi:10.1093/bioinformatics/btu638

    While the main purpose of HTSeq is to allow you to write your own
    analysis scripts, customized to your needs, there are also a couple
    of stand-alone scripts for common tasks that can be used without any
    Python knowledge. See the Scripts section in the overview below for
    what is available.
