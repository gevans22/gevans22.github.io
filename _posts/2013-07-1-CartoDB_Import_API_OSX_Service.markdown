---
layout: post
title:  "CartoDB Importer API and an OSX Service"
date:   2013-07-1 14:13:18
categories: CartoDB OSX API
---

APIs are great, and the CartoDB team has [recently released](http://blog.cartodb.com/post/54101913823/got-files-weve-got-a-import-api) an importer API. I have been playing around with it a bit as a pretty heavy user of CartoDB and it has been working pretty well. It allows you to do stuff like this:

![OSX Service for Uploading to CartoDB](http://www.galenevans.org/images/cartodb_osx_service.png)  

![Upload Started](http://www.galenevans.org/images/upload_started.png)
![Upload Finished](http://www.galenevans.org/images/upload_finished.png)
![Table in CartoDB](http://www.galenevans.org/images/cartodb_table_uploaded.png)

This was done through creating an OSX Service via Automator and it is pretty easy to do. The service is mainly a wrapper around [the CartoDB upload bash script](https://gist.github.com/andrewxhill/5884845) that was put together by [andrewxhill](https://www.github.com/andrewxhill) at CartoDB. 

To create the service in OSX you want to open Automator and create a new service.

![Create OSX Automator Service](http://www.galenevans.org/images/OSX_Automater_Service.png)

Once you have a blank service you need to add the 'Get Selected Finder Items' action that is located within the 'Files & Folders' area of the actions library. After the 'Get Selected Finder Items' you will need to add 'Run Shell Script' and make sure 'Pass input' is set to 'as arugments'.
![CartoDB Automator Service](http://www.galenevans.org/images/CartoDB_Upload_Service_in_Automator.png)

In the script itself you can copy and past the following and add your own CartoDB Username and 
[API Key](http://developers.cartodb.com/documentation/cartodb-apis.html#authentication). 

<script src="https://gist.github.com/gevans22/5900712.js">
</script>

You can now save the service as "Upload to CartoDB" or however you like and it will now be available when you right click files in Finder.

Update:

I wasn't the biggest fan of the system events pop ups. They required you to close them and also it would have been too intrustive to have pop ups with the status reports from the upload process. As an alternative to this I made a version that using [Growl](http://growl.info/) and the [GrowlNotify](http://growl.info/downloads) command line tool. Growl costs $3 in the app store but pretty useful for this type of thing. It shows alerts like this,

![Growl CartoDB Import Service](http://www.galenevans.org/images/grunt_cartodb_import.png)

Here is the modified shell script,

<script src="https://gist.github.com/gevans22/5908507.js">
</script> 