API design style guide
======================

This chapter introduces methods in APIJSON. These methods are:

+-------------------------+-------------------------------------------------------+
|:ref:`GET <GETdef>`      |It provides a general way to retrieve resources.       |
+-------------------------+-------------------------------------------------------+
|:ref:`HEAD <HEADdef>`    |It provides a general way to count resources satisfying|
|                         |specifics in the request body.                         |
+-------------------------+-------------------------------------------------------+
|:ref:`GETS <GETSdef>`    |It requests for highly secured and confidential data   |
|                         |like bank accounts, birth dates.                       |
+-------------------------+-------------------------------------------------------+
|:ref:`HEADS <HEADSdef>`  |It's used for getting counts of highly secured         |
|                         |resources(eg. bank accounts).                          |
+-------------------------+-------------------------------------------------------+
|:ref:`POST <POSTdef>`    |It creates new resources under the specified parent    |
|                         |resource(TableName).                                   |
+-------------------------+-------------------------------------------------------+
|:ref:`PUT <PUTdef>`      |This method asks the server to update/edit an existing |
|                         |resource.                                              |
+-------------------------+-------------------------------------------------------+
|:ref:`DELETE <DELETEdef>`|This method deletes the specified resource.            |
+-------------------------+-------------------------------------------------------+

Request method tells the server what kind of action the client wants the server to take. The method are also commonly referred to as the request "verb". This chapter will show you how these methods are included in url to send requests.

In the following explanations, the *base_URL* means the root URL. Everything that follows it is known as a URL path. All URL paths are relative to the base URL.

1. APIJSON Methods
------------------

.. _GETdef:

**GET** :
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A general way to retrieve resources.

.. role:: blue

:blue:`base_url/get/`

.. content-tabs::

    .. tab-container:: tab1
       :title: Request

        .. code-block::

            {
             "TableName"{
             // conditions
             }
            }

           // eg. Request a post with id = 235 in table "Post":
            {
             "Post"{
             "id": 235
              }
             }

    .. tab-container:: tab2
       :title: Response

        .. code-block::

           {
            "TableName":{
            ...
            },
            "code":200,
            "msg":”success”
            }

          // eg. The returned response:
          {
           "Moment":{
           "id":235,
           "userId":38710,
           "content":"..."
            },
           "code":200,
           "msg":"success"
          }

.. _HEADdef:

**HEAD** :
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A general way to count resources satisfying specifics in the request body.

.. role:: blue

:blue:`base_url/head/`

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

       .. code-block::

          {
           "TableName":{
           // conditions
           }
          }

          // eg. Get the number of posts posted by the user whose id = 38710:
          {
           "Post":{
           "userId":38710
           }
          }

   .. tab-container:: tab2
       :title: Response

       .. code-block::

         {
          "TableName":{
          "code":200,
          "msg":"success",
          "count":...
          },
           "code":200,
           "msg":"success"
         }

         // eg.
         {
          "Post":{"code":200, "msg":"success", "count":10},
          "code":200,
          "msg":"success"
         }

.. _GETSdef:

**GETS** :
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Request for highly secured and confidential data like bank accounts, birth dates.

.. role:: blue

:blue:`base_url/gets/`

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

        .. code-block::

           // You need to nest a key-value pair

           “tag”: tag

           // at the top level of the request json object. The tag is usually the related table's name.

           //Except that, the structure is the same as **GET**.

   .. tab-container:: tab2
       :title: Response

        .. code-block::

           // Same as **GET**

.. _HEADSdef:

**HEADS** :
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It's used for getting counts of highly secured resources(eg. bank accounts).


.. role:: blue

:blue:`base_url/heads/`

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

       .. code-block::

          // You need to nest a key-value pair

           “tag”: tag

          // at the top level of the request json object.

          //Except that, the structure is the same as **HEAD**.

   .. tab-container:: tab2
       :title: Response

       .. code-block:: json

          //  Same as **HEAD**.

.. _POSTdef:

**POST** :
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The **POST** method creates new resources under the specified parent resource(TableName).

.. role:: blue

