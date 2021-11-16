#lodash.js
---

 Its toolkit provides important artifacts that empower you to write functional programs, and it contains a rich repertoire of utility functions that handle many common programming tasks. Once it’s installed, you can access its functionality via the global `_` (underscore or low-dash) object.


#### `filter` example

```js
let males = _(people).filter( p => p.gender === "male").value()
let males2 = _.filter(people, p => p.gender === "male")
console.log(JSON.stringify(males))
console.log(JSON.stringify(males2))
```

#### `map` example

```js
let names2 = _(people).map(p => p.name ).value()
let names = _.map(people, p => p.name )
console.log(names);
console.log(names2);
```

### `filter` and `map` example
```js
let namesNonNull =  _(people)
                      .filter(p => p.name )
                      .map(p => p.name)
                      .value()
console.log(namesNonNull);
                  
// more readable

const validName = p => p.name
const getName = p => p.name
let namesNonNull2 =  _(people)
                      .filter(validName)
                      .map(getName)
                      .value()
console.log(namesNonNull2);
```

#### `reduce` example

```js

//count people of same age and return an object with them

let ageStatistics = 
      _(people).reduce( (stats, p) => {
                  stats[p.age] = stats[p.age] ? stats[p.age]+1 : 1;
                  return stats;        
                }, {}       
    );
console.log("age statistics: " + JSON.stringify(ageStatistics, null, 2));
```

#### `filter` `map` `reduce` example

```js
const getAge = person => person.age;
const gatherStats =  (stats, age) => { 
        stats[age]  = (stats[age] ?? 0) + 1; 
        return stats
    };
const ageAvailable = person => person.age;

console.log("age statistics: "  
    + JSON.stringify(
        _(people)
        .filter(ageAvailable)
        .map(getAge)
        .reduce(gatherStats, {})
    )
);
```

#### `some` and `every` example

```js
const ageAvailable = p => p.age
const ageNotAvailable = p => ! ageAvailable(p)

const notAllHaveAge = _(people).some(ageNotAvailable)
console.log("Some don't have the age field: " + notAllHaveAge)

const allHaveAge = _(people).every(ageAvailable)
console.log("All have the age field: " + allHaveAge)
```

#### chaining 

```js

// functional/descriptive implementation
const replaceUnderscore = str => str.replace(/_/, ' ')
let normalizeNames2 = _.chain(names)
                        .fiter(isValid)
                        .map(replaceUnderscore) // not required - _.startCase is doing it
                        .map( el => el.toLowerCase())
                        .map( _.startCase)
                        .uniq()
                        .sort()
                        .value();

```