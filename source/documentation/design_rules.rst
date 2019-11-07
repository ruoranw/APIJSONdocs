API design style guide
======================

This chapter introduces methods in API designs with APIJSON. These methods are:

**GET**, **HEAD**, **GETS**, **HEADS**, **POST**, **PUT**, **DELETE**.

Methods are desired actions to be performed on identified resources. This chapter also include how these methods are mapped to HTTP methods.

Base URL means the root address of the website. Everything that follows it is known as a URL path. All API paths are relative to the base URL.

1. Methods and API endpoints
----------------------------

**GET** : A general way to retrieve resources.

Base_url/get/

.. content-tabs::

    .. tab-container:: tab1
       :title: Request

        .. code-block::

            {
             "TableName"{
             // conditions
             }
            }

           // eg. Request a post with id=235 in table "Post":
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


**HEAD** : A general way to retrieve the number of rows in a table satisfying the criteria specified in the request body.

Base_url/head/

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

**GETS** : Get data with high security and confidentiality like bank accounts, birth date.

Base_url/gets/

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

        .. code-block:: json

           // You need to add “tag”: tag with the same level of post{}. Others are the same as **GET**.

   .. tab-container:: tab2
       :title: Response

        .. code-block:: json

           // Same as **GET**

**HEADS** : Get counts of confidential data(eg. bank account).

Base_url/heads/

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

       .. code-block:: json

          // You need to add “tag”: tag with the same level of post{}. Others are the same as HEAD.

   .. tab-container:: tab2
       :title: Response

       .. code-block:: json

          //  Same as HEAD.

**POST** : Add new data to the database.

Base_url/post/

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

       .. code-block:: json

          {
          TableName:{…},
          "tag":tag
          }

          // The id in {...} is generated automatically when table is built and can’t be set by the user.

          // eg. A user with id = 38710 posts a new post：
          {
             "Post":{
               "userId":38710,
               "content":"APIJSON,let interfaces and documents go to hell !"
             },
             "tag":"Moment"
          }

   .. tab-container:: tab2
       :title: Response

       .. code-block:: json

          {
           TableName:{
             "code":200,
             "msg":"success",
             "id":38710
           },
           "code":200,
           "msg":"success"
        }
        // eg.
        {
           "Moment":{
             "code":200,
             "msg":"success",
             "id":120
           },
           "code":200,
           "msg":"success"
        }

**PUT** : Make changes to a specific item. Only change the part sent to server.

Base_url/put/

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

       .. code-block:: json

            {
               TableName:{
                 "id":id,
                 …
               },
               "tag":tag
            }

            // You can also add multiple id as id{}.

           // eg. Make changes to post content with id= 235:
            {
               "Post":{
                 "id":235,
                 "content":"APIJSON,let interfaces and documents go to hell !"
               },
               "tag":"Post"
            }

   .. tab-container:: tab2
       :title: Response

        .. code-block:: json

           \\ Same as POST.

**DELETE** : Delete data.

Base_url/delete/

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

       .. code-block:: json

          {
             TableName:{
               "id":id
             },
             "tag":tag
          }
          // You can also add multiple id as id{}.

          // Or Delete contents with multiple id：
          {
             "Comment":{
               "id{}":[100,110,120]
             },
             "tag":"Comment[]"
          }

   .. tab-container:: tab2
       :title: Response

       .. code-block:: json

          {
             TableName:{
               "id":id
             },
             "tag":tag
          }

          // You can also add multiple id as id{}.

          // Or Delete contents with multiple id：
          {
             "Comment":{
               "id{}":[100,110,120]
             },
             "tag":"Comment[]"
          }


