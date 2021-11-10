# Functional Programming as SQL
---

### generate some data for the examples

https://www.json-generator.com/

```js
[
  '{{repeat(400,401)}}',
  {
    index:      '{{index()}}',
    firstname:	'{{firstName()}}',
    lastname:	'{{surname()}}',
    birtYear:	'{{ 2021 - integer(20,40) }}',
    country:	'{{random ( country(), country(),  country()) }}'
  }
]
```

result 
```JSON
[
  {
    "index": 0,
    "firstname": "Haney",
    "lastname": "Ramos",
    "birtYear": 1993,
    "country": "Belarus"
  },
  {
    "index": 1,
    "firstname": "Erin",
    "lastname": "Dale",
    "birtYear": 1983,
    "country": "Yugoslavia"
  },
  ...
]
```

#### SQL querry

As it turns out, thinking in terms of a query language when building programs is similar to the operations applied to arrays in functional programming.

```sql
SELECT firstname FROM Person
    WHERE birthYear > 1990 AND country IS NOT 'Yugoslavia'
    ORDER BY firstname
```
#### aliasing in `lodash` 

Alias some `lodash` functions to look like **SQL** syntax:

```js
_.mixin({'select':   _.map,
         'from':     _.chain,
         'where':    _.filter,
         'sortBy':   _.sortByOrder});
```

#### JS querry

```js

const jsQuerry = _.from(persons)
                  .where( p => p.birtYear > 1990 && p.country !== 'Yugoslavia' )
                  .sortBy(['firstname'])
                  .select( p=> p.firstname )
//apply the querry                  
let jsQuerryResult = jsQuerry.value()
```

 Like SQL, this JavaScript code models the data in the form of functions, also known as **functions as data**. Because it’s declarative, it describes **what** the data output is and not **how** it came to be.