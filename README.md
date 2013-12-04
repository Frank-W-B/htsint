High-Throughput Sequencing Integrate - htsint
===============================================

A Python library (under initial development) to integrate
high-throughput sequencing data using probabilistic graphical models.

INSTALLATION
============

Prerequisites (Ubuntu/Debian)
--------------

General:

  * ncbi-blast+
  * python package - numpy
  * python package - matplotlib 
  * python package - networkx
  * python package - pymc 
  * python package - biopython

Database specific:

  * postgresql (or another relational db)
  * database driver i.e. psycopg2 
  * python package - sqlalchemy


ABOUT
=====

Database
-----------
The non-sequencing data is stored in a database:

  * Taxa
  * Gene names, synonyms
  * Gene accessions
  * Gene Ontology terms and annotations

The data is managed and accessed using SQLAlchemy

  http://www.sqlalchemy.org

BLAST and other sequence analyses 
-----------------------------------

This is a collection of functions to carry out the general analysis of
high-thoughput sequencing data.  These functions make heavy use of
Biopython:

  http://biopython.org/wiki/Main_Page

Statistical Models
----------------------

The statistical models extensively use the PyMC sampling toolkit.

  https://pypi.python.org/pypi/pymc

SETUP 
=====

In order for the unit tests to pass the database must be running and 
the BLAST files downloaded.

Database
---------

for more info see /src/database/HOWTO

  1. Create an empty Postgresql database
  2. ~$ cd /src/database
  3. Tell htsint your database params
    * ~$ cp config.py.dist config.py
    * Then edit the file with the appropriate info
    * the field 'dbhost' may be 'localhost' or a remote one
    * edit the taxa field depending on user needs
      more taxa can be added later
  4. ~$ python FetchNcbiData.py
  5. ~$ python FetchGo.py
  6. ~$ python CreateDatabase.py
  7. ~$ python TestDatabase.py

 
BLAST
------

  1. ~$ cd /src/blast
  2. ~$ python FetchBlastDBs.py  
  3. ~$ makeblastdb -in uniprot_trembl.fasta -dbtype prot -out uniprot_trembl
  4. ~$ makeblastdb -in nr.db -dbtype prot -out nr
  5. ~$ makeblastdb -in swissprot.db -dbtype prot -out swissprot

These are examples of local databases.  Download and convert any database that fits you user needs.