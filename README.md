# entail

entails looks logs that are produced by a [nomad job](https://developer.hashicorp.com/nomad/docs/concepts/architecture#job) from _all_ its allocations<br/>
and allows two basic ops with these logs:

* tail'em all in one place
* grep'em all in one place

## how to play

```
$ entail --help

entail 0.0.1
------------
a.k.a. "nomad tail"
-------------------
I tail logs from all nomad allocations for a given job

how to play:

$ entail job [opts]

opts are:

    -h, --help           show this usage details
    -v, --verbose        show details of what is run under the hood
    -t, --task           zoom in on logs for a particular nomad job's task
    -l, --log-root       root directory for "entail" to tail or grep logs from
    -n, --file-name      specific file name to grep
    -g, --grep           a pattern that will be plugged in to "grep -E <pattern>"

example : entail my-job                          ## tail -f logs from all allocations of my-job
example : entail my-job -t my-task               ## if a job has one or more tasks
example : entail my-job -l /opt/app/hubble/logs  ## changing a log root directory to tail / grep from
example : entail my-job -g "soft[^[:space:]]+"   ## grep -E "soft[^[:space:]]+"

make sure NOMAD_ADDR and NOMAD_TOKEN are exported/set to point to the correct environment
```

### tail'em all

tailing logs from all the allocations of a job named "hubble":

```bash
$ entail hubble
hit ctrl-c to stop
-------------------------------------------------------------------------------------
looking at logs for       "hubble" app
log file                  /alloc/logs/hubble.log

                          allocation | version | node client
-------------------------------------------------------------------------------------
fffced31-0168-4b63-1e58-5f62d05a0857 |   v1.42 | nomad-dev-client-i-076921e2a56a65500
eba351b6-a1f1-3983-bdcb-6e7b8c9f27bd |   v1.42 | nomad-dev-client-i-014af3afd328a7a30
38e93fd6-2183-ecae-80c6-7ea75370d193 |   v1.42 | nomad-dev-client-i-0e5a4c7134c7fe2c5
-------------------------------------------------------------------------------------
2022-11-24T05:17:41,473 [pool-1-thread-1] INFO  ...
2022-11-24T06:37:43,680 [async-dispatch-5] INFO  ...
2022-11-24T06:37:43,764 [async-dispatch-6] INFO  ...
2022-11-24T06:37:43,880 [async-dispatch-7] INFO  ...
...
```

### grep'em all

looking for something, a.k.a. grepping (`-g`) inside all the logs of all the allocations of a "hubble" job:

```bash
$ entail flow -g "Horsehead"
hit ctrl-c to stop
-------------------------------------------------------------------------------------
looking at logs for       "hubble" app
log file                  /alloc/logs/hubble.log

                          allocation | version | node client
-------------------------------------------------------------------------------------
fffced31-0168-4b63-1e58-5f62d05a0857 |   v1.42 | nomad-dev-client-i-076921e2a56a65500
2022-11-24T05:17:41,473 [pool-1-thread-1] INFO  enter the Horsehead nebula
2022-11-24T06:37:43,680 [async-dispatch-5] INFO  ...

eba351b6-a1f1-3983-bdcb-6e7b8c9f27bd |   v1.42 | nomad-dev-client-i-014af3afd328a7a30
2022-11-24T05:18:41,123 [pool-1-thread-2] INFO  a small dark nebula in the constellation Orion is known as Horsehead
2022-11-24T06:27:41,489 [async-dispatch-15] INFO  ...

38e93fd6-2183-ecae-80c6-7ea75370d193 |   v1.42 | nomad-dev-client-i-0e5a4c7134c7fe2c5
2022-11-23T19:42:14,350 [async-dispatch-3] INFO  The Horsehead Nebula (also known as Barnard 33)...
2022-11-23T19:42:14,470 [async-dispatch-4] INFO  ...
-------------------------------------------------------------------------------------
```

## rationale

started as a [proposal](https://github.com/hashicorp/nomad/issues/10308)<br/>

## license

Copyright © 2022 tolitius

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.
