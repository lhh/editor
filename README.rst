🖋 editor - open a text editor from inside Python 🖋
------------------------------------------------------------------

``editor`` opens a text editor for an existing file, a new file, or a tempfile,
blocks while the user edits text, then returns the results.

You can specify a command line that runs the editor, but usually you leave it
empty - in that case, ``editor`` gets the command line from the environment
variable ``VISUAL``, or if that's empty, the environment variable ``EDITOR``, or if
*that's* empty, either ``Notepad`` on Windows or ``vi`` elsewhere.

EXAMPLE
========

Using a temporary file
~~~~~~~~~~~~~~~~~~~~~~~~~

If no filename is provided, a temporary file gets edited, and its contents
returned.

.. code-block:: python

    import editor

    MESSAGE = 'Insert comments below this line\n\n'
    comments = editor(text=MESSAGE)
    # Pops up the default editor with a tempfile, containing MESSAGE

EXAMPLE
=========

Using a named file
~~~~~~~~~~~~~~~~~~~~

If a filename is provided, then it gets edited!

.. code-block:: python

    import os

    FILE = 'file.txt'
    assert not os.path.exists(FILE)

    comments = editor(text=MESSAGE, filename=FILE)
    # Pops up an editor for new FILE containing MESSAGE, user edits

    assert os.path.exists(FILE)

    # You can edit an existing file too, and select your own editor.
    comments2 = editor(filename=FILE, editor='emacs')

API
===

``editor(text=None, filename=None, editor=None, **kwargs)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

(`editor.py, 69-110 <https://github.com/rec/editor/blob/master/editor.py#L69-L110>`_)

Open a text editor, block while the user edits, then return the results

ARGUMENTS
  text
    A string which is written to the file before the editor is opened.
    If ``None``, the file is left unchanged.

  filename
    The name of the file to edit.  If ``None``, a temporary file is used.

  editor
    A string containing the command used to invoke the text editor.
    If ``None``, use ``editor.default_editor()``.

  kwargs
    Arguments passed on to ``runs.call()``, an enhanced ``subprocess.call()``

``editor.default_editor()``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

(`editor.py, 112-124 <https://github.com/rec/editor/blob/master/editor.py#L112-L124>`_)

Return the default text editor.

The default text editor is the contents of the environment variable
``EDITOR``, it it's non-empty, otherwise if the platform is Windows, it's
``'notepad'``, otherwise ``'vim'``.

(automatically generated by `doks <https://github.com/rec/doks/>`_ on 2020-11-18T18:14:07.417688)