:blue:`base_url/post/`

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

       .. code-block::

          {
          "TableName":{…
          },
          "tag":tag
          }

          // Note the id in the object "TableName":{...} has been generated automatically when table is built and can’t be set by the user here.

          // eg. A user with id = 38710 posts a new post：

          {
             "Post":{
               "userId":38710,
               "content":"APIJSON lets interfaces and documents go hell!"
              },
             "tag":"Moment"
          }

   .. tab-container:: tab2
       :title: Response

       .. code-block::

          {
           "Moment":{
             "code":200,
             "msg":"success",
             "id":...
           },
           "code":200,
           "msg":"success"
          }


        // If the request is successful, it should return following object.

          {
             TableName:{
               "code":200,
               "msg":"success",
               "id":38710
             },
             "code":200,
             "msg":"success"
          }

.. _PUTdef:

**PUT** :
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The **PUT** method asks the server to update/edit an existing resource. The part that will be modified is included in the request body.

.. role:: blue

:blue:`base_url/put/`

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

       .. code-block::

            {
               "TableName":{
                 "id":id,
                 …
               },
               "tag":tag
            }

            // You need to either specify the id in the TableName object like the example above or add a id{} object in the request body.

           // The following example makes request to update the content made by id = 235:

            {
               "Post":{
                 "id":235,
                 "content":"APIJSON lets interfaces and documents go hell !"
               },
               "tag":"Post"
            }

   .. tab-container:: tab2
       :title: Response

        .. code-block:: json

           \\ Same as **POST**.

.. _DELETEdef:

**DELETE** :
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The **DELETE** method deletes the specified resource.


.. role:: blue

:blue:`base_url/delete/`

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

       .. code-block::

          {
             TableName:{
               "id":id
             },
             "tag":tag
          }
          // You need to either specify the id in the TableName object like the example above or add a id{} object in the request body.

          // The following example send a request to delete comments made by id = 100,110,120

          {
             "Comment":{
               "id{}":[100,110,120]
             },
             "tag":"Comment[]"
          }

   .. tab-container:: tab2
       :title: Response

       .. code-block::

          {
           "TableName":{
             "code":200,
             "msg":"success",
             "id[]":[...]
             "count":3
           },
           "code":200,
           "msg":"success"
          }

          // The response to the request in the example above

          {
          "Comment":{
          "code":200,
          "msg":"success",
          "id[]":[100,110,120],
          "count":3
          },
          "code":200,
         "msg":"success"
          }

**Note:**

    1. *TableName* means the name of the table that a user interacts with. It's a string with the first letter capitalized. It can be any combination of letters, numbers and underscores. As a key, its value is a jsonObject which may include columns' names in the table.

    2. :code:`“tag”:tag` needs to be included when the request method is neither **GET** nor **HEAD**. The value *tag* is the key of the returned jsonObject in the response body. Usually, it's the name of the related table.

    3. The request form under **GET** and **HEAD** methods are very flexible. The request jsonObject can be nested many levels. However, other methods need to be constrained by adding tags, etc. The structure of the request body needs to conform resources at the backend.

    4. **GETS** and **GET**, **HEADS** and **HEAD** are the same type of operation. For both groups, the request bodies have something different, while the response bodies are the same.

    5. When transmit through HTTP protocal, all the API methods (get,gets,head,heads,post,put,delete) use HTTP **POST** verb.

    6. All jsonObjects are seen as variables or folders with the form of :code:`{...}`. It can store objects or associative arrays.

    7. Each object is related to an individually-addressable resource which has an unique address.


2. Functional Key-Value Pairs
-----------------------------

**Get data in an array:** :code:`/get/{"key[]":{"tableName":{}}}`

The part after the colon is a JSONObject. The :code:`key` is optional. When :code:`key` is as the same as the :code:`tableName`, the JSONObject will be in a simplified form. For example: :code:`{"User[]":{"User":{"id",...}}}` will be written as :code:`{"User[]":{"id",...}}`.

.. toggle-header::
    :header: Example

       `/get/{"User[]":{"count":3,"User":{}}} <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%7D%7D%7D>`_

       In this example, the request is to **GET** 3 users' information. The response includes 3 users information with all categories saved in an array.
-----------------------------------------------------------------------------------

