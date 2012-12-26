PUL Search Solr
===============
This is an instance of [Solr 4.0][solr] pre-configured for PUL-Search. 

On a production system you'll want to make a `solr` user to own and run Solr, (`sudo useradd -d /opt/apache/solr -s /sbin/false solr`) but for debugging it's easier to own and run Solr as yourself.

Defaults for Solr / Jetty are in `pulsearch-solr/etc/default/jetty` (following conventions of an `/etc/default` file, but this way the configs can travel with the app). The only thing you're likely to need to adjust there is the JVM memory and garbage collection settings.

Note that the value you set for JETTY_USER needs to own the application directory and the log directory. You won't get any handy log messages about what's wrong if you don't do this, so do it.

You can now start Solr with `jetty.sh start`.

Also, in a production environment, you'll want to register `jetty.sh` to be run as an init script. Assuming you're running a failrly recent instance of Ubuntu:
 * ln -s `$SOLR_HOME/jetty.sh /etc/init.d/jetty`
 * Register the script: `sudo update-rc.d jetty defaults`
 * Start: `sudo service jetty start`
 * Confirm http://localhost:8983/solr

 [solr]: <http://lucene.apache.org/solr> "Solr"