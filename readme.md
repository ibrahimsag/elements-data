Content behind [canberead.com/elements](https://canberead.com/elements). Based on [this translation](http://farside.ph.utexas.edu/books/Euclid/Euclid.html).

# Structure

Array of `Section` for each book.

`Section` is an object of following properties.
 - `id` unique identifier across all books. e.g. `1.47`, `10.d1`, `10.28-lemII`.
 - `title` e.g. 'Proposition 47', 'Lemma II'.
 - `prose` plain text with `{...}` markup for references.
    - `{[a-zA-Z]+ [a-z]+( [a-zA-Z])?}` should match the references
    - e.g. `{oA line}`, `{ABC arc O}`, `{DEFGHK given}`.
 - `points` position of points. Each point is an array of 2 or 3 numbers.
    - e.g. `{'A': [315.0, 515.0], ...}`
 - `letters` the position of the letter drawn on figure relative to the position of the point above.
    - Array of two numbers, radial direction(Math.PI/4) and distance.
    - e.g. `{ 'A': [1], 'B': [5], 'L': [3, 3] }` for `A` is above, `B` below and `L` to the left.
    - Second number in L is for leaving more space. 
 - `shapes` array of shapes. Each shape is itself an array.
    - First element of the shape array is the name of a primitive.
    - Rest are points to be taken as arguments to the primitive.
    - Primitive should be one of `point`, `line`, `polygon`, `circle`, `arc`, `arcc`(ccw arc), `angle`, `curve`, `gnomon`(arc with dashed line).
    - final element can be an object with the following properties `stroke`(stroke color), `strokeWidth`.
 - \*`polygonl` when the polygon is referenced by two diagonal corners in prose, all the corners are found through this map.
 - \*`given` when the reference in prose is not a primitive but should be an array of primitives, this object maps to an array similar to `shapes` above.

`polygonl` and `given` are optional.

`Section` can contain a `figures` array. Each element of the array would be made up of separate `points`, `letters` and `shapes`. Each figure sharing the same canvas but possibly highlighted independently. Prose would then contain `{figure 1}` for highlighting references on just the first figure, `{figure 2}` for highlighting the second figure or `{figure 0}` for highlight all the figures at each reference. Occurence of `{figure ..}` should be at the start of a sentence and marks all the references until another occurence. See [Proposition 3.36](https://canberead.com/elements/3.36) for the motivation.
