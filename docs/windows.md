# Windows

## robocopy

When using robocopy, you need to supply a source and destination directory. You
will need to create the destination directory if it doesn't already exist.

```text
robocopy <source> <destination> /e /r:1 /w:1
```

Replace `<source>` with the directory you want to copy, and `<destination>` with
the directory to copy to. The `/r` option tells robocopy how many times to retry
a file if there is an error. The `/w` option tells robocopy how long to wait
between tries in seconds. The defaults for `/r` and `/w` are not sane, so we
need to supply them. The `/e` option tells robocopy to copy all subdirectories,
even empty ones.
