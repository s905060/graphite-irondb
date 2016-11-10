Graphite-IronDB
================

A plugin for using graphite with the IronDB from Circonus.

Requires Graphite-web 0.10.X.

Graphite-web 0.10.X is currently unreleased. You'll need to install from
source.

Installation
------------

```
$ git clone http://github.com/circonus-labs/graphite-irondb
$ cd graphite-irondb
$ sudo python setup.py install
```

Using with graphite-web
-----------------------

In your graphite's `local_settings.py`:

    STORAGE_FINDERS = (
        'irondb.IronDBFinder',
    )

    IRONDB_URLS = (
        'http://<irondb-host>:<port>/graphite/<account>'
    )

    IRONDB_BATCH_SIZE = 250

Where `irondb-host` is the DNS or IP of an IronDB node, `port` (usually 8112)
is the listening port for IronDB, and <account> is some integer you have been
ingesting your metrics under (see Namespacing in the IronDB docs).  If you have
a multi-node IronDB installation (likely), you should specify multiple URLS
(one for each node in the cluster), or place the IronDB installation behind a
load balancer.  For example,

    IRONDB_URLS = (
        'http://host1:8112/graphite/1',
        'http://host2:8112/graphite/1',
    )

IRONDB_BATCH_SIZE is optional and will default to 250.  Batch size is used to perform
multi-fetch from the IronDB backend if you use graphs with wildcard expansions in the
datapoints.

Changelog
---------

* **0.0.1** (2016-11-10): initial version.