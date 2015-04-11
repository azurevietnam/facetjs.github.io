---
layout: doc_page
---

# facet.js <3 Druid

**Note this section is being written right now**

This section is devoted to explaining facet.js with the assumption you are coming from the Druid world.
A familiarity with the Druid query language is expected here.

There are many Druid [libraries](http://druid.io/docs/0.6.171/Libraries.html) out there but they are 1-1 wrappers of
the Druid API. They save you the hustle of writing JSON but you are still fundamanetaly constrained to the
expressiveness of the Druid query language.


## Basic Druid queries expressed in facet.js

Here are facet queries the would translate directly to single Druid queries.

### TimeBoundary query

*ToDo: add description*

```javascript
$()
  .apply('maxTime', '$wiki.max($timestamp)')
  .apply('minTime', '$wiki.min($timestamp)')
```

### Timeseries query

*ToDo: add description*

```javascript
$()
  .apply('TimeByHour'
    $('wiki').split($('timestamp').numberBucket('PT1H', 'Etc/UTC'), "Time")
      .apply('Count', '$wiki.count()')
      .apply('Added', '$wiki.sum($added)')
      .sort('Time', 'ascending')
  )
```

### TopN query

*ToDo: add description*

```javascript
$()
  .apply('Pages'
    $('wiki').split('$page', "Page")
      .apply('Count', '$wiki.count()')
      .apply('Added', '$wiki.sum($added)')
      .sort('Count', 'descending')
      .limit(10)
  )
```
