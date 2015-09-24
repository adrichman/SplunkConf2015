# Optimizing Knowledge Objects

_from [.conf 2015](http://adrichman.github.io/SplunkConf2015/)_


## Fields:

each earch segment expanded on its own without context

props.conf for one sourcetype will radiate into `normalizedSearch` of sother sourcetypes when field names match

Avoid calculated fields and field aliases entirely where possible
*   extract fields using standarized names in the first place
*   some calcculated fields can be replaced with `lookups`

monitor their effects where unavoidable

## Reverse Lookups

Automatic lookups in `props.conf`: `[splunk_web_access]`

Other sourcetypes' `props.conf` settings radiate into searches

## Mitigation Strategies

1. subsearch using inputlookup

    - removes the per-sourcetype duplication
    - lets you choose between reverse lookups and classic behavior
    - ignores the configured knowledge per sourcetype
    - more effort required to write and maintain searches
    - Not eventtype-compatible
    - Subsearch overhead

2. Define the per-sourcetype automatic lookup using sourcetype-specific input fields
3. Define the per-sourcetype automatic lookup using sourcetype-specific output fields 
```LOOKUP-ul = user_location user OUTPUT location AS sourcetye_location```
4. Replace per-sourcetype lookups with broader `props.conf` stanzas
5.  `[source::*access.log*]`

## How eventtypes work

store a search filter or fragments thereof in a resuable box

no pipes, no subsearches

run search and see searchCanBeEventType in Job Inspector

events that match an eventtype have their eventtype field set


### Good for:
two different systems likely don't log login attempts the same way

define eventtypes for each system, search on eventtypes
    tag your eventtypes and search ont ags

## Tags (field-value pairs)

give a set of field/value pairs a common name 

homognenized system-specific values to allow unified searches

`tags.conf`
```
[eventtype=splunk_access]
application = enabled
authenticated - enabled
```

avoid long lists of tags mapping to the same field=value
-- especially with eventtypes and reverse lookups 

## Takeaways

Scope knowledge object sharing as narrowly as possible

clean up unused knowledge objects and TAs
