# Search Optimization

_from [.conf 2015](http://adrichman.github.io/SplunkConf2015/)_

## Basic Search Best Practices

* Ensure as much work as possible is distributed (`| stats`)
* Ensure as little data as possible is moved (limit the time range)
    + use `earliest` and `latest` or  `_index_earliest` and `_index_latest`
    + limit real-time searches
* Scope on metadata fields i.e. `index` ,`sourcetype`
* Use `Fast`, `Smart` search modes if possible
* __Inclusionary__ search terms perform much better than __Exclusionary__
* customize fields in `fields.conf`

## Monitoring searches

* DMC
* Job Inspector
    - Completion Time
    - Number of Events Scanned
    - Search SID
    - Timings from the search command
        + Rawdata
        + KV
        + Lookups
        + Typer (Inefficient Eventtypes)
        + Alias

## Field extraction 

* common: duplicate structured fields
* don't want search time and index type parsing

## Regex Optimization

* Backtracking is expensive
* Diagnostic: high `kv time`
* Good Practices:
    - Prefer `+` to `*`
    - Extract multiple fields together where they appear and are used together
    - Simple expressions are usually better (e.g. IP addresses)
    - Anchor cleanly `^` and `$`
    - Test and benchmark for accuracy and speed
* Benchmark via `search.kv` in job inspector

## Lookups:Best Practice

* use gzippd csv for large lookups
* auto-lookups for commonly used fields
* scope time-based lookups cleanly
* order lookup table by `key` first, then `values`
* when building lookups, use `inputlookup` and `stats` to combine (particularly useful for tracker type lookups)
* benchmark via `search.lookups`

## Avoid Joins / Transactions when possible 

* look at whole pool of data
* use `stats`:
    - `values(field_name)`
    - `range(_time)` works for __duration__
    - `dc(sourcetype)` for knowing you joined multiple sources
    - `eval` nested inside `stats` expressions
    - `searchmatch` for ad-hoc grouping, `eventtypes` if disciplined
        + `range(eval(if(searchmatch("B OR C"), _time, null())) as duration` 

## Using `subsearch` effectively

* when something is sparse in the dataset (e.g. rare errors?)