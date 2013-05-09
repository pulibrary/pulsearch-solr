PUL Search Solr
===============
This is an instance of [Solr ~~4.1~~ 4.3][solr] pre-configured for PUL-Search. 

On a production system you'll want to make a `solr` user to own and run Solr, (`sudo useradd -s /sbin/false pulsearch`) but for debugging it's easier to own and run Solr as yourself.

Defaults for running the webapp w/ Jetty are in `etc/default/jetty` (following conventions of an `/etc/default` file, but this way the configs can travel with the app). You can override this file by copying it to `jetty.local` and making changes. Note that only one or the other is read (there is no inheritance) and if a `jetty.local` file exists it will be used.

The only things you're likely to need to adjust there are the JVM memory and garbage collection settings, and the `JETTY_USER`.

The user you set for JETTY_USER needs to own the application directory and the log directory. You won't get any handy log messages about what's wrong if you don't do this, so do it.

You can now start Solr with `jetty.sh start`.

Also, in a production environment, you'll want to register `jetty.sh` to be run as an init script. Assuming you're running a failrly recent instance of Ubuntu:
 * ln -s `$SOLR_HOME/jetty.sh /etc/init.d/jetty`
 * Register the script: `sudo update-rc.d jetty defaults`
 * Start: `sudo service jetty start`
 * Confirm http://localhost:8983/solr

 [solr]: <http://lucene.apache.org/solr> "Solr"
