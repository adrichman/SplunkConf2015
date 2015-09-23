# Splunk Data Visualization

_from .conf 2015_

Splunk is good a understanding machine data

People are good at understanding visualizations

## Basic Visualization:

* Filter
* Format
* Sort
* Transform

Doing Better:

* Color
* Shape
* Size
* Knowledge

Even Better:

* More knowledge
* Complexity
* Interaction

new Splunk Built-ins:
* single value 
* maps / chloropleths

## Extending Splunk's Capabilities

* Splunk Web Framework and JS
    * Splunk Dashboard Extensions (JS in a panel)
    * Standalone Views
    * Standalone Splunk Apps

### Web Framework

* _Search Manager_ gets data from server and hands it to _Simple Splunk View_

* Scaffold:

```
    appserver / static

        javascript

    default / ui / views

        xml
```

### `SearchManager`

    id: 'manager'

    search: "index=somthing"

### `ResultsView`

    managerId: 'manager'

    el: $('blah')

### `SimpleSplunkView`

    createView - for one time view requirements


    formatData - called before passing data to updateView

### `SearchBarView`
    
    watch for changes in the search bar

XML: in `<query> ... | $filter$ | ...`

JS: `.setPageToken('filter')`

## Resources:

* Developer Guide
* Developer reference app
* Dashboard examples app
* Splunk Web Framework reference
* Splunk Web Framework Toolkit

