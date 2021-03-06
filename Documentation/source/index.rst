.. CorGAT documentation master file, created by
   sphinx-quickstart on Mon Jul 20 20:13:11 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to CorGAT's documentation!
==================================

`CorGAT <https://github.com/matteo14c/CorGAT>`_ is a collection of Perl utilities that can be used to align complete assemblies of SARS-CoV-2 genomes wih the reference genomic sequence, to obtain a list of polymorphic positions and to **annotate** genetic variants according to the method described in *Chiara et al 2020*  to be published soon (hopefully). The manuscript is currently submitted and undergoing peer review.

This software package is composed of 2 very simple scripts and a collection of files with functional annotation data. Since the number of available SARS-CoV-2 genomic sequences is increasingly constantly, these files are regularly updated on a monthly basis. If you do not feel comfortable in installing/running CorGAT from the command line, you can find a Galaxy running the software at http://corgat.ba.infn.it/galaxy , or download a dockerized version of the Galaxy, with all the tools `here <https://hub.docker.com/r/laniakeacloud/galaxy_corgat>`_.

.. figure:: _static/img/galaxy_corgat.png
   :scale: 50%
   :align: center

If you find any of this software useful for your work, please cite:

**Chiara M, Horner DS, Gissi C, Pesole G. Comparative genomics provides an operational classification system and reveals early emergence and biased spatio-temporal distribution of SARS-CoV-2 bioRxiv 2020.06.26.172924; doi: https://doi.org/10.1101/2020.06.26.172924**

and

**Chiara M, Zambelli F, Tangaro MA, Mandreoli P, Horner DS, Pesole G. CorGAT: a tool for the functional annotation of SARS-CoV-2 genomes. Under Peer review**

If you find any issue with the software, please contact `me <mailto:matteo.chiara@unimi.it>`_, or report it  on `github <https://github.com/matteo14c/CorGAT/issues>`_.

.. toctree::
   :maxdepth: 2
   :caption: Command line version

   prerequisites.rst
   align_to_refdata.rst
   func_annotation.rst
   quickstart.rst

.. toctree::
   :maxdepth: 2
   :caption: Galaxy version

   galaxy_import_data.rst
   galaxy_analyse_data.rst
 
.. toctree::
   :maxdepth: 2
   :caption: Docker version

   install_docker.rst


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
