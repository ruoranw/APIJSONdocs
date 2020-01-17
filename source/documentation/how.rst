How does APIJSON works?
=======================

APIJSON-Server will turn JSON formatted requests to SQL statements. Then as the database has been connected, those SQL statements will be executed. The server will return specified resources in JSON. During the whole process, APIJSON automatically verify the user's role and permissions, which will prevent malicious SQL injection.

You can also set restrictions on the request content by set rules in the database beforehand. For instance, to verify if the value of :code:`type{}` would be one of :code:`[0,1,2]`, you just need to add the following in the database:

.. code-block:: json

  "VERIFY":{
    "type{}":[0,1,2]
  }

Others that are used to verify requests include:

.. code-block:: json

  "VERIFY": { "money&{}":">0,<=10000" }              //To verify if the value if money is between 0 and 10000.
  "TYPE": { "balance": "Double" }                    //To verify if the data type of the "balance" is "Double".
  "UNIQUE": "phone"                                  //The value of "phone" must be unique.
  "NECESSARY": "id,name"                             //"id" and "name" must be included in the request body.
  "DISALLOW": "balance"                              //"Balance" is not allowed to be included in the request body.
  "INSERT": { "@role": "OWNER" }                     //If the "role" is not included in the request, the system will assign one by default.
  "UPDATE": { "id@": "User/id" }                     //To force to insert a key-value pair.


To see a full list of key words that used to set constraints on requests or verify requests, `click here <https://github.com/APIJSON/APIJSON/blob/master/APIJSON-Java-Server/APIJSONORM/src/main/java/zuo/biao/apijson/server/Operation.java>`_.


