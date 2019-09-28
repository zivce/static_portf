---
layout: posts
title: Finally uploaded File to Google Drive!
linktitle: google-drive-upload
date: 2019-09-28T09:33:52.897Z
tags:
  - news
  - development
  - elixir
  - phoenix
  - google drive api
  - google services
  - google api v3
categories:
  - DEVELOPMENT
---
## Google Drive Upload

Finally I got the file upload to work as expected. I've used swagger as described in previous posts, but for some reason it won't work like that. I will now list the changes I hade to make in order for it to work.

###  Drive Connection

First I had to change the default adapter for `Tesla`, Elixir package for http requests. First error I got was with `httpc` package. 

```elixir
defmodule Drive.Connection do
  @moduledoc """
  Handle Tesla connections for Drive.
  """

  use Tesla

  adapter :hackney
```

You need to change the the host url to `www.googleapis.com/upload/` for it to be able to upload. After you start the server and start up the upload with `multipart/form-data`, if host stays without upload you will get the `wrongUrlUpload` error, and it will tell you to re-send the request to supplied url. Just listen to the console and you are closer to Drive upload.

```yaml
swagger: '2.0'
schemes:
  - https
host: www.googleapis.com/upload/
basePath: drive/v3
info:
  contact:
    name: Google
```
### Open API Yaml

Yaml file used to generate the api client had `File` model. That was the problem because it interfered with built-in model for File in Java. So I had to change the name to DriveFile. After generating the client stub you will see the Elixir struct create with the name DriveFile.

### 


