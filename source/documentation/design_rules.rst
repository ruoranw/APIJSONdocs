API design style guide
======================

1. Methods and API endpoints
----------------------------

**GET** : A general way to get counts. You can use dev tools to make edits in a web browser.

Base_url/get/

.. content-tabs::

    .. tab-container:: tab1
       :title: Request

        .. code-block:: json

           {
              TableName{
              // conditions.
               }
            }

           // eg. To get a post with id = 235:
            {
              "Post"{
              "id": 235
               }
             }

    .. tab-container:: tab2
       :title: Response

        .. code-block:: json

           {
            TableName:{ … },
            “code”:200,
            “msg”:”success”
            }

          // eg.
          {

            “Moment”:{ “id”:235, “userId”:38710, “content”:”..”},
            “code”:200,
            “msg”:”success”
            }


**HEAD** : A general way to get counts. You can use dev tools to make edits in a web browser.

Base_url/head/

.. content-tabs::

   .. tab-container:: tab1
       :title: Request

       .. code-block:: json

          {
           TableName:{
           ...
           }
          }

          // eg. Get the number of posts posted by the user with id =38710:
          {
          "Post":{
          "userId":38710
          }
          }

   .. tab-container:: tab2
       :title: Response

       .. code-block:: json

         {
         TableName:{"code":200, "msg":"success", "count":10},
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




















