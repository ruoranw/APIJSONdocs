
Features
==========

**For API developers:**

* APIJSON largely reduces API developers' workload by reducing most API protocal design work and documentation work.

* APIJSON supports automatic permission verification, version management and SQL injection prevention. Developers no longer need to worry about compatibility of APIs and documentation update with legacy apps.

* With these feature, it saves communication time between front-end and back-end developers about the API design.

**For API users:**

* You can get different types of data or different data forms by making just one request to the server. It's very convenient and flexible, and it saves sending multiple requests with many different API endpoints.

* It provides CRUD(read and write), Fuzzy Search, Remote Function Calls, etc. Other features include saving duplicate data, checking request history, etc.

Examples
---------

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

