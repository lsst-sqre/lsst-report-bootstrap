#######################
lsst-technote-bootstrap
#######################

Write technotes that are native to the web
==========================================

``lsst-technote-bootstrap`` is a template for LSST technical notes that are written in `reStructuredText`_, generated with `Sphinx`_, and deployed to the web with `LSST the Docs`_.

For background on the DM technote platform, see `SQR-000`_.

Quick Start
===========

1. Install cookiecutter
-----------------------

We use `cookiecutter`_ to help you create a new technote.
Install cookiecutter via:

.. code-block:: bash

   pip install cookiecutter

2. Create a technote
--------------------

Start a new technote project in a convenient directory.
Run this command (verbatim):

.. code-block:: bash

   cookiecutter https://github.com/lsst-sqre/lsst-technote-bootstrap.git

(Alternatively you can ``git clone`` this repository and run cookiecutter directly on it: ``cookiecutter lsst-technote-bootstrap``).

.. note::

   If you're running cookiecutter_ with Python 3, you *might* get a ``RuntimeError``:

      RuntimeError: Click will abort further execution because Python 3 was configured to use ASCII as encoding for the environment.  Either run this under Python 2 or consult http://click.pocoo.org/python3/ for mitigation steps.

   See `Cookiecutter and Python 3 <#cookiecutter-and-python-3>`_ for a solution.

Answer the prompts, and you'll have a brand new technote project.
`The prompts are documented below <#configuration-prompts>`_.

``cd`` into the technote's directory and initialize git:

.. code-block:: bash

   cd {{repo_name}}
   git init .
   git add --all
   git commit -m "Init technote"

3. Customize the technote's Metadata and README
------------------------------------------------

We maintain technote metadata (such as authors, title, etc.) in the ``metadata.yaml`` file contained in the technote's repository.

Edit the metadata to correct any errors made in the cookiecutter prompts, or to add additional authors.

You can also edit the ``README.rst`` to give additional cues to readers/authors viewing the technote on GitHub.

4. Push to GitHub
-----------------

The technote should be published to a new GitHub repo as early as possible, even before you've added content.
Having the repo on GitHub effectively reserves your technote's serial number.

Which organization you place the technote in depends on the document's series:

- SQuaRE technical notes (SQR series) go in https://github.com/lsst-sqre.
- DM technical notes (DMTN series) go in https://github.com/lsst-dm.
- Simulations Group technical notes (SMTN series) go in https://github.com/lsst-sims.
- Official, change-controlled documents (LDM, LSE, etc.) go in the main https://github.com/lsst organization.

Ensure that the ``github_namespace`` you provided at the ``cookiecutter`` prompt matches the technote's name and organization on GitHub.

When you're creating the GitHub repository, make an empty project; you've already created the README, LICENSE and gitignore files locally.

The repo's GitHub summary line should correspond to the technote's title and the homepage should be the URL of the published technote.

5. Write the Docs
-----------------

Write the technote in the ``index.rst`` file.
The markup language of DM is `reStructuredText`_.
We've written a page on writing reStructuredText for DM that may help you get started: http://developer.lsst.io/en/latest/docs/rst_styleguide.html

It's best to start writing content on a new branch, usually a `ticket branch <https://developer.lsst.io/processes/workflow.html#git-branching>`_.
This way you can use a pull request to have your content reviewed before it's published at the main URL.

The ``README.rst`` in your technote includes details on how to locally build the technote.

6. Publish with LSST the Docs
-----------------------------

LSST technotes are continuously distributed (published) to the web using Travis CI and LSST the Docs.
To publish to `LSST the Docs`_, let Jonathan Sick (jsick at lsst org) know, and he will

1. Create a `LSST the Docs`_ project, and
2. Create a Travis CI configuration for Sphinx builds

This is a one-time step for each technote.

Now whenever you push new commits to any branch, your versioned technote will be viewable from your technote's subdomain of ``*.lsst.io``.
See `SQR-006 <https://sqr-006.lsst.io/#versioned-documentation-urls>`__ for details on versioned URLs in LSST the Docs.

7. Get a DOI with Zenodo
------------------------

A Digital Object Identifier (DOI) allows your technote to be cited in literature.
Zenodo_ is an archive that provides DOIs.

To connect your technote's GitHub repo to Zenodo_, follow the instructions at https://guides.github.com/activities/citable-code/.

When following the `Creating a new Release`_ section of GitHub's instructions, use semvar (e.g., ``v1.0``) for both the release tag *and* title. 
The release description can be something as simple as 'v1.0 release of SQR-001: Git LFS Architecture Note'.

.. _Creating a New Release: https://guides.github.com/activities/citable-code/#create

When following the `Minting a DOI`_ section of GitHub's instructions, you'll add metadata about the technote.
Here is some guidance on what metadata to add:

.. _Minting a DOI: https://guides.github.com/activities/citable-code/#finishing

