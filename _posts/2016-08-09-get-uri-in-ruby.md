---
layout: post
title: Get HTML/JSON response from URL simply in Ruby
tags: ruby
---

## GET HTML response from URL

To `GET` URL and the response simply in Ruby:

```rb
require 'net/http'
require 'uri'

uri = URI('https://google.com/')
response = Net::HTTP.get(uri)
```

1. Parse URL from URI string
2. `Net::HTTP.get` the parsed URL

## GET HTTP status code from URL

```rb
require 'net/http'
require 'uri'

uri = URI('https://google.com/')
Net::HTTP.get_response(uri).code
```

`get_response` method returns `Net::HTTPResponse` which has methods like `code`, `body`, etc.

## GET JSON response from URL

```rb
require 'net/http'
require 'uri'
require 'json'

uri = URI('http://www.example.com/sample.json')
json = Net::HTTP.get(uri)
result = JSON(json)
```

## Reference

- [Class: Net::HTTP (Ruby 2.3.3)](https://ruby-doc.org/stdlib-2.3.3/libdoc/net/http/rdoc/Net/HTTP.html)
- [JAPANESE] [RubyでJSON形式の結果が返ってくるURLをParseする - Qiita](http://qiita.com/awakia/items/bd8c1385115df27c15fa)
