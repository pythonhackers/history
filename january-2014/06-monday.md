System
------------

* Installed Cassandra in 2 node cluster
* Installed OpsCenter + Agents
* Installed NewRelic Agent on cassa1, cassa2, web01
* Stability problems with the cassa2 which was running 1GB machine. Cassandra service was shutting down frequently ( ~30MB RAM
was available). Machine upgraded to 2GB, Oracle Java7 installed, openjdk-7-headless removed

```
ubuntu@cassa2:~# tail -f /var/log/datastax-agent/agent.log
ERROR [os-metrics-5] 2014-01-06 16:01:59,052 Long os-stats collector failed: Cannot run program "iostat": error=2, No such file or directory
```

Agent needs iostat program to send information to the OpsCenter console.
Installed [**sysstat**](http://packages.ubuntu.com/lucid/sysstat) on the machines ( which iostat is part of )

Oracle Java7 Installation procedure for Debian/Ubuntu
```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java7-installer
```

Everything seems to be running smoothly afterwards.


Programming
------------
* Rewrote the Cassandra management.py hierarchy.py connection.py https://github.com/pythonhackers/pythonhackers/commit/ce772e9e2e3a08cf03c0be7f27114e058960ddf1
to both have a gracefiul start
* Partially fixed the Sentry import operation which was causing None object Exceptions ( since it's not initialized correctly)


Release
--------------

* Staging environment upgraded to the latest master
* Added Cassandra config to the ```app.local.cfg```
* Tester JobWorker with test messages. Worked smoothly. Need to add a config to supervisor


Design
--------------

* Thought about the Tutorial object to be able to publish short tutorials about Python functionality/features etc..
Generate HTML from Markdown on ```after_save``` of the Tutorial object. URL could be like ```tutorial/<user_nick>/<tutorial_slug>```

UI
-------------

- Loading 400 projects each time when the ```/open-source/``` path is requested is utterly useless. I bet most people does not pass 50/100 projects. Lets think about a solution; **infinite scroll** with fetch 20 or 50 items per request. The initial request could return 30-50 projects and once the user starts to scroll down, fetch more. Need to implement
JSON response logic with paging or latest index so that we can fetch the correct records from the database. Think about caching as well. 

- Can we just store the complete list on memcache as a JSON object, maybe ?! 
- Flask cache is also involved; how the combination of the two caching mechanism will work together. Think grasshoper later!

Architecture
--------------

- Does Postgres an overkill for PythonHackers ? 

Postgres currently stores User/SocialUser/Projects/Packages/Messages 

I think for storing User information, it is crucial. Also in the worst case scenario like the whole Cassandra cluster is down, we can still serve the website from Postgres. One other benefit is that we can utilize Flask Admin for basic administration stuff, which is extremely handy mostly.

I guess the better strategy could be to decide what object/data to store in Postgres and what not. Stay away from high writes and place them as much as possible to Cassandra, think Postgres as the Master Data store for important things. 
And use Memcache/Redis to cache data as much as possible. 

Enough thinking.

The End.