- **Types(s) of Files**: 'Publication'.
- **Publication type**: 'Technical note'.
- **Publication date**: Date of publication, or today.
- **Title**: Use the '{{series}}-{{serial} {{tag}} {{title}}' format. E.g. 'SQR-001 v1.0 The LSST DM Technical Note Publishing System'.
- **Authors**: List all authors (matching ``metadata.yaml``) and their affiliations. You may need to manually add authors that aren't in the git history.
- **Description**: A short summary or abstract of the document.
- **Keywords**: Add the 'lsst' keyword. Also add a keyword for the technote series, such as 'lsst-sqr' for 'SQR-NNN' technotes.
- **Additional notes**: Add the text ``View this document online at http://sqr-000.lsst.io`` (replacing your document's URL as appropriate).
- **License**: 'Creative Commons Attribution'
- **Access Rights**: 'Open Access'
- **Communities**: 'Large Synoptic Survey Telescope Data Management'
- **Related/alternate identifiers**: In addition to the GitHub URL provided by default, add the document's published URL and annotate that URL as "is compiled/created by this upload."

Note that the 'Large Synoptic Survey Telescope Data Management' collection (`lsst-dm`_) organizes DM technotes to provide additional visibility.

.. _lsst-dm: https://zenodo.org/collection/user-lsst-dm

Once your metadata is prepared, you can **Submit** the technote and generate a DOI and object page on Zenodo.

In your ``README.rst``, uncomment the markup for the DOI badge (updating it with your technote's DOI), and add the DOI to ``metadata.yaml``.

8. Publishing the tagged document
---------------------------------

When you create a GitHub Release for Zenodo, it's good practice to publish that tag on Read the Docs and have that tag linked from the Zenodo deposition page.

1. Go on Read the Docs and add the tag as a built *version* (if Jonathan Sick created the Read the Docs project for you, let him know and he'll do this for you).
2. On Zenodo, find your uploaded document by clicking on **My Uploads** from your account dropdown.

   a. **Edit** the upload.
   
   b. On the metadata page, add the URL for the tagged version on Read the Docs (e.g., ``http://sqr-000.lsst.io/en/v1.0/``) to the **Related/alternate identifiers** section with a 'is compiled/created by this upload' relationship. The Related/alternate identifiers section will now list both the GitHub repo's URL and the Read the Docs URL.
   
   c. Re-submit the deposition. Only the metadata will be updated; the DOI will remain the same.

Configuration Prompts
=====================

This section describes the content expected by the prompts when running `cookiecutter`_ to create a new technote project.

- ``first_author``: The first author's name, formatted as "First Last". You can edit ``metadata.yaml`` to add additional authors.
- ``series``: The technote series, which can be

  - ``SQR`` for SQuaRE technical notes
  - ``DMTN`` for Data Management technical notes
  - ``SMTN`` for Simulations Group technical notes

- ``serial_number``: the serial number. Use three digits padded with zeros.
- ``title``: Title of the technote.
- ``github_org``: The GitHub organization where this technote resides, which can be

  - ``lsst-dm`` for the DM DMTN series
  - ``lsst-sqre`` for the SQuaRE SQR series
  - ``lsst-sims`` for the Simulations Group's SMTN series

- ``github_namespace``: This is the expected GitHub URL of the technote, minus the 'github.com/' prefix. For example, ``lsst-sqre/sqr-000``.
- ``docushare_url``: The URL of the technote on Docushare, if the canonical version is stored there. If Docushare is not used, leave this field blank.
- ``description``: This should be a short, 1-2 sentence description of the technote. This description is placed just below the title in the README.
- ``copyright_year``: Should be the current year for new projects
- ``copyright_holder``: Should be ``AURA/LSST`` for technotes made by DM employees.

Note that errors when entering `cookiecutter`_ prompts can be easily fixed by editing the ``index.rst``, ``README.rst`` and ``metadata.yaml`` files in the generated technote project.


Cookiecutter and Python 3
=========================

Depending on how your shell is set up, you may get this error when running cookiecutter_ under Python 3:

    RuntimeError: Click will abort further execution because Python 3 was configured to use ASCII as encoding for the environment.  Either run this under Python 2 or consult http://click.pocoo.org/python3/ for mitigation steps.

To solve this, you need to set your shell's *locale* to use UTF-8.
Type these lines into your shell:

.. code-block:: bash

   export LC_ALL=en_US.utf-8
   export LANG=en_US.utf-8

*This will work on macOS. Linux distributions may be different (try C.UTF-8).*

After the locale is set, re-try the cookiecutter_ command.

****

Copyright 2015-2017 Association of Universities for Research in Astronomy, Inc.

`lsst-technote-bootstrap` is open source (MIT license).

.. _SQR-000: https://sqr-000.lsst.io
.. _`LSST the Docs`: https://sqr-006.lsst.io
.. _Zenodo: http://zenodo.org
.. _reStructuredText: http://sphinx-doc.org/rest.html
.. _Sphinx: http://sphinx-doc.org
.. _cookiecutter: http://cookiecutter.rtfd.org/
