# Decompress a File Replacing It with the Original Uncompressed Version Using Gzip

`gzip` is used for compressing a single file while a tool such as `tar` creates
an archive file by gathering multiple files together into a single file.

We can use `gzip` to decompress a file. For example, to decompress a compressed
file `example.csv.gz` replacing it with the original uncompressed version:

```bash
# Decompress a file, replacing it with the original uncompressed version using gzip [gzip, common]
$ gzip -d example.csv.gz

> example.csv # original, uncompressed version
```

## Use Cases

Decompress `some-file.txt.gz` replacing it with the original uncompressed
version; `some-file.txt`.

## References

- [ELI5: Difference between TAR and ZIP files? : r/explainlikeimfive](https://www.reddit.com/r/explainlikeimfive/comments/9yny8d/eli5_difference_between_tar_and_zip_files/)

