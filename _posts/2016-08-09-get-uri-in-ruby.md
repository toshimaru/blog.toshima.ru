---
layout: post
title: Get response from URL simply in Ruby
tags: ruby
---

## GET response from URL

To `GET` URL and the response simply in Ruby:

```rb
require 'net/http'
require 'uri'

uri = URI.parse('https://google.com/')
response = Net::HTTP.get(uri)
```

1. parse URL from URI string
2. `Net::HTTP.get` the parsed URL

## GET status code from URL

```rb
require 'net/http'
require 'uri'

uri = URI.parse('https://google.com/')
Net::HTTP.get_response(uri).code
```

## GET JSON-response from URL

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
