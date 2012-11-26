PUL Search Solr
===============
This is an instance of [Solr 4.0][solr] pre-configured for PUL-Search. 

On a production system you'll want to make a `solr` user to own and run Solr, (`sudo useradd -d /opt/apache/solr -s /sbin/false solr`) but for debugging it's easier to own and run Solr as yourself.

Either way, you'll need this in /etc/default/jetty, with the appropriate values:

```
JAVA_HOME=/usr/lib/jvm/java-1.7.0-openjdk-amd64
JAVA_OPTIONS="$JAVA_OPTIONS -Dsolr.solr.home=/opt/apache/solr/cores -Djava.util.logging.config.file=etc/logging.properties -Xms2G -Xmx2G -XX:+UseConcMarkSweepGC -XX:NewRatio=3"
JETTY_HOME=/opt/apache/solr  # start.jar should be here
JETTY_USER=solr
JETTY_LOGS=/var/log/solr
```

Adjust any paths as needed, note that the memory setting are __extremely__ conservative, and that we're likely to change garbage collection strategies.

Note also that the value you set for JETTY_USER needs to own the application (SOLR_HOME) directory and the log directory. You won't get any handy log messages about what's wrong if you don't don this, so do it.

You can now start Solr with `jetty.sh start`.

Also, in a production environment, you'll want to register `jetty.sh` to be run as an init script. Assuming you're running a failrly recent instance of Ubuntu:
 * ln -s `$SOLR_HOME/jetty.sh /etc/init.d/jetty`
 * Register the script: `sudo update-rc.d jetty defaults`
 * Start: `sudo service jetty start`
 * Confirm http://localhost:8983/solr

 [solr]: <http://lucene.apache.org/solr> "Solr"