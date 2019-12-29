Client-side Deployment
========================

1. For Android app
------------------

Make sure you have either `ADT Bundle <https://stuff.mit.edu/afs/sipb/project/android/docs/sdk/installing/bundle.html>`_ or `Android Studio <https://developer.android.com/studio>`_ installed.

My configuration:

* Windows 7 + JDK 1.7.0_71 + Android Studio 2.2
* OSX EI Capitan + JDK 1.8.0_91 + Android Studio 3.0
* All the systems and software are 64 bit.

1.Importing

Select **Open an existing Android Studio project > Select the path of APIJSON-Master/APIJSON-Android/APIJSONApp(or APIJSONTest） > OK**

2.Running

**Run > Run app**

3.Testing

In the browser, send a request to the server to see if it responses.

If the default url is not available, change it to an available one, such as the IPV4 address which is running APIJSON project back side. Then click the request button again.

2.For iOS app
--------------

Open xCode, then **APIJSON-Master/APIJSON-iOS/APIJSON-Swift > Open**

In xCode, **Product > Run**

3. For Javascript
------------------

You can use either an IDE or text editor like sublime, Atom, etc. Webstorm is recommended.

While using a text editor, you just open the .html file in the APIJSON-JS folder.

You can also open it with Vue javascript framework. Click `here <https://vuejs.org/>`_ to learn more.