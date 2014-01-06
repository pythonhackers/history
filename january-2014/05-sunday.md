Programming
----------------
* Job Worker via [RQ](http://python-rq.org/) Thank you [@nvie](https://github.com/nvie) ! What a awesome simple job worker
* Moved Cassandra host setting and keyspace settings to the configuration file so that staging/production can use different keyspaces
* Try/Except block around Cassandra operations, thus stopping the whole cluster will not affect the production trafic once its upgraded. Fallback to Postgres
* Soft start option in the [start_app function](https://github.com/pythonhackers/pythonhackers/blob/06754a19fdde8ac7b221fb3cf8dae5eb2e42220e/pyhackers/app.py#L54)
* Removed Cassandra TimeUUID from Post objects, and replaces ```orig_id``` with ```id``` so that 1 ID for Postgres + Cassandra (https://github.com/pythonhackers/pythonhackers/blob/06754a19fdde8ac7b221fb3cf8dae5eb2e42220e/pyhackers/model/cassandra/hierachy.py#L17)
* Moved HipChat sender, New Message user->timeline distribution to the worker class
* [Twitter-Python-Extractor](https://github.com/ianozsvald/twitter-text-python/) refactored for PythonHackers https://github.com/pythonhackers/pythonhackers/blob/06754a19fdde8ac7b221fb3cf8dae5eb2e42220e/pyhackers/util/textractor.py
* Borrowed [Redirect Link](https://github.com/ianozsvald/twitter-text-python/blob/master/ttp/utils.py) follower from the same project
