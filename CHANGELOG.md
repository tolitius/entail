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

