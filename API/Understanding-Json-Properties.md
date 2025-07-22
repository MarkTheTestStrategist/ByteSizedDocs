# Overview
When talking about api json (schemas), is it common to call the `key` a property or simply keep the naming convention as "key" with a "value"

* * *

In JSON itself, you typically talk about keys (sometimes called “field names”) and their corresponding values—so you’d say things like:


```
{
  "userId": 123,
  "name": "Alice"
}
```

`"userId"` is a key (or field name)

`123` is its value

* * *


When you move into JSON Schema (the vocabulary and meta-format for describing JSON documents), the term property is the standard name for what you’re defining under the "properties" keyword. For example:

```
{
  "type": "object",
  "properties": {
    "userId": { "type": "integer" },
    "name":   { "type": "string"  }
  },
  "required": ["userId", "name"]
}
```

Here, each entry under `"properties"` is a property in the schema:

`"userId"` is the property name (i.e. the key in your JSON)

`{ "type": "integer" }` is that property’s schema definition

* * *

### Best Practice
In documentation or conversation about raw JSON, keep it simple: call them keys and values.

In the context of JSON Schema, call them properties, because that’s the term the specification uses.