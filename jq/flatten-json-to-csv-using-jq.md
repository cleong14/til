---
title: 2025-01-27 - TIL - Flatten JSON to CSV Using JQ
date: 2025-01-27 21:02:58
tags: [flatten-json-to-csv-using-jq, resources, til]
aliases: [today-i-learned, things-i-learned]
---


# 2025-01-27 - TIL - Flatten JSON to CSV Using JQ

How to flatten a JSON object into CSV using JQ.


## Usage

```sh
$ cat file.json | jq -r '.value[] | [ keys[] as $k | .[$k] ] | flatten | @csv' > file.csv
```


## Use Cases

- Convert JSON to CSV
- Flatten JSON array before converting to CSV


## References

- [JSON object values into CSV with jq | DJ Adams](https://qmacro.org/blog/posts/2022/05/19/json-object-values-into-csv-with-jq/)