**Note:**

    1. TableName means the name of the table where you get data. It’ll respond with a JSON Object(the form is {....})with columns inside.

    2. “Tag”:tag is needed when methods are not GET or HEAD. The tag after the colon is the key in JSON Object of making requests. Generally, it’s the name of the table you’re looking for.

    3. GET, HEAD are methods for general data requests.They support versatile JSON Object structure. Other methods are used for requesting confidential data and the requesting JSON Object needs to be in the same form/order as that in the database. Otherwise, the request shall be denied.

    4. GETS and GET, HEADS and HEAD return the same type of data. But the request form is a little different.

    5. For HTTP, all API methods (get,gets,head,heads,post,put,delete) make requests with HTTP POST.

    6. All JSON Objects here are with {...} form. You can put items or objects in it.

    7. Each object in the database has a unique address.


2. How to make a request
------------------------

**Get data in arrays:** :code:`"key[]":{}`

The part after the colon is a JSONObject where "key" is optional. When key is the same as the table name, the JSONObject will be in a simplified form. For example: :code:`{Table:{Content}}` will be written as :code:`{Content}`.

.. toggle-header::
    :header: Example

       `{"User[]":{"User":{}}} <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%7D%7D%7D>`_

       This is used for getting data from a user. Here, key and tablename are all “User”, then :code:`{"User":{"id", ...}}` will be written as :code:`{"id", ...}`


----------------

**Get data that meets specific conditions:** :code:`"key{}":[]`

The part after the colon is a JSONArray with conditions inside.

.. toggle-header::
    :header: Example

       `"id{}":[38710,82001,70793] <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22id%7B%7D%22:%5B38710,82001,70793%5D%7D%7D%7D>`_

       In SQL, this would be id :code:`IN(38710,82001,70793)`. It means getting data with id equals 38710,82001,70793.

----------------

**Get data with comparison operation：** :code:`"key{}":"condition0,condition1..."`

Conditions can be any SQL comparision operation. Use''to include any non-number characters.

.. toggle-header::
    :header: Example

       `"id{}":"<=80000,>90000" <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22id%7B%7D%22:%22%3C=80000,%3E90000%22%7D%7D%7D>`_

       In SQL, it'd be id<=80000 OR id>90000, which means get User array with id<=80000 | id>90000

----------------

**Get data that contains an element:** :code:`"key<>":Object` => :code:`"key<>":[Object] `

*key* must be a JSONArray while *Object* cannot be JSON.

.. toggle-header::
    :header: Example

       `"contactIdList<>":38710 <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22contactIdList%3C%3E%22:38710%7D%7D%7D>`_

       In SQL, this would :code:`bejson_contains(contactIdList,38710)`.It means find data of the User whose contactList contains 38710.

----------------

**See if it exists** :code:`"key}{@":{"from":"Table","Table":{ ... }}`

