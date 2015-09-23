# Splunkd

_.conf 2015_

* Server -> Logs to Disk -> Forwarder -> Indexes
* Monitor Input -> Queue -> Processors -> Queue -> Indexer

## Data Structures
* Pipelines, processors, queues
* Pipeline Data
    - conf key uniqifies data streams
    - boolean flags indicate what forwarders data has passed through
* Parsing Pipeline (utf8, linebreaker, header)
    - when univeral forwarder, TCP output goes here
    - if sourcetype is structured data, the rest of the pipeline will be used
* Agg Queue
* Merging Pipeline (aggregator)
* Typing Queue
* Typing Pipeline (regex, annotator)
* Index Queue
* Index Pipeline
