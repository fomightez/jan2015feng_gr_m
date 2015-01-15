Real World Examples II: Using APIs
==================================

Plotly
------

`Plotly`_

This will be a non-interactive demo of a script running on `Domino Data
Lab`_.

1. Look at date and stats of plot `here`_

2. Script will be run.

3. Look at date and stats of plot `here`_

Yeastmine
---------

`YeastMine`_ has a `Python web service API`_

Demo of where to get Python code fragments for designed queries

Example integrating that into your work
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Plan:

Use Yeastmine to convert information into a table into more useful form.

Initial steps will be non-interactive in the interest of time.

Those steps will produce

::

    table_4_gene_list = ["YBL091C-A", "YBL059W", "YBR090C", "YBR186W", "YBR219C", "YBR230C", "YCL005W-A_1", "YCL005W-A_2", "YCR028C-A", "YCR097W_2", "YDL219W", "YDL189W", "YDL137W", "YDL125C", "YDL082W", "YDL079C", "YDL064W", "YDR059C", "YDR099W", "YDR305C", "YDR318W", "YDR367W", "YDR381W", "YDR381C-A", "YDR535C", "YER003C", "YER007C-A", "YER014C-A", "YER044C-A", "YER131W", "YER179W", "YFL039C", "YFL034C-B", "YFL031W", "YFR045W", "YGL251C", "YGL187C", "YGL183C", "YGL033W", "YGR029W", "YGR183C", "YGR225W", "YHR012W", "YHR039C-A", "YHR041C", "YHR079C-A", "YHR123W", "YHR141C", "YHR218W", "YIL148W", "YIL111W", "YIL073C", "YIL004C", "YJL189W", "YJL041W", "YJL031C", "YJL024C", "YJR079W", "YJR094W-A", "YJR112W-A", "YKL006C-A", "YKR005C", "YLL050C", "YLR054C", "YLR078C", "YLR128W", "YLR199C", "YLR202C", "YLR211C", "YLR275W", "YLR333C", "YLR445W", "YML085C", "YML067C", "YML036W", "YML025C", "YML024W", "YML017W", "YMR194C-B", "YMR242C", "YMR292W", "YNL312W", "YNL138W-A", "YNL130C", "YNL066W", "YNL050C", "YNL044W", "YNR053C", "YOL047C", "snR17A", "YOR318C", "YPL241C", "YPL230W", "snR17B", "YPR010C-A", "YPR153W"]

Now replace the example list in the code below and run the code of
``finding_genes_in_list_with_SGD_Systematic_Name.py`` found below.

\`\`\` #!/usr/bin/env python

USAGE: TAKES A LIST OF GENES PROVIDED IN THE LONG SGD SYSTEMATIC NAME FORM
--------------------------------------------------------------------------

AND COLLECTS MORE USER FRIENDLY VERSION OF NAME AND INFORMATION FOR EACH GENE.
------------------------------------------------------------------------------

Example input:
--------------

[“YPR187W”, “YPR202W”]
----------------------

Example output:
---------------

S000006391 YPR187W RPO26 RNA POlymerase S. cerevisiae Rpo26p RPB6 ABC23 ORF RNA polymerase subunit ABC23; common to RNA polymerases I, II, and III; part of central core; similar to bacterial omega subunit
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

S000006406 YPR202W None None S. cerevisiae None None ORF Putative protein of unknown function; similar to telomere-encoded helicases; down-regulated at low calcium levels; YP
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

.. _Plotly: https://plot.ly/~wayne461/42/file-size-distribution-of-all-105222-protein-data-bank-entries-as-of-jan-7-2015/
.. _Domino Data Lab: http://www.dominodatalab.com/
.. _here: https://plot.ly/~wayne461/42/file-size-distribution-of-all-105222-protein-data-bank-entries-as-of-jan-7-2015/
.. _YeastMine: http://yeastmine.yeastgenome.org/yeastmine/begin.do
.. _Python web service API: http://yeastmine.yeastgenome.org/yeastmine/api.do?subtab=python
