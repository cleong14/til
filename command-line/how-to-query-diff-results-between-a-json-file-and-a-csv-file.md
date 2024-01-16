# 2024-01-15 TIL - How to Query/Diff Results Between a JSON File and a CSV File

How to query/diff the results between a JSON file and a CSV file.


## Usage

```bash
#!/usr/bin/env bash

#######################################
# DESCRIPTION:
#   Use `fastgron` to convert JSON file to greppable JSON, 
#   `jq` to query a JSON file, `yq` to query a CSV file, 
#   then perform a diff between the 2 results.
# COMMANDS:
#   `fastgron` - https://github.com/adamritter/fastgron
#   `jq` - https://github.com/jqlang/jq
#   `yq` - https://github.com/mikefarah/yq
# ARGUMENTS:
#   `1-list.json` - JSON file
#   `2-list.csv` - CSV file
# OUTPUTS:
#   `fastgron` - list of greppable `jq` queries
#   `jq` - query results on a JSON file
#   `yq` - query results on a CSV file
# RETURNS:
#   Diff between the 2 results.
#######################################

#######################################
# `fastgron`
#######################################

# `fastgron` outputs all possible `jq` queries that can be used on a JSON file
fastgron 1-list.json

# -u,--ungron  -- ungron: convert fastgron output back to JSON
fastgron 1-list.json | fastgron -u

# make json greppable with `fastgron` and save output to file
fastgron 1-list.json > 1-list.fastgron


#######################################
# `jq`
#######################################

# `jq` will JSON-quote output if it's a string
cat 1-list.json | jq '.data[].name'

# --raw-output  -- don't JSON-quote output if it's a string
cat 1-list.json | jq --raw-output '.data[].name'

# using `jq`, query a JSON file for a value, don't JSON-quote output if it's a string, save output to file
cat 1-list.json | jq --raw-output '.data[].name' > jq-results.txt


#######################################
# `yq`
#######################################

# using `yq`, query a CSV file
cat 2-list.csv | yq --input-format csv '.'

# using `yq`, query a CSV file for a key that has spaces in it
cat 2-list.csv | yq --input-format csv '.[].["A Key With Spaces"]'

# using `yq`, query a CSV file for a key that has spaces in it, save output to file
cat 2-list.csv | yq --input-format csv '.[].["A Key With Spaces"]' > yq-results.txt


#######################################
# diff between `jq-results.txt` and `yq-results.txt`
#######################################

# diff between `jq-results.txt` and `yq-results.txt`
diff jq-results.txt yq-results.txt
```


## Use Cases

- Determine the difference between a JSON file and a CSV file
- Get all possible `jq` queries that can be used on a JSON file


## References

- [adamritter/fastgron: High-performance JSON to GRON (greppable, flattened JSON) converter](https://github.com/adamritter/fastgron)
- [jqlang/jq: Command-line JSON processor](https://github.com/jqlang/jq)
- [mikefarah/yq: yq is a portable command-line YAML, JSON, XML, CSV, TOML and properties processor](https://github.com/mikefarah/yq)

