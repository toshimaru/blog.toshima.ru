---
layout: post
title: Get URL simply in Ruby
tags: ruby
---

## GET URL

To `GET` URL and the response simply in Ruby:

```rb
require 'net/http'
require 'uri'

uri = URI.parse('https://google.com/')
response = Net::HTTP.get(uri)
```

1. parse URL from URI string
2. `Net::HTTP.get` the parsed URL

## GET JSON-response URL

```rb
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse('http://www.example.com/sample.json')
json = Net::HTTP.get(uri)
result = JSON.parse(json)
```

## Reference

- [JAPANESE] [RubyでJSON形式の結果が返ってくるURLをParseする - Qiita](http://qiita.com/awakia/items/bd8c1385115df27c15fa)