*}{* means EXISTS; *key* is the one you want to check.

.. toggle-header::
    :header: Example

       `"id}{@":{
                 "from":"Comment",
                 "Comment":{
                    "momentId":15
                 }
                } <http://apijson.cn:8080/get/%7B%22User%22:%7B%22id%7D%7B@%22:%7B%22from%22:%22Comment%22,%22Comment%22:%7B%22momentId%22:15%7D%7D%7D%7D>`_

       WHERE EXISTS(SELECT * FROM Comment WHERE momentId=15)

----------------

**Include functions in parameters** :code:`"key()":"function (key0,key1...)"`

This will trigger the back-end function(JSONObject request, String key0, String key1...)to get or testify data.

Use - and + to show the order of priority: analyze key-() > analyze the current object > analyze key() > analyze child object > analyze key+()

.. toggle-header::
    :header: Example

       `"isPraised()":"isContain(praiseUserIdList,userId)" <http://apijson.cn:8080/get/%7B%22Moment%22:%7B%22id%22:301,%22isPraised()%22:%22isContain(praiseUserIdList,userId)%22%7D%7D>`_

       This will use function boolean :code:`isContain(JSONObject request, String array, String value)`. In this case, client will get :code:`“is praised”: true` (In this case, client use function to testify if a user clicked ‘like’ button for a post.)

------------------

**Subquery**

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

----------------

**Fuzzy matching** :code:`"key$":"SQL search expressions"` => :code:`"key$":["SQL search expressions"]`

Any SQL search expression can be applied here.

.. toggle-header::
    :header: Example

       `"name$":"%m%" <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22name$%22:%22%2525m%2525%22%7D%7D%7D>`_

       In SQL, it's :code:`name LIKE '%m%'`, meaning that get *User* with ‘m’ in name.


----------------

**Regular Expression** :code:`"key~":"regular expression"` => :code:`"key~":["regular expression"]`

It can be any regular expressions. Advanced search is applicable.

.. toggle-header::
    :header: Example

       `"name~":"^[0-9]+$" <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22name~%22:%22%5E%5B0-9%5D%252B$%22%7D%7D%7D>`_

       In SQL, it's :code:`name REGEXP '^[0-9]+$'`.

----------------

**Get data in a range** :code:`"key%":"start,end"` => :code:`"key%":["start,end"]`

The data type of start and end can only be either **Boolean**, **Number** or **String**. Eg. "2017-01-01,2019-01-01", ["1,90000", "82001,100000"]. It's used for getting data from a specific time range.

.. toggle-header::
    :header: Example

       `"date%":"2017-10-01,2018-10-01" <http://apijson.cn:8080/get/%7B%22User%5B%5D%22:%7B%22count%22:3,%22User%22:%7B%22date%2525%22:%222017-10-01,2018-10-01%22%7D%7D%7D>`_

        In SQL, it's :code:`date BETWEEN '2017-10-01' AND '2018-10-01'`, meaning to get *User* data that registered between 2017-10-01 and 2018-10-01.

----------------

**Make an alias** :code:`"name:alias"`

This changes name to alias in returning results. It’s applicable to column, tableName, SQL Functions, etc. but only in GET, HEAD requests.

.. toggle-header::
    :header: Example

       `"@column":"toId:parentId" <http://apijson.cn:8080/get/%7B%22Comment%22:%7B%22@column%22:%22id,toId:parentId%22,%22id%22:51%7D%7D>`_

       In SQL, it's :code:`toId AS parentId`. It'll return *parentID* instead of *toID*.

----------------

**Add / expand an item** :code:`"key+":Object`

The type of Object is decided by key. Types can be **Number**, **String**, **JSONArray**. Forms are 82001,"apijson",["url0","url1"] respectively. It’s only applicable to **PUT** request.

.. toggle-header::
    :header: Example

       :code: `"praiseUserIdList+":[82001]`

       In SQL, it's json_insert(praiseUserIdList,82001). Add an id that praised the post.

----------------

**Delete / decrease an item** :code:`“Key-”:object`

It’s the contrary of “key+”.

.. toggle-header::
    :header: Example

       :code:`"balance-":100.00`

       In SQL, it's :code:`balance = balance - 100.00`, meaning there's 100 less in balance.

-----------------

**Operations** :code:`&,|,!`

They're used in logic operations. It’s the same as **AND**, **OR**, **NOT** in SQL respectively.

By default, for the same key, it’s ‘|’ (OR)operation among conditions; for different keys, the default operation among conditions is ‘&’(AND).

.. toggle-header::
    :header: Example

        ① `"id&{}":">80000,<=90000" <http://apijson.cn:8080/head/%7B%22User%22:%7B%22id&%7B%7D%22:%22%3E80000,%3C=90000%22%7D%7D>`_

        In SQL, it's :code:`id>80000 AND id<=90000`, meaning id needs to be :code:`id>80000 & id<=90000`

        ② `"id|{}":">90000,<=80000" <http://apijson.cn:8080/head/%7B%22User%22:%7B%22id%7C%7B%7D%22:%22%3E90000,%3C=80000%22%7D%7D>`_.

        It's the same as :code:`"id{}":">90000,<=80000"`. In SQL, it'sid>80000 OR id<=90000, meaning that id needs to be id>90000 | id<=80000

        ③ `"id!{}":[82001,38710] <http://apijson.cn:8080/head/%7B%22User%22:%7B%22id!%7B%7D%22:%5B82001,38710%5D%7D%7D>`_.

        In SQL, it's :code:`id NOT IN(82001,38710)`, meaning id needs to be :code:`! (id=82001 | id=38710)`.



