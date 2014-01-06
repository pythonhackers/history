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