**Get filtered data:** :code:`/get/{"key[]":{"tableName":{"key2{}":[]}}}`

Specifically in this part: :code:`"key2{}":[]`, the part after the colon is a JSONArray which contains :code:`key2`'s values. This part is to specify the conditions that the return should satisfy.

.. toggle-header::
    :header: Example

       `/get/{"User[]":{"count":3,"User":{"id{}":[38710,82001,70793]}}} <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22id%7B%7D%22:%5B38710,82001,70793%5D%7D%7D%7D>`_

       This example shows how to get users's information with id equals 38710,82001,70793.
-----------------------------------------------------------------------------------

**Get data with comparison operation：** :code:`/get/{"key[]":{"tableName":{"id{}":"<=80000,>90000"}}}`

Just as the comparison operation functions in SQL, it's used here to get resources in a range. It dosn't need to be numbers though.

.. toggle-header::
    :header: Example

       `/get/{"User[]":{"count":3,"User":{"id{}":"<=80000,>90000"}}} <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22id%7B%7D%22:%22%3C=80000,%3E90000%22%7D%7D%7D>`_

       In SQL, it'd be :code:`id<=80000 OR id>90000`, which means get User array with id<=80000 | id>90000
-----------------------------------------------------------------------------------


**Get data that contains an element:** :code:`/get/{"key[]":{"User":{"key2<>":[object]}}}`

This also used when the user wants to get data that meets specific conditions. :code:`key2` must be a JSONArray while :code:`object` cannot be JSON.

.. toggle-header::
    :header: Example

       `"/get/{"User[]":{"count":3,"User":{"contactIdList<>":38710}}}":38710 <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22contactIdList%3C%3E%22:38710%7D%7D%7D>`_

       In this example, it requests 3 User arrays whose contactIdList contains 38710. In SQL, this would be :code:`json_contains(contactIdList,38710)`.
-----------------------------------------------------------------------------------

**See if it exists** :code:`/get/{"key":{"key2}{@":{"from":"tableName","tableName":{...}}}}`

