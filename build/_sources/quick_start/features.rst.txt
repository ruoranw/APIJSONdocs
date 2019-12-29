
Features
==========

**For API developers:**

* APIJSON largely reduces API developers' workload by reducing most API protocals design work and documentation work.

* APIJSON supports automatic permission verification, version management and SQL injection prevention. The API has no version, so developers no longer need to worry about the update of API protocals or the derivative documentation update.

* With these features, it saves communication time between front-end and back-end developers about the API design.

**For users:**

* You can get many resources and different forms of data by making just a single request While typical REST APIs require loading from multiple URLs. Being convenient and flexible, it saves sending multiple requests with multiple API endpoints.

* It provides CRUD(read and write), Fuzzy Search, Remote Method Invocation (RMI), etc. Other features include saving duplicate data, checking request history, etc.

Examples
---------

APIJSON is organized by json objects not endpoints. The client can access full capabilities of the data from a single endpoint. To send a request, the basic structure is :

**baseURL / Methods(GET,GETS,POST,etc.) / JSONObject query**

The following example shows how to query a user's information.

**Get a user:**

Request

.. code-block:: json

 {
  "User":{
  }
 }

Response

.. code-block:: json

 {
  "User":{
    "id":38710,
    "sex":0,
    "name":"TommyLemon",
    "certified":true,
    "tag":"Android&Java",
    "phone":13000038710,
    "head":"http://static.oschina.net/uploads/user/1218/2437072_100.jpg?t=1461076033000",
    "date":1485948110000,
    "pictureList":[
      "http://static.oschina.net/uploads/user/1218/2437072_100.jpg?t=1461076033000",
      "http://common.cnblogs.com/images/icon_weibo_24.png"
    ]
  },
  "code":200,
  "msg":"success"
 }

`Try it yourself <http://apijson.cn:8080/get/{"User":{}}>`_

The following example shows the query of getting three users' :code:`id` and :code:`name`.

**Get an array of users**

Request

.. code-block:: json

 {
  "[]":{
    "count":3,            
    "User":{
      "@column":"id,name"
    }
  }
 }

Response

.. code-block:: json

 {
  "[]":[
    {
      "User":{
        "id":38710,
        "name":"TommyLemon"
      }
    },
    {
      "User":{
        "id":70793,
        "name":"Strong"
      }
    },
    {
      "User":{
        "id":82001,
        "name":"Android"
      }
    }
  ],
  "code":200,
  "msg":"success"
 }

`Try it yourself <http://apijson.cn:8080/get/{"[]":{"count":3,"User":{"@column":"id,name"}}}>`_


`Test it online <http://apijson.cn/>`_

.. image:: https://raw.githubusercontent.com/TommyLemon/StaticResources/master/APIJSON_Auto_get.jpg

|

.. image:: https://raw.githubusercontent.com/TommyLemon/StaticResources/master/APIJSON_Auto_code.jpg

