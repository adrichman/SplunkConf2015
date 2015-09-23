# Beyond the Lookup Glass

_from [.conf 2015](http://adrichman.github.io/SplunkConf2015/)_

## Simple Lookups (CSV)

* must re-write file for any change
* need to push file out to all indexers
* big files = big headaches
* automatic lookups via props.conf
* no updating via REST API

## Simple Lookups (KV Store)

* Random Access Updates
* KV Store Captain for Clusters (no guarentee it's same box as search head captain)
* migrating ES -> SHC: outputlookup then inputlookup into cluster when migrating 
* REST API access
* SPLUNK 6.3 - KV Store will send to indexers using modified csv 
* SSL configuration 

## CIDR Lookups

## Incremental update (CSV/KV Store)
```
some_search
| inputlookup append=true ...
| reduce
| outputlookup append=true ...
```

## Time Based Lookups

* KVStore ideal since don't have to regenerate full list repeatedly

## Sentinel Values for Tables

* need to represent keys with null/0 values

```
sourcetype=access_combined action=purchase
| stats sum(price) by productID
| inputlookup append=true productIDs
| chart ...
```

## Avoiding Big Searches

* schedule a shorter window search (e.g. every 15 mins)
* the lookup content is self-updating
* use in dashboards via `| inputlookup`

## Avoiding Big Searches - KV Store

## Short Circuit Cascaded Lookups

* Slow DB Connect query

## Splunk ES and Asset lookup patch

* When you have multiple asset lookup sources ES bindly merges them
