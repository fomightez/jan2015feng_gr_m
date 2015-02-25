.. contents::
   :depth: 3.0
..

Epilogue to Session I
---------------------

In response to questions raised during Session I. I look forward to
another!

Comments and docstrings and placeholders
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Comments
^^^^^^^^

Python will disregard everything on a line after an ``#`` that is not
within a string. You can comment out entire lines by beginning them with
``#``.

Example:

::

    sequence = 'GAATTC' #EcoRI site
    # I like enzymes
    print sequence

If you need to comment out blocks of code, you can take advantage of
your text editor to add ``#`` to multiple lines at once. In Sublime Text
you highlight the text block with the cursor and then use the ``Edit``
menu to naviagte to ``Toggle Block Comment``, i.e., ``Edit``
menu\ ``>``\ Comment\ ``>``\ Toggle Block Comment\`.

Alternatively you can use a docstring.

Docstrings
^^^^^^^^^^

Typically docstrings are used below the first line of a a function,
function ``def`` line to explain the function of the function. Example:

::

    def function_name(variable_passed_in):
        """
        Calculate or do something

        Args:
            variable_passed_in: a variable represention something
        Returns:
            description of output
        Raises:
            TypeError: if variable_passed_in is not a number.
            ValueError: if variable_passed_in is negative.

        """
        pass

code example adapted from
http://stackoverflow.com/questions/3898572/what-is-the-standard-python-docstring-format

Docstrings used elsewhere can be used for large comment blocks as well.

Docstrings can also be assigned as strings. Typically that approach is
used when you want to print to stdout a a lot of text. Such as a guide
to usage of your program in repsonse to certain input fromt the user.

Pass as a placholder
^^^^^^^^^^^^^^^^^^^^

Note that in the function example adove, ``pass`` is used a placeholder
for code to be fleshed out later.

``pass`` can be useful for building the skeleton of your script as
certain text editors and Interactive Development Environments (IDE) will
not allow you to leave lines following a colon blank.

Installed modules/packages/libraries
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Get installed modules/package command library command

``help('modules')``

works on sourcelair.com at the Python prompt. Interestingly, it doesn't
work on my Mac at the Python prompt (in Terminal) where I have Enthought
Canopy installed as my version of Python. Enthought has a package
manager and so they are listed under that if you open Entought's Canopy
gui analysis environment.

adapted from from
http://stackoverflow.com/questions/739993/how-can-i-get-a-list-of-locally-installed-python-modules

Current scope and visualizing your coding steps
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In Python interactive mode that comes up when you type ``Python``:

::

    - dir() will give you the list of in scope variables
    - vars() gives you a dictionary of variables
    - globals() will give you a dictionary of global variables
    - locals() will give you a dictionary of local variables
    - vars()

In IPython Notebook: type ``whos``

adapted from
http://stackoverflow.com/questions/633127/viewing-all-defined-variables

(For more on scope and Python's namespaces, see `A beginner's guide to
Python's namespaces, scope
resolution... <http://nbviewer.ipython.org/github/rasbt/python_reference/blob/master/tutorials/scope_resolution_legb_rule.ipynb>`__)

Examining the current scope can be part of the more general process of
debugging your script, and so I'll touch on that too.

The `Online Python Tutor <http://pythontutor.com/>`__ or `Codeskulptor's
visualization mode (Viz
mode) <http://www.codeskulptor.org/viz/index.html>`__ will show values
as you step through each line of your script.

For debugging real scripts in the typical Python environment, you can:

::

    - add printing variables and messages. You can comment these out. You can even use a the `logging` module to control statements you can turn off at a document level. See lines 70-72 and line 115 of  https://github.com/fomightez/sequencework/blob/master/ConvertSeq/ConvertFASTAdnaSEQtoRNA.py for an example if it in action. See https://docs.python.org/2/howto/logging.html for information about the `logging` module in general.

    - use a debugger module (see https://docs.python.org/2/library/pdb.html and  http://hplgit.github.io/bioinf-py/doc/pub/html/main_bioinf.html for some guidance in this)

    - Enthought Canopy has a nice debugging implementation. You can see a video [here](https://www.enthought.com/products/canopy/canopy-python-debugger/) to get an idea of the features and how one uses these types of approaches to debug in general.
