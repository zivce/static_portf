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

### Facade

To call the drive API I had to create a facade (I will probably rename it to service don't judge my naming!). Here is the snippet to call the Elixir Drive Client.

```elixir

# drive_facade.ex

  file = %Drive.Model.DriveFile{
          description: "Hello",
          originalFilename: filename,
          mimeType: "application/octet-stream",
          name: filename
        }
        keyword_list = [{:uploadType, "multipart"}]
        case drive_files_create(driveClient, file, filename, keyword_list) do
          {:ok, resp} ->
            resp |> inspect |> Logger.debug
          {:error, error} ->
            error |> inspect |> Logger.error
        end
    {:error, file_error} ->
      file_error |> inspect |> Logger.error
```

```elixir
# drive_files_create function

   %{}
    |> method(:post)
    |> url("/files")
# it is important to get the resource struct first
    |> add_param(:body, :"resource", body)
# after that comes the file
    |> add_param(:file, :"media", file)
    |> add_optional_params(optional_params, opts)
    |> Enum.into([])
    |> (&Connection.request(connection, &1)).()
    |> decode(Drive.Model.DriveFile)

```

Generation of file part is not dynamic, I added that line directly into the client. What you need to do also is to change `%Drive.Model.DriveFile{}` to `Drive.Model.DriveFile`.

That's all for now! More updates coming soon!


