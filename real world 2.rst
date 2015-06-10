.. contents::
   :depth: 3.0
..

Real World Examples II: Using APIs
==================================

Plotly
------

`Plotly <https://plot.ly/~wayne461/42/file-size-distribution-of-all-105222-protein-data-bank-entries-as-of-jan-7-2015/>`__

This will be a non-interactive demo of a script running on `Domino Data
Lab <http://www.dominodatalab.com/>`__.

1. Look at date and stats of plot
   `here <https://plot.ly/~wayne461/42/file-size-distribution-of-all-105222-protein-data-bank-entries-as-of-jan-7-2015/>`__

2. Script will be run.

3. Look at date and stats of plot
   `here <https://plot.ly/~wayne461/42/file-size-distribution-of-all-105222-protein-data-bank-entries-as-of-jan-7-2015/>`__

Additional help with plotting biological data via plotly - `Exploratory
bioinformatics with plot.ly and IPython notebook: Visualizing gene
expression data <https://plot.ly/ipython-notebooks/bioinformatics/>`__
(That
`notebook <https://github.com/plotly/IPython-plotly/tree/master/notebooks/bioinformatics>`__
on github.)

Yeastmine
---------

`YeastMine <http://yeastmine.yeastgenome.org/yeastmine/begin.do>`__ has
a `Python web service
API <http://yeastmine.yeastgenome.org/yeastmine/api.do?subtab=python>`__

More information about YeastMine:

-  `Page about it at Saccharomyces Genome Database
   (SGD) <http://www.yeastgenome.org/help/analyze/yeastmine-help-page>`__

-  `Paper about implementing Intermine system with SGD to make
   YeastMine <http://www.ncbi.nlm.nih.gov/pubmed/22434830>`__

I'll demo Query Builder and where to get Python code fragments for
designed queries.

Example of integrating YeastMine code fragments into your work
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Plan:

Use Yeastmine to convert information into a table into more useful form.

Initial steps will be non-interactive in the interest of time.

Those steps will produce

::

    table_4_gene_list = ["YBL091C-A", "YBL059W", "YBR090C", "YBR186W", "YBR219C", "YBR230C", "YCL005W-A_1", "YCL005W-A_2", "YCR028C-A", "YCR097W_2", "YDL219W", "YDL189W", "YDL137W", "YDL125C", "YDL082W", "YDL079C", "YDL064W", "YDR059C", "YDR099W", "YDR305C", "YDR318W", "YDR367W", "YDR381W", "YDR381C-A", "YDR535C", "YER003C", "YER007C-A", "YER014C-A", "YER044C-A", "YER131W", "YER179W", "YFL039C", "YFL034C-B", "YFL031W", "YFR045W", "YGL251C", "YGL187C", "YGL183C", "YGL033W", "YGR029W", "YGR183C", "YGR225W", "YHR012W", "YHR039C-A", "YHR041C", "YHR079C-A", "YHR123W", "YHR141C", "YHR218W", "YIL148W", "YIL111W", "YIL073C", "YIL004C", "YJL189W", "YJL041W", "YJL031C", "YJL024C", "YJR079W", "YJR094W-A", "YJR112W-A", "YKL006C-A", "YKR005C", "YLL050C", "YLR054C", "YLR078C", "YLR128W", "YLR199C", "YLR202C", "YLR211C", "YLR275W", "YLR333C", "YLR445W", "YML085C", "YML067C", "YML036W", "YML025C", "YML024W", "YML017W", "YMR194C-B", "YMR242C", "YMR292W", "YNL312W", "YNL138W-A", "YNL130C", "YNL066W", "YNL050C", "YNL044W", "YNR053C", "YOL047C", "snR17A", "YOR318C", "YPL241C", "YPL230W", "snR17B", "YPR010C-A", "YPR153W"]

Now replace the example list in the code below and run the code of
``finding_genes_in_list_with_SGD_Systematic_Name.py`` found below.

