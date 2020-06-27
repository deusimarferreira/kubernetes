# Json

## Find

~~~js
// Find all firstname
$.prizes[*].laureates[*].firstname

// Find all firstname by year 2014
$.prizes[?(@.year == 2014)].laureates[*].firstname
~~~
