/api/tree
=========

Trees are meta data used to organize time series in a heirarchical structure for browsing similar to a typical file system. The tree endpoing enables creating, modifying or deleting trees, rules and fetching generated branches.

Tree API Endpoints
------------------

.. toctree::
   :maxdepth: 1
   
   branch
   collisions
   notmatched
   rule
   rules
   
Verbs
-----

* GET - Retrieve one or more tree definitions
* POST - Edit tree fields
* PUT - Replace tree feidls
* DELETE - Delete a tree and all associated meta data

Requests
--------

The following fields can be used for all tree endpoint requests:

.. csv-table::
   :header: "Name", "Data Type", "Required", "Description", "Default", "QS", "RW", "Example"
   :widths: 10, 5, 5, 45, 10, 5, 5, 15
   
   "tree", "Integer", "Required*", "Used to fetch or modify a specific tree. *When creating a new tree, the ''tree' value must not be present.", "", "tree", "RO", "1"
   "name", "String", "Required*", "A brief, descriptive name for the tree. *Required only when creating a tree.", "", "name", "RW", "Network Infrastructure"
   "description", "String", "Optional", "A longer description of what the tree contains", "", "description", "RW", "Tree containing all network gearl"
   "notes", "String", "Optional", "Detailed notes about the tree", "", "notes", "RW", ""
   "strictMatch", "Boolean", "Optional", "Whether or not timeseries should be included in the tree if they fail to match one or more rule levels.", "false", "strict_match", "true"
   
Response
--------

A successful response to a ``GET``, ``POST`` or ``PUT`` request will return tree objects with optinally requested changes. Successful ``DELETE`` calls will return with a ``204`` status code and no body content. When modifying data, if no changes were present, i.e. the call did not provide any data to store, the resposne will be a ``304`` without any body content. If the requested tree did not exist in the system, a ``404`` will be returned with an error message. If invalid data was supplied an ''400'' error will be returned.

All **Request** fields will be present in the response in addition to others:

.. csv-table::
   :header: "Name", "Data Type", "Description", "Example"
   :widths: 10, 10, 60, 20
   
   "rules", "Map", "A map or dictionary with rules defined for the tree organized by ''level'' and ''order''. If no rules have been defined yet, the value will be ''null''", "*See Examples*"
   "created", "Integer", "A Unix Epoch timestamp in seconds when the tree was originally created.", "1350425579"

GET
---

A ''GET'' request to ''/api/tree'' without a tree ID will return a list of all of the trees configured in the system. The results will include configured rules for each tree. If no trees have been configured yet, the list will be empty. 

Example GET All Trees Query
^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

  http://localhost:4242/api/tree
  
Example Response
^^^^^^^^^^^^^^^^



To fetch a specific tree, supply a ''tree' value. The response will include the tree object if found. If the requested tree does not exist, a 404 exception will be returned.

Example GET Single Tree
^^^^^^^^^^^^^^^^^^^^^^^
:;

  http://localhost:4242/api/tree?tree=1
  
Example Response
^^^^^^^^^^^^^^^^


POST/PUT
--------

Using the ''POST'' or ''PUT'' methods, you can create a new tree or edit most of the fields for an existing tree. New trees require a ''name'' value and for the ''tree' value to be empty. Existing trees require a valid ''tree'' ID and any fields that require modification. A successful request will return the modified tree object.

Example POST Create Request
^^^^^^^^^^^^^^^^^^^^^^^^^^^
::
  
  http://localhost:4242/api/tree?name=Network%20Tree&method=post


Example Response
^^^^^^^^^^^^^^^^


Example POST Edit Request
^^^^^^^^^^^^^^^^^^^^^^^^^
::

  http://localhost:4242/api/tree?tree=1&description=Network%20Device%20Information&method=post
  
Example Response
^^^^^^^^^^^^^^^^


DELETE
------

Using the ''DELETE'' method will remove a tree, rules, collisions, not matched entries and all branches from storage. This endpoint starts a delete. Because the delete can take some time, the endpoint will return a successful 204 response without data if the delete was able to start. If the tree was not found, it will return a 404.

.. WARNING:: This method cannot be undone. Once executed, the purge will continue running unless the TSD is shutdown.

.. NOTE:: Before executing a ''DELETE'' query, you should make sure that a manual tree syncronization is not running somehwere on your data. If it is, there may be some orphaned branches or leaves stored during the purge. Use the _____ CLi tool sometime after the delete to cleanup left over branches or leaves.

Example DELETE Request
^^^^^^^^^^^^^^^^^^^^^^
::

  http://localhost:4242/api/tree?tree=1&method=delete
  
Example Response
^^^^^^^^^^^^^^^^

