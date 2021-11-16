The powerful effect of raising this level of **abstraction** is that you begin to think of operations as **agnostic** to the **underlying data** structures used. Theoretically speaking, whether you’re working with arrays, linked lists, binary trees, or otherwise, it shouldn’t change the semantic meaning of your program. For this reason, **functional programming** focuses on **operations** more than on the structure of the data.

```js
const isValid = obj => obj !== null && obj !== undefined
const getCountry = obj => obj.address.country
const gatherStats = (stats, country) => {
    stats[country] = stats[country] ?? { "name" : country, "count" : 0 }
    stats[country].count += 1;
    return stats;
}
const res = _.chain(people)
            .filter(isValid)
            .map(getCountry)
            .reduce( gatherStats, {})
            .values()
            .orderBy("count")
            .reverse()
            .first()
            .value().name

console.log(res)

```

The `_.chain` function can be used to augment the state of an input object by connecting operations that transform the input into the desired output. It’s powerful because, unlike wrapping arrays with the shorthand `_(...)` object, it explicitly makes any function in the sequence **chainable**.

Another benefit of using `_.chain` is that you can create complex programs that behave **lazily**, so **nothing** executes until that last `value()` function is called.