# New Relic University

https://learn.newrelic.com/

![](new-relic-university.png)

# O11y
## Ollie - So "O11Y", if you're really cool, you call it Ollie

> "But "O11Y" if you've queued into this standard, you take a long word, take the first letter, the last letter, and then you count the characters in between. There's your industry term."

> "Because you know what, Praveen, I always miss the V. Every time I type observability. I always miss the V. So O11Y or Oliie, I will never miss a V."

# Monitoring and Ollie

https://www.logicmonitor.com/blog/monitoring-and-o11y-why-you-need-both

- Monitoring alerts when something is wrong, while observability endeavors to understand why.
- The data from the monitoring stack forms a basis of observability.
- Therefore, observability is impossible without some level of monitoring.
- Observability is a practice, while monitoring is driven by technology
- Monitoring only tells you that a problem happened. Ideally, observability tells you what caused that problem.
- Observability identifies unknowns, while monitoring aims at reporting known errors

> "Metrics tell you whether you have a problem, but they don’t tell you the root cause. Common examples would be: a CPU at 100%, a disk that’s full, or a network link that’s dropping packets."

- Observability is more about the relationship between data than the data itself.
- Rather than merely logging numbers, observability helps determine the app’s health by providing insights into the applications’ future performance.
- Observability is a fundamental property of an application and its supporting infrastructure.

# CHAOS ENGINEERING

https://principlesofchaos.org/

Chaos Engineering is the discipline of experimenting on a system in order to build confidence in the system’s capability to withstand turbulent conditions in production.

# Myths and Historical Accidents

https://www.youtube.com/watch?v=pLPMAAOSxSE

![](ted-youtube.png)

# O11y Foodme

https://o11y-foodme.glitch.me/#/customer

![](foodme.png)

# (NRQL) New Relic Query Language

```
SELECT count(*) FROM Transaction where appName = 'O11yFoodMe'
```

![](nrql.png)

```
SELECT uniqueCount(session) from PageView FACET city,countryCode SINCE 1 week ago
SELECT average(duration) from Transaction FACET name SINCE 1 day ago TIMESERIES 
SELECT max(duration) FROM Transaction WHERE appName = 'FoodMe' 
SELECT count(*) FROM Transaction FACET http.statusText
SELECT count(*) FROM Transaction WHERE httpResponseCode != '200'
```

# Custom Instrumentation

## Server Side

```
SELECT count(*) FROM Transaction FACET restaurant
```

```
newrelic.addCustomAttributes({
    'customer': order.deliverTo.name,
    'restaurant': order.restaurant.name,
    'itemCount': itemCount,
    'orderTotal': orderTotal
});
```

## Client Side

```
SELECT count(*) FROM PageAction FACET restaurant,item,qty
```

```
self.items.forEach(
    function(item) {
    newrelic.addPageAction('orderItem', { 
        restaurant: self.restaurant.name, 
        item: item.name,
        qty: item.qty
    });
});
```

# NR Queries

https://docs.newrelic.com/docs/data-apis/understand-data/event-data/default-events-reported-new-relic-produ

```
SELECT count(*) FROM PageView WHERE appName ='O11yFoodMe' FACET countryCode,city SINCE 1 day ago 
```

![](hello-nr.png)

# Scripted Browser Monitors

https://docs.newrelic.com/docs/synthetics/synthetic-monitoring/scripting-monitors/introduction-scripted-browser-monitors/

