# Using Web Logs for Synthetic Transation Tests

_from [.conf 2015](http://adrichman.github.io/SplunkConf2015/)_

Selenium Testing via Python API

Using: Splunk App for Synthetic Transaction Monitoring
http://apps.splunk.com/app/1880

Sample Data: 1 starting and 1 ending transaction with unique execution id

Failure when no end transaction 

## Problems with manual method:

* two events per test
    - forced to use transaction cmd
    - false positives
    - false alerts when service restarted on indexers

* missing data 
    - no server info
    - no context for failures

* manually building tests is slow
    - slow to building
    - difficult to maintain


## Goals
single event per test
capture error info 
build tests dynamically given an array of info

### `splunktransactions.py`

added possed/warning/failed status

added error info

add server info

combined data into one event

## Building Dynamic Tetss using Splunk Data

Build Splunk User & Report
* minimum privelages
* IIS Logs
* Top sites by unique users over 7 days
* `splunklib` python module
    - needed to modify for > 100 results

## Alerting on Issues

Are tests still running?

Are there failures on individual sites?
    * lookup table for `cc` emails for interested parties per site
    * provide link to relevant dashboard in alert emails

Did failures exceed a pre-defined failure_kpi 

## in the future: 

Distrubute via Seleniium Grid?

Interface in splunk for individual users to subscribe to alerts

Adding sites to manual list

Ability to blacklist sites

Combine tests failures inline with IIS logs