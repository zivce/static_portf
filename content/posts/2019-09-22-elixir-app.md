---
layout: posts
title: Elixir App
linktitle: elixir-api-app
date: 2019-09-22T07:30:19.356Z
tags:
  - elixir
  - development
categories:
  - DEVELOPMENT
---
# Elixir App

## Idea

Hi, I'll be working on elixir app for multi upload. Main idea is to contact multiple API's and send some data. Everything will be done via DynamicSupervisor and multiple workers so it could enable concurrency.

## Tools

I will use swagger to generate the elixir client as it is fairly easy to generate the api with it. Below is command I used to generate api client for YouTube.

```
java -jar swagger-codegen-cli-2.4.8.jar generate -l elixir -i api_spec\youtube.yaml -o lib\elixir-clients\youtube
```

As for deps I used they are listed below.

```ruby
defp deps do
    [
      {:tesla, "~> 0.8"},
      {:poison, "~> 1.3.1"}
    ]
end
```

Tesla will be used for making the connection to API and Poison is used for JSON encoding/decoding. Elixir SDK used is at version 1.9.1. 

## Errors

I had error with poison encoding, as it had to get the map for encoding decoding from API models. To resolve this problem I had to add function `Map.from_struct/2`:

```ruby
defmodule YouTubeData.Deserializer do
  @spec deserialize(struct(), :atom, :atom, struct(), keyword()) :: struct()
  def deserialize(model, field, :list, mod, options) do
    # adding Map.from_struct(mod) will resolve any decoding errors
    model
    |> Map.update!(field, &(Poison.Decode.decode(&1, [as: [Map.from_struct(mod)]])))
  end
  def deserialize(model, field, :struct, mod, options) do
    model
    |> Map.update!(field, &(Poison.Decode.decode(&1, [as: Map.from_struct(mod)])))
  end
  def deserialize(model, field, :map, mod, options) do
    model
    |> Map.update!(field, &(Map.new(&1, fn {key, val} -> {key, Poison.Decode.decode(val, Keyword.merge(options, [as: Map.from_struct(mod)]))} end)))
  end
  def deserialize(model, field, :date, _, _options) do
    value = Map.get(model, field)
    case is_binary(value) do
      true -> case DateTime.from_iso8601(value) do
                {:ok, datetime, _offset} ->
                  Map.put(model, field, datetime)
                _ ->
                  model
              end
      false -> model
    end
  end
end
```
