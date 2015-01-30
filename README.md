# pgtune

**pgtune** prints generalized performance optimizations for `postgresql.conf` given the optional inputs `max_connections` and `mem_fraction`. The original `postgresql.conf` file is not an input.

**CAUTION:** This software is experimental. Use of benchmark tests, perhaps with `pgbench`, is advisable.

https://github.com/impredicative/pgtune/

## Help
```
$ ./pgtune.py -h
usage: pgtune.py [-h] [-c MAX_CONNECTIONS] [-f MEM_FRACTION]

postgresql.conf tuner

optional arguments:
  -h, --help            show this help message and exit
  -c MAX_CONNECTIONS, --max-connections MAX_CONNECTIONS
                        minimally necessary maximum connections (default: 100)
                        (min: 1)
  -f MEM_FRACTION, --mem-fraction MEM_FRACTION
                        fraction (>0 to 1.0) of total physical memory (1877MB)
                        to consider (default: 1.0)
```

## Example
### Usage example
```
$ ./pgtune.py --max-connections=32
# pgtune configuration for connections=32 and memory=1877MB.

# CONNECTIONS AND AUTHENTICATION
max_connections = 32

# RESOURCE USAGE (except WAL)
shared_buffers = 469MB
temp_buffers = 36MB
work_mem = 17MB
maintenance_work_mem = 93MB
max_stack_depth = 8MB
vacuum_cost_delay = 50ms
effective_io_concurrency = 4

# WRITE AHEAD LOG
synchronous_commit = off
wal_buffers = 16MB
wal_writer_delay = 10s
checkpoint_segments = 64
checkpoint_timeout = 10min
checkpoint_completion_target = 0.8

# QUERY TUNING
random_page_cost = 2.5
effective_cache_size = 1173MB
```

### Inclusion example
The printed values can be written to a file which can be used by `postgresql.conf` with the *include directive*, as for example:

`include 'postgresql.conf.custom'`

## License

See [license](LICENSE).
