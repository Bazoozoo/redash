Supported Data Sources
######################

re:dash supports several types of data sources, and if you set it up using the provided images, it should already have
the needed dependencies to use them all. Starting from version 0.7 and newer, you can manage data sources from the UI
by browsing to ``/data_sources`` on your instance.

If one of the listed data source types isn't available when trying to create a new data source, make sure that:

1. You installed required dependencies.
2. If you've set custom value for the ``REDASH_ENABLED_QUERY_RUNNERS`` setting, it's included in the list.

PostgreSQL / Redshift
---------------------

-  **Options**:

   -  Database name (mandatory)
   -  User
   -  Password
   -  Host
   -  Port

-  **Additional requirements**:

   - None


MySQL
-----

-  **Options**:

   -  Database name (mandatory)
   -  User
   -  Password
   -  Host
   -  Port

-  **Additional requirements**:

   - ``MySQL-python`` python package


Google BigQuery
---------------

-  **Options**:

   -  Project ID (mandatory)
   -  JSON key file, generated when creating a service account (see `instructions <https://developers.google.com/console/help/new/#serviceaccounts>`__).


-  **Additional requirements**:

   - ``google-api-python-client``, ``oauth2client`` and ``pyopenssl`` python packages (on Ubuntu it might require installing ``libffi-dev`` and ``libssl-dev`` as well).


Graphite
--------

-  **Options**:

   -  Url (mandatory)
   -  User
   -  Password
   -  Verify SSL certificate


MongoDB
-------

-  **Options**:

   -  Connection String (mandatory)
   -  Database name
   -  Replica set name

-  **Additional requirements**:

   - ``pymongo`` python package.

For information on how to write MongoDB queries, see :doc:`documentation </usage/mongodb_querying>`.


ElasticSearch
-------------

...

InfluxDB
--------

...

Presto
------

...

Hive
----

...

Impala
------

...

URL
---

A URL based data source which requests URLs that return the :doc:`results JSON
format </dev/results_format>`.

Very useful in situations where you want to expose the data without
connecting directly to the database.

The query itself inside re:dash will simply contain the URL to be
executed (i.e. http://myserver/path/myquery)

-  **Options**:

   -  Url - set this if you want to limit queries to certain base path.


Google Spreadsheets
-------------------

-  **Options**:

   -  JSON key file, generated when creating a service account (see `instructions <https://developers.google.com/console/help/new/#serviceaccounts>`__).

-  **Additional requirements**:

   -  ``gspread`` and ``oauth2client`` python packages.

Notes:

1. To be able to load the spreadsheet in re:dash - share your it with
   your ServiceAccount's email (it can be found in the credentials json
   file, for example
   43242343247-fjdfakljr3r2@developer.gserviceaccount.com).
2. The query format is "DOC\_UUID\|SHEET\_NUM" (for example
   "kjsdfhkjh4rsEFSDFEWR232jkddsfh\|0")


Python
------

**Execute other queries, manipulate and compute with Python code**

This is a special query runner, that will execute provided Python code as the query. Useful for various scenarios such as
merging data from different data sources, doing data transformation/manipulation that isn't trivial with SQL, merging
with remote data or using data analysis libraries such as Pandas (see `example query <https://gist.github.com/arikfr/be7c2888520c44cf4f0f>`__).

While the Python query runner uses a sandbox (RestrictedPython), it's not 100% secure and the security depends on the
modules you allow to import. We recommend enabling the Python query runner only in a trusted environment (meaning: behind
VPN and with users you trust).

-  **Options**:

   -  Allowed Modules in a comma separated list (optional). **NOTE:**
      You MUST make sure these modules are installed on the machine
      running the Celery workers.
