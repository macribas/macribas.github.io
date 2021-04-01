---
layout: post
title: Exporting Paper Docs from Dropbox using the Python SDK
date: '2021-04-01 01:14:00 -0600'
published: true
---
Exporting Paper Docs from Dropbox using the Python SDK
======================================================
[Dropbox Paper](https://www.dropbox.com/lp/create-docs-online) is a collaborative creation tool, included with Dropbox at no cost.  


Originally Paper was a separate repository, but when Dropbox started to integrate Cloud Docs from [Google](https://blog.dropbox.com/topics/product-tips/google-docs-sheets-slides) and [Microsoft](https://blog.dropbox.com/topics/product/dropbox-and-office-online), it made sense to also bring Paper to the Dropbox file system.


With that, [the original Paper API has been deprecated](https://developers.dropbox.com/paper-migration-guide). Because Cloud Docs are, well, in the cloud, they aren't regular files. Most of them are JSON or XML documents that are treated by the web apps as if they were files. Therefore you cannot download them. Instead, if you need to take them out of Dropbox, you need to export them. 


[There is an endpoint to export Paper files](https://dropbox.tech/developers/new-paper-endpoints-released-in-preview), and I created a Python script to demonstrate its functionality.  


[Here it is!](https://github.com/dropbox/DropboxBusinessScripts/blob/master/Paper/paper-export.py)  
Have fun and let me know what you think!
