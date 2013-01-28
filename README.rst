Django tsearch2
===============

Djang tsearch implements an abstract model Class that allows models to be full text searchable using postgresql's tsearch2 functionality.

Installation
------------

First you'll need a Postgres 9.1 database server that has plpython
installed then you can install django-tsearch2 with pip.

  $ pip install https://github.com/akimboio/django-tsearch2

Usage
-----

To use the djangotsearch in a project simply inherit from
SearchableModel and override the model manager.


Example Model
^^^^^^^^^^^^^

.. code:: python
class model(SearchableModel):
    name = models.CharField(max_length=255)
    description = models.TextField()
    objects = SearchManager(
        {
           'name': 'A',
           'description': 'C"
            }
        )

NOTE: the letters A-D are used to denote the sorting rank for fields
that are being searched.
	     

Bugs
^^^^

South does not yet recognize the VectorField datatype.  

When changing an existing model to be a SearchableModel, you must
add a column named search_index, of type tsvector to the table:

alter table <table name> add search_index tsvector;