In this request url, *}{* means EXISTS; *key2* is the item you want to check.

.. toggle-header::
    :header: Example

       `{"User":
          {"id}{@":{
              "from":"Comment",
              "Comment":{"momentId":15}
              }
              }
              } <http://apijson.cn:8080/get/%7B%22User%22:%7B%22id%7D%7B@%22:%7B%22from%22:%22Comment%22,%22Comment%22:%7B%22momentId%22:15%7D%7D%7D%7D>`_

       In this example, the request is to check if the id whose :code:`momentId = 15` exists. The SQL form would be :code:`WHERE EXISTS(SELECT * FROM Comment WHERE momentId=15)`
-----------------------------------------------------------------------------------

**Include functions in url parameters** :code:`/get/{"Table":{"key":value, key()":"function (key0,key1...)}"`

This will trigger the back-end function(JSONObject request, String key0, String key1...)to get or testify data.

Use - and + to show the order of priority: analyze key-() > analyze the current object > analyze key() > analyze child object > analyze key+()

.. toggle-header::
    :header: Example

       `/get/{"Moment":{"id":301,"isPraised()":"isContain(praiseUserIdList,userId)"}} <http://apijson.cn:8080/get/%7B%22Moment%22:%7B%22id%22:301,%22isPraised()%22:%22isContain(praiseUserIdList,userId)%22%7D%7D>`_

       This will use function boolean :code:`isContain(JSONObject request, String array, String value)`. In this case, client will get :code:`“is praised”: true` (In this case, client use function to testify if a user clicked ‘like’ button for a post.)
-----------------------------------------------------------------------------------

**Refer a value**

.. code-block:: json

    "key@":"key0/key1/.../refKey"

Use forward slash to show the path. The part before the colon is the key that wants to refer. The path after the colon starts with the parent level of the key.

.. toggle-header::
    :header: Example

       `"Moment":{
              "userId":38710
              },
        "User":{
              "id@":"/Moment/userId"
              } <http://apijson.cn:8080/get/%7B%22User%22:%7B%22id@%22:%7B%22from%22:%22Comment%22,%22Comment%22:%7B%22@column%22:%22min(userId)%22%7D%7D%7D%7D>`_

       In this example, the value of :code:`id` in :code:`User` refer to the :code:`userId` in :code:`Moment`, which means :code:`User.id = Moment.userId`. After the request is sent, :code:`"id@":"/Moment/userId"` will be :code:`"id":38710`.
-----------------------------------------------------------------------------------

**Subquery expression**

.. code-block:: json

    "key@":{
        "range": "ALL",
        "from":"Table",
        "Table":{ ... }
    }

Range can be **ALL**, **ANY**. It means which table you want to query. It’s very similar to how you query in SQL. You can also use **COUNT**, **JOIN**, etc.

.. toggle-header::
    :header: Example

       `"id@":{
               "from":"Comment",
               "Comment":{
               "@column":"min(userId)"
                }
               } <http://apijson.cn:8080/get/%7B%22User%22:%7B%22id@%22:%7B%22from%22:%22Comment%22,%22Comment%22:%7B%22@column%22:%22min(userId)%22%7D%7D%7D%7D>`_

       :code: `WHERE id=(SELECT min(userId) FROM Comment)`
-----------------------------------------------------------------------------------

**Fuzzy matching** :code:`"key$":"SQL search expressions"` => :code:`"key$":["SQL search expressions"]`

Any SQL search expression can be applied here.

.. toggle-header::
    :header: Example

       `"name$":"%m%" <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22name$%22:%22%2525m%2525%22%7D%7D%7D>`_

       In SQL, it's :code:`name LIKE '%m%'`, meaning that get *User* with ‘m’ in name.
-----------------------------------------------------------------------------------

**Regular Expression** :code:`"key~":"regular expression"` => :code:`"key~":["regular expression"]`

It can be any regular expressions. Advanced search is applicable.

.. toggle-header::
    :header: Example

       `"name~":"^[0-9]+$" <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22name~%22:%22%5E%5B0-9%5D%252B$%22%7D%7D%7D>`_

       In SQL, it's :code:`name REGEXP '^[0-9]+$'`.
-----------------------------------------------------------------------------------

**Get data in a range** :code:`"key%":"start,end"` => :code:`"key%":["start,end"]`

The data type of start and end can only be either **Boolean**, **Number** or **String**. Eg. "2017-01-01,2019-01-01", ["1,90000", "82001,100000"]. It's used for getting data from a specific time range.

.. toggle-header::
    :header: Example

       `"date%":"2017-10-01,2018-10-01" <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22date%2525%22:%222017-10-01,2018-10-01%22%7D%7D%7D>`_

        In SQL, it's :code:`date BETWEEN '2017-10-01' AND '2018-10-01'`, meaning to get *User* data that registered between 2017-10-01 and 2018-10-01.
-----------------------------------------------------------------------------------

**Make an alias** :code:`"name:alias"`

This changes name to alias in returning results. It’s applicable to column, tableName, SQL Functions, etc. but only in GET, HEAD requests.

.. toggle-header::
    :header: Example

       `/get/{"Comment":{"@column":"id,toId:parentId","id":51}} <http://apijson.cn:8080/get/%7B%22Comment%22:%7B%22@column%22:%22id,toId:parentId%22,%22id%22:51%7D%7D>`_

       In SQL, it's :code:`toId AS parentId`. It'll return *parentID* instead of *toID*.
-----------------------------------------------------------------------------------

**Add / expand an item** :code:`"key+":number/string/array...`

The type of value on the right of the colon is decided by key. Types can be **Number** (such as 82001), **String** (such as "url0"), **JSONArray** (such as ["url0","url1"]). The method can only be **PUT**.

.. toggle-header::
    :header: Example

       :code: `"praiseUserIdList+":[82001]`

       In this example, add id 82001 to the praiser's list. In SQL, it should be :code:`json_insert(praiseUserIdList,82001)`.
----------------

**Delete / decrease an item** :code:`“Key-”:number/string/array...`

It has the contrary function of :code:`“key+”`.

.. toggle-header::
    :header: Example

       :code:`"balance-":100.00`

       This example subtract 100 in the balance. In SQL, it would be :code:`balance = balance - 100.00`.
-----------------------------------------------------------------------------------

**Logical Operators** :code:`&,|,!`

:code:`&,|,!` refer to **AND**, **OR**, **NOT** in SQL respectively. The basic form to use them are: :code:`"key&{}":"conditions"`, :code:`"key|{}":"conditions"`, :code:`"key!{}":Object`.

By default, conditions of the same key are connected with :code:`|` operator. As for different :code:`"key":"conditons"`pairs, the default operator among them is :code:`&`.

.. toggle-header::
    :header: Example

        ① `/head/{"User":{"id&{}":">80000,<=90000"}} <http://apijson.cn:8080/head/%7B%22User%22:%7B%22id&%7B%7D%22:%22%3E80000,%3C=90000%22%7D%7D>`_

        In SQL, it's :code:`id>80000 AND id<=90000`, meaning id needs to be :code:`id>80000 & id<=90000`

        ② `/head/{"User":{"id|{}":">90000,<=80000"}} <http://apijson.cn:8080/head/%7B%22User%22:%7B%22id%7C%7B%7D%22:%22%3E90000,%3C=80000%22%7D%7D>`_.

        It's the same as :code:`"id{}":">90000,<=80000"`. In SQL, it's :code:`id>80000 OR id<=90000`, meaning that id needs to be :code:`id>90000 | id<=80000`.

        ③ `/head/{"User":{"id!{}":[82001,38710]}} <http://apijson.cn:8080/head/%7B%22User%22:%7B%22id!%7B%7D%22:%5B82001,38710%5D%7D%7D>`_.

        In SQL, it's :code:`id NOT IN(82001,38710)`, meaning :code:`id` needs to be :code:`! (id=82001 | id=38710)`.
-----------------------------------------------------------------------------------

3. Build-in string functions part one
-------------------------------------

① :code:`"count":Integer`

This is used to set the maximum number of the returning resources. The maximum number the system supports is 100. Without this, it'll return the maximum number of results that meet the condition.

.. toggle-header::
    :header: Example

        `/get/{"[]":{"count":5,"User":{}}} <http://apijson.cn:8080/get/%7B%22%5B%5D%22:%7B%22count%22:5,%22User%22:%7B%7D%7D%7D>`_

        This example requests 5 Users' data.
-----------------------------------------------------------------------------------

② :code:`"page":Integer`

This is to indicate the page number starting with 0. The max number can be 100. It's usually used with :code:`"count":Integer`

.. toggle-header::
    :header: Example

        `/get/{"[]":{"count":5,"page":3,"User":{}}} <http://apijson.cn:8080/get/%7B%22%5B%5D%22:%7B%22count%22:5,%22page%22:3,%22User%22:%7B%7D%7D%7D>`_

        This example get Users data on page 3 with the total number of 5.
-----------------------------------------------------------------------------------

③ :code:`"query":Integer`

When the :code:`Integer` is 0, it means get the resource. When it's 1, it means counting the number and returning the number.When it's 2, it means returning both.

.. toggle-header::
    :header: Example

        `/get/{"[]":{"query":2, User:{}}, "total@":"/[]/total"} <http://apijson.cn:8080/get/%7B%22%5B%5D%22:%7B%22query%22:2,%22count%22:5,%22User%22:%7B%7D%7D,%22total@%22:%22%252F%5B%5D%252Ftotal%22%7D>`_
-----------------------------------------------------------------------------------

④ :code:`"join":"&/Table0/key0@,</Table1/key1@"`

The joining table functions are represented by symbols:

"<" - LEFT JOIN

">" - RIGHT JOIN

"&" - INNER JOIN

"|" - FULL JOIN

"!" - OUTTER JOIN

.. toggle-header::
    :header: Example

        `/get/{"[]":{"join": "&/User/id@,</Comment/momentId@", "Moment":{}, "User":{"name?":"t", "id@": "/Moment/userId"}, "Comment":{"momentId@": "/Moment/id"}}} <http://apijson.cn:8080/get/%7B%22%5B%5D%22:%7B%22count%22:5,%22join%22:%22&%252FUser%252Fid@,%3C%252FComment%252FmomentId@%22,%22Moment%22:%7B%22@column%22:%22id,userId,content%22%7D,%22User%22:%7B%22name%253F%22:%22t%22,%22id@%22:%22%252FMoment%252FuserId%22,%22@column%22:%22id,name,head%22%7D,%22Comment%22:%7B%22momentId@%22:%22%252FMoment%252Fid%22,%22@column%22:%22id,momentId,content%22%7D%7D%7D>`_

      This examples is equal to SQL expression :code:`Moment INNER JOIN User LEFT JOIN Comment`.
-----------------------------------------------------------------------------------

4. Build-in string functions part two
-------------------------------------

① :code:`"@combine":"&key0,&key1,|key2,key3,!key4,!key5,&key6,key7..."`

This function combines conditions that have been listed to request data. It'll group conditions according to their types. It uses logical operators(&,|,!) to connect among groups while within a group, it'll follow the order that conditions have been listed. So, it'll become :code:`(key0 & key1 & key6 & other keys) & (key2 | key3 | key7) & !(key4 | key5) `

The:code:`other keys` means keys that aren't included in :code:`combine` function. By default, it's connected by AND.

.. toggle-header::
    :header: Example

        `/get/{"User[]":{"count":10,"User":{"@column":"id,name,tag","name~":"a","tag~":"a","@combine":"name~,tag~"}}} <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:10,%22User%22:%7B%22@column%22:%22id,name,tag%22,%22name~%22:%22a%22,%22tag~%22:%22a%22,%22@combine%22:%22name~,tag~%22%7D%7D%7D>`_

        This example request User objects whose :code:`name` or :code:`tag` includes "a".
-----------------------------------------------------------------------------------

② :code:`"@column":"column;function(arg)..."`

This function defines which colunms will be returned.

.. toggle-header::
    :header: Example

       `/get/{"User":{"@column":"id,sex,name","id":38710}} <http://apijson.cn:8080/get/%7B%22User%22:%7B%22@column%22:%22id,sex,name%22,%22id%22:38710%7D%7D>`_

       This request only returns colunms: id, sex, name. The returning follows the same order.
-----------------------------------------------------------------------------------

③ :code:`"@order":"column0+,column1-..."`

This function can set descendent or ascendent order of returning data within a column.

.. toggle-header::
    :header: Example

        `/get/{"[]":{"count":10,"User":{"@column":"name,id","@order":"name-,id"}}} <http://apijson.cn:8080/get/%7B%22%5B%5D%22:%7B%22count%22:10,%22User%22:%7B%22@column%22:%22name,id%22,%22@order%22:%22name-,id%22%7D%7D%7D>`_

        This example requests data following descendent order in name column while the default order in id column.
-----------------------------------------------------------------------------------

④ :code:`"@group":"column0,column1..."`

This function groups data with columns. If the table's :code:`id` has been declared in :code:`@column`, then the :code:`id` needs to be included in :code:`@group`.

.. toggle-header::
    :header: Example

        `/get/{"[]":{"count":10,"Moment":{"@column":"userId,id","@group":"userId,id"}}} <http://apijson.cn:8080/get/%7B%22%5B%5D%22:%7B%22count%22:10,%22Moment%22:%7B%22@column%22:%22userId,id%22,%22@group%22:%22userId,id%22%7D%7D%7D>`_

        This example returns :code:`id` grouped by userId.
-----------------------------------------------------------------------------------

⑤ :code:`"@having":"function0(...)?value0;function1(...)?value1;function2(...)?value2..."`

This function is as same as the **HAVING** function in AQL. Normally, it's used with :code:`@group`.

.. toggle-header::
    :header: Example

        `/get/{"[]":{"Moment":{"@column":"userId;max(id)","@group":"userId","@having":"max(id)>=100"}}} <http://apijson.cn:8080/get/%7B%22%5B%5D%22:%7B%22count%22:10,%22Moment%22:%7B%22@column%22:%22userId%253Bmax(id)%22,%22@group%22:%22userId%22,%22@having%22:%22max(id)%3E=100%22%7D%7D%7D>`_

        This example get an array of Moment with userID and id where id >=100, grouped by userId.
-----------------------------------------------------------------------------------

⑥ :code:`"@schema":"sys"`

