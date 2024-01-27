# 2024-01-26 TIL - Generate Typed Models and Serializers from JSON, JSON Schema, TypeScript, and GraphQL Queries Easy Using Quicktype

`quicktype` generates strongly-typed models and serializers from JSON, JSON Schema, TypeScript, and [GraphQL queries](https://blog.quicktype.io/graphql-with-quicktype/), making it a breeze to work with JSON type-safely in many programming languages.


## Usage

```bash
# Run quicktype without arguments for help and options
quicktype

# quicktype a simple JSON object in C#
echo '{ "name": "David" }' | quicktype -l csharp

# quicktype a top-level array and save as Go source
echo '[1, 2, 3]' | quicktype -o ints.go

# quicktype a sample JSON file in Swift
quicktype person.json -o Person.swift

# A verbose way to do the same thing
quicktype \
  --src person.json \
  --src-lang json \
  --lang swift \
  --top-level Person \
  --out Person.swift

# quicktype a directory of samples as a C++ program
# Suppose ./blockchain is a directory with files:
#   latest-block.json transactions.json marketcap.json
quicktype ./blockchain -o blockchain-api.cpp

# quicktype a live JSON API as a Java program
quicktype https://api.somewhere.com/data -o Data.java
```


## Use Cases

- Generate strongly-typed models and serializers from JSON, JSON Schema, TypeScript, and GraphQL queries


## References

- [glideapps/quicktype: Generate types and converters from JSON, Schema, and GraphQL](https://github.com/glideapps/quicktype)

