ActiveSupport method: `PHash.from_xml`

```rb
xml = <<-XML
  <?xml version="1.0" encoding="UTF-8"?>
    <hash>
      <foo type="integer">1</foo>
      <bar type="integer">2</bar>
    </hash>
XML

hash = Hash.from_xml(xml)
```