::

    #!/usr/bin/env python

    ## USAGE: TAKES A LIST OF GENES PROVIDED IN THE LONG SGD SYSTEMATIC NAME FORM
    ## AND COLLECTS MORE USER FRIENDLY VERSION OF NAME AND INFORMATION FOR EACH GENE.

    ## Example input:
    ## ["YPR187W", "YPR202W"]

    ## Example output:
    ## S000006391 YPR187W RPO26 RNA POlymerase S. cerevisiae Rpo26p RPB6 ABC23 ORF RNA polymerase subunit ABC23; common to RNA polymerases I, II, and III; part of central core; similar to bacterial omega subunit
    ## S000006406 YPR202W None None S. cerevisiae None None ORF Putative protein of unknown function; similar to telomere-encoded helicases; down-regulated at low calcium levels; YPR202W is not an essential gene; transcript is predicted to be spliced but there is no evidence that it is spliced in vivo

    # See the README.txt for this script at the link below for more information:
    # https://github.com/fomightez/yeastmine

    ## IMPETUS FOR THIS SCRIPT:
    ## Kawashima et al. 2014 [http://www.ncbi.nlm.nih.gov/pubmed/24722551] HAD
    ## GOOD-SIZED GENE LISTS WITH SYSTEMATIC NAMES AS PART OF SOME TABLES AND I
    # WANTED THE LIST IN A FORM THAT IS MORE INFORMATIVE AND HUMAN-READABLE.
    ##
    ## LATER ADDED THE CONCEPT OF BEING ABLE TO ADD FAVORITE GENES.
    ## CURRENTLY FAVORITE GENES USE THE SGD 'STANDARD NAME' BECAUSE THAT IS
    ## HOW I USUALLY TRACK THEM BUT YOU CAN CHANGE THAT BE PUTTING THEM IN THE
    ## FORM YOU'D LIKE AND ADJUSTING THE CONDITIONAL THAT CHECKS THEM AGAINST THE
    ## SGD GENE LIST.


    list_to_get_info_for = ["YPR063C", "YPR098C", "YPR132W", "YPR170W-B", "YPR187W", "YPR202W"]

    #OPTIONAL - SEE BELOW
    #my_favorite_genes = ["NMD2", "MUD1", "TAN1"]

    # The following two lines will be needed in every python script:
    import intermine
    from intermine.webservice import Service
    service = Service("http://yeastmine.yeastgenome.org/yeastmine/service")

    # Get a new query on the class (table) you will be querying:
    query = service.new_query("Gene")

    # The view specifies the output columns
    query.add_view(
        "primaryIdentifier", "secondaryIdentifier", "symbol", "name",
        "organism.shortName", "proteins.symbol",  "sgdAlias", "featureType", "description"
    )

    # This query's custom sort order is specified below:
    query.add_sort_order("Gene.secondaryIdentifier", "ASC")


    print "primaryIdentifier\tsecondaryIdentifier\tsymbol\tname\torganism.shortName\tproteins.symbol\tsgdAlias\tfeatureType\tdescription"


    for row in query.rows():
        if row["secondaryIdentifier"] in list_to_get_info_for:
        #LIST OF FAVORITE GENES AND ADD AN 'AND' CONDITION TO ABOVE LINE TO LIMIT TO YOUR FAVORITE GENES, like so:
        #if (row["secondaryIdentifier"] in list_to_get_info_for) & (row["symbol"] in my_favorite_genes):
            print row["primaryIdentifier"], row["secondaryIdentifier"], row["symbol"], row["name"], \
                row["organism.shortName"], row["proteins.symbol"], row["sgdAlias"], row["featureType"], \
                 row["description"]

NCBI
----

Using the `NCBI Entrez
server <http://www.ncbi.nlm.nih.gov/books/NBK25501/>`__ via Biopython

See the `Real World example
#1 <http://jan2015feng-gr-m.readthedocs.org/en/latest/real%20world%201/#example-1>`__
for a reminder of how to take the script below and run it on
Sourcelair.com. The process is the same.

Unless you have previously installed the Biopython package in your
current SourceLair project, you'll get an error if you try to run the
script below. (If you already did the examples under the Real World
exercises set #1 then you should be all set unless you startd over with
a new project folder since then.)

If you try to run the script and see the error below, you need to
install the module again.

::

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

Now we should be set to run the script below to use the `NCBI Entrez
server <http://www.ncbi.nlm.nih.gov/books/NBK25501/>`__ via Biopython.

::

    from Bio import Entrez
    Entrez.email = "YOUR_EMAIL_GOES HERE" #so NCBI can contact you if you abuse system

    protein_accn_numbers = ["ABR17211.1", "XP_002864745.1", "AAT45004.1", "XP_003642916.1" ]
    protein_gi_numbers = []

    print "The Accession numbers for protein sequence provided:"
    print protein_accn_numbers

    #ESearch
    print "\nBeginning the ESearch..."
    # BE CAREFUL TO NOT ABUSE THE NCBI SYSTEM.
    # see http://biopython.org/DIST/docs/tutorial/Tutorial.html#sec119 for information.
    # For example, if searching with more than 100 records, you'd need to do this ESearch step
    # on weekends or outside USA peak times.
    for accn in protein_accn_numbers:
        esearch_handle = Entrez.esearch(db="protein", term=accn)
        esearch_result= Entrez.read(esearch_handle)
        esearch_handle.close()
        #print esearch_result
        #print esearch_result["IdList"][0]
        protein_gi_numbers.append(esearch_result["IdList"][0])
    #print protein_gi_numbers

    retrieved_mRNA_uids = []
    #ELink
    print "Beginning the ELink step..."
    handle = Entrez.elink(dbfrom="protein", db="nuccore", LinkName="protein_nuccore_mrna", id=protein_gi_numbers)
    result = Entrez.read(handle)
    handle.close()
    #print result
    for each_record in result:
        mrna_id = each_record["LinkSetDb"][0]["Link"][0]["Id"]
        retrieved_mRNA_uids.append(mrna_id)
    #print retrieved_mRNA_uids

    #EPost
    print "Beginning the EPost step..."
    epost_handle = Entrez.epost(db="nuccore", id=",".join(retrieved_mRNA_uids))
    epost_result = Entrez.read(epost_handle)
    epost_handle.close()

    webenv = epost_result["WebEnv"]
    query_key = epost_result["QueryKey"]

    #EFetch
    print "Beginning the EFetch step..."
    count = len(retrieved_mRNA_uids)
    batch_size = 20
    the_records = ""
    for start in range(0, count, batch_size):
        end = min(count, start + batch_size)
        print("Fetching records %i thru %i..." % (start + 1, end))
        fetch_handle = Entrez.efetch(db="nuccore",
                                     rettype="fasta", retmode="text",
                                     retstart=start, retmax=batch_size,
                                     webenv=webenv,
                                     query_key=query_key)
        data = fetch_handle.read()
        fetch_handle.close()
        the_records = the_records + data
    print the_records
