What APIJSON has achieved?
==========================

Functions
----------

•Registeration and login

•CRUD and remote procedure call(RPC) of functions

•Setting orders and pages on returned data

•Calculating and grouping data

•Fuzzy matching search

•Regular expressions

•Joining tables, subquery, and other SQL functions

---------------------

Request Methods
-----------------

The APIJSON supports the following request methods:

**GET,HEAD,GETS,HEADS,POST,PUT,DELETE**

For details of these requests methods, see `design rules <https://apijsondocs.readthedocs.io/en/latest/documentation/design_rules.html#methods-and-http-mapping>`_.

---------------------

Request body structures
-----------------------

{ "Table":{...} }

{ "Table0":{...}, "Table1":{...}, "Table2":{...} ... }

{ "[]":{ "Table":{...} } }

{ "[]":{ "Table0":{...}, "Table1":{...}, "Array0[]":{...}, ... } }
.
.
.
etc.

---------------------

Response body
--------------

The reponse body structure will be the same as request body structure.

---------------------

Build-in functions
-------------------

.. code-block:: json

    "key[]":{}                                       // retrieve data arrays.

    "key{}":[1,2,3]                                  // Add constraints on returned data.

    "key{}":"<=10;length(key)>1..."                  // Add constraints on returned data.

    "key()":"function(arg0,arg1...)"                 // RPC of functions.

    "key@":"key0/key1.../targetKey"                  // Refer a value.

    "key$":"%abc%"                                   // Fuzzy machting research.

    "key~":"^[0-9]+$"                                // Include regular expressions.

    "key%":"2018-01-01,2018-10-01"                   // Add constraints on returned data.

    "key+":[1]                                         // Add/Expand data.

    "key-":888.88                                      // Reduce/Delete data.

    "name:alias"                                       // Make an alias.

    "@combine":"name~,tag~"                            // Set more than two conditions.

    "@column":"id,sex,name"                            // Set returned value.

    "@group":"userId"                                  // Group data.

    "@having":"max(id)>=100"                           // Add aggregate functions.

    "@order":"date-,name+"                             // Set orders.

    "@schema":"sys"                                    //

    "@database":"POSTGRESQL"                           // Interact with different databases.

    "@explain":true                                    // Performance analysis.

    "@role":"LOGIN"                                    // Set the visiting role.

