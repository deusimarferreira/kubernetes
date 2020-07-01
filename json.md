# Json

## Query get values in Json Path

~~~js
// Find all firstname
$.prizes[*].laureates[*].firstname

// Find all firstname by year 2014
$.prizes[?(@.year == 2014)].laureates[*].firstname

// 0 = Init, 3 = End
$[0:3]

// 0 = Init, 3 = End, 2 = Step
$[0:8:2]
~~~
