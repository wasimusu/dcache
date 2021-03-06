### DistCache (Distributed Cache)
Distcache is a open-source distributed in-memory cache and database.
Operations are mostly asynchronous to achieve high performance.
It is implemented purely in python without any external dependency 
which should make it easier to install and get started with.
One of design goal of this project is ease of use and less cognitive load to users of
similar caching/database systems like Redis, Memcached.

See [wiki](https://github.com/wasimusu/distcache/wiki) or [readthedocs](https://distcache.readthedocs.io/en/latest/) for extensive documentation.

#### Build and test status
<img src="https://travis-ci.com/wasimusu/distcache.svg?branch=master" width="100">
<img src="https://readthedocs.org/projects/distcache/badge/?version=latest">

### Features
1. Data types supported:
    - All basic data types and their combination. For instance, int, str, dict, set, tuple, list, etc and
    objects that have only these types as their attributes are supported.
    - You can even read any object (image, pdfs, etc) in binary format and save them as key, value pair.
2. Key cache operations are logged so when the server fails, the cache can be reconstructed from the log files.
3. The APIs are similar to Memcached and Redis to reduce cognitive when migrating between platforms.
4. Since, distcache has pure python implementation the installation process should painless. It's makes it easier to get started up and running.
5. Its' architecture assumes that the cache clients and servers can fail and plans for it. The impact is minimal on adding and removing cache servers.
6. Snapshot the servers at regular intervals to avoid cold starts upon crash or planned shutdowns
7. Log replays also available for slow but complete reconstruction of the cache upon server crash, error or shutdown.
8. Thread safe increment and decrement operations on keys.
9. Health of the cache servers is monitored by the client.

### Install
```
pip install distcache
```

# Platform
* Linux
* Windows
* Python 2.7 to Python 3.5

#### Same Usage Code
Run server.py and client.py on server and client respectively. You can run client.py on as many PCs but remember 
to ask the server to spawn it once you run client.py. You can run both server and one or more client.py on the same PC.
It will create both server and client locally.

client.py
```
from distcache.cache_client import CacheClient

client = CacheClient()

# Cache operations
client.set("brazil", "football")
client.set("harry", "potter")
client.set(1, 2)
client.set(3, 6)
client.set("hey", "hola")
client.get("hey")
client.get(1)
client.set("hey", "there")
client.get("hey")
client.delete(3)
client.get(3)
client.get("brazil")
```

server.py
```
from distcache.cache_server import CacheServer

server = CacheServer('localhost', 2050)
```
There are more usage codes in the usage directory.

### Usage
- You have multiple servers serving users.
And you need to increment user id across the server such that there is no duplicate.
Similarly you can store product_id, session_id, user_id, etc.
- 80% of the database access is generated by 20% of the queries. You should absolutely not be doing duplicate computations.
Cache the results. And, the figures vary and you can still use caching service. It just makes things faster.

### Contributing
Please read [contributing](https://github.com/wasimusu/distcache/blob/master/contributing.md) to learn how to contribute to this project.