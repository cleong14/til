# July 26, 2023 TIL - Map Data Structures in Go Are Not Ordered by Default

Map data structures in Go behave differently than other languages.

To ensure predictable outputs when using maps, remember that a map data structure:

- Doesn’t order the data by keys
- Doesn’t preserve the insertion order
- Doesn’t have a deterministic iteration order
- Doesn’t guarantee that an element added during an iteration will be produced during this iteration

### Use Cases

- Knowing and understanding at a deeper level the language you’re working in reduces the risk of false assumptions

### References

- [Making wrong assumptions during map iterations (ordering and map insert during iteration) (#33)](https://github.com/teivah/100-go-mistakes/blob/master/README.md#making-wrong-assumptions-during-map-iterations-ordering-and-map-insert-during-iteration-33)

