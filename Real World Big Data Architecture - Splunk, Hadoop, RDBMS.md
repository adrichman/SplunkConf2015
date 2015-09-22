# Real World Big Data Architecture - Splunk, Hadoop, RDBMS

_.conf 2015_

## Hunk

* Hadoop, NoSQL, EMR, S3 as backends to the search head
* Virtual Index - natively handles Map Reduce
* Schema on the fly (Search-time indexing)
* no real-time searches
* report accelerations

## Alternative Open Source Approach

* hadoop, pig, hive, tez, solr, spark, slider, hbase, phoenix, acccumulo, storm, falcon, atlas, etc...
* cheap storage
* batch distributed processing
* no viz
* no apps
* ++coding

## Real-World Customer Architecture (Example)

* Splunk / Hunk / DBConnect on Search Heads
* 2000 Forwarders > 25 Indexers
* Historical data (VIX) Flume -> 60 Hortonworks nodes for long-term retention
    - 30 Flume Agents -> 60 Hadoop Nodes 
    - 1.2 PB of storage, stored for 2 yrs
* Enrich data (lookup) w/ MySQL (DBConnect)
    - recommend indexing data from DB in splunk
    - `dbmon-tail`
    - `dbmon-dump`
    - `output` splunk -> DB
    - DBXQuery
* ~2TB / day | 250 Users | ~30 Concurrent Users
* Haddop -> Hunk -> Splunk
* A search over history conducts a query of all data storage and combines results
* Can still use other tools (e.g. Spark) and query languages to query the splunk indexed and archived data
* `indexes.conf` defines when data gets archived
* database lookup tables - `lookup` cmd into database