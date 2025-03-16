# 0.1.4

* add colored output for better readability:
  * colorizes log levels (ERROR, WARN, INFO, DEBUG)
  * colorizes timestamps in various formats (ISO with milliseconds, with Z, space separator, timezone offset)
  * colors job name, version and section headers for better visual separation
  * add `--no-color` option to disable colorization (useful when redirecting output to files)
  * adds special support for structured trace formats (like mulog):
    * colorizes function/event names in light blue
    * colorizes outcome values according to status (`:ok` green, `:warn` orange, `:error` red)
    * configurable via environment variables to support other log formats:
      * `TRACE_FUNCTION_NAME` (default: "mulog/event-name")
      * `TRACE_OUTCOME` (default: "mulog/outcome")
      * `TRACE_ID` (default: "traceId")
      * `TRACE_OUTCOME_OK`, `TRACE_OUTCOME_WARN`, `TRACE_OUTCOME_ERROR` for status values

# 0.1.3

* add "`--tail-all`" (`-a`) to support "`tail -f`" for all files inside "`/alloc/logs/*`":

```bash
==> app.stderr.0 <==
2023-05-18 01:07:34.766:DEBUG:...
2023-05-18 01:07:34.766:DEBUG:...
2023-05-18 01:07:34.766:DEBUG:...

==> app.stdout.0 <==
2023-05-18 01:07:34.766:DEBUG:...
2023-05-18 01:07:34.766:DEBUG:...
2023-05-18 01:07:34.766:DEBUG:...

==> redis.stderr.0 <==
...

==> redis.stdout.0 <==
17 May 2023 23:13:14.723 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
```

without "`-a`", by default nomad would only show logs from the standard out (`.stdout`)

_`-g` works for all files (no need for `-a` when grepping)_

