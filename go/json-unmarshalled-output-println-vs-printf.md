---
title: 2025-01-28 - TIL - JSON Unmarshalled Output - Println vs Printf
date: 2025-01-28 21:15:31
tags: [json-unmarshalled-output-println-vs-printf, resources, til]
aliases: [today-i-learned, things-i-learned]
---


# 2025-01-28 - TIL - JSON Unmarshalled Output - Println vs Printf

The differences between `println` and `printf` when printing JSON unmarshalled output.


## Usage

```sh
1970/01/01 00:00:00 JSON UNMARSHALLED PRINTLN:
1970/01/01 00:00:00 {{0x1400001fc80 0x140000e2ce0 0x140000ab640 0x140000fd290 map[] {}} {0x1400027fcb0  {}}}
1970/01/01 00:00:00 JSON UNMARSHALLED PRINTF:
{<STRUCT1>:{<STRUCT1_KEY1>:0x1400001fc80 <STRUCT1_KEY2>:0x140000e2ce0 <STRUCT1_KEY3>:0x140000ab640 <STRUCT1_KEY4>:0x140000fd290 <STRUCT1_KEY5>:map[] <STRUCT1_KEY6>:{}} <STRUCT2>:{<STRUCT2_KEY1>:0x1400027fcb0 <STRUCT2_KEY2>: <STRUCT2_KEY3_STRUCT1>:{}}}
```


## Use Cases

- Understand the difference between `println` and `printf` when printing JSON unmarshalled output
- Understand when to use `println` and when to use `printf`


## References

- NA


