---
layout: post
title: Exporting Paper Docs from Dropbox using the Python SDK
date: '2021-04-01 01:14:00 -0600'
published: true
---
Exporting Paper Docs from Dropbox using the Python SDK
======================================================
Dropbox Paper is a collaborative creation tool, included with Dropbox at no cost.  
Originally Paper was a separate repository, but when Dropbox started to integrate Cloud Docs from Google and Microsoft, it made sense to also bring Paper to the Dropbox file system.  
With that, the original Paper API has been deprecated and now you can use the same API endpoints that manipulate files. However you can't download Cloud Docs as you can download normal files. You need to export them.  
There is an endpoint to export Paper files, and I created a Python script to demonstrate its functionality.  
Here it is: [https://github.com/dropbox/DropboxBusinessScripts/blob/master/Paper/paper-export.py]  
Have fun and let me know what you think!