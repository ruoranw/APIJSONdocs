How does APIJSON works?
=======================

APIJSON-Server will turn JSON formatted requests to SQL statements. Then as the database has been connected, those SQL statements will be executed. The server will return specified resources in JSON. During the whole process, APIJSON automatically verify the user's role and authorization, which will prevent malicious SQL injection.

Besides, developers can verify the request body by adding code in database. For instance, to verify if the value of :code:`type{}` would be one of :code:`[0,1,2]`, you just need to add the following in the database:

.. code-block:: json

  "VERIFY":{
    "type{}":[0,1,2]
  }

Others that are used to verify requests include:

.. code-block:: json

  "VERIFY": { "money&{}":">0,<=10000" }              //Verify if money>0 & money<=10000.
  "TYPE": { "balance": "Double" }                    //Verify if the "TYPE" of the "balance" is "Double".
  "UNIQUE": "phone"                                  //The value of "phone" shouldn't be the same as any one already in the database.
  "NECESSARY": "id,name"                             //"id" and "name" are requested.
  "DISALLOW": "balance"                              //"Balance" is not allowed to be included in the request body.
  "INSERT": { "@role": "OWNER" }                     //If "role" is not included, then the default value will be add to the database.
  "UPDATE": { "id@": "User/id" }                     //Force to add key-value pairs.

To see a full list of key words that used to set constraints on requests or verify requests, `click here <https://github.com/APIJSON/APIJSON/blob/master/APIJSON-Java-Server/APIJSONORM/src/main/java/zuo/biao/apijson/server/Operation.java>`_.


