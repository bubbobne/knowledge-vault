# Day 1 --- Generics Deep Dive (Wildcards, `<T>`{=html}, Producer/Consumer)

## 1. Wildcard (`?`) --- What It Really Means

`?` means: **unknown type**.

Examples:

-   `List<?>` → completely unknown type
-   `List<? extends Number>` → unknown type that is a subtype of
    `Number`
-   `List<? super Integer>` → unknown type that is a supertype of
    `Integer`

Wildcard = you do NOT know the exact type and you cannot name it.

------------------------------------------------------------------------

## 2. `? extends T` (Read Only)

Example:

``` java
List<? extends Number> list;
```

You can:

``` java
Number n = list.get(0);
```

You cannot:

``` java
list.add(10); // compile error
```

Reason: The list might be `List<Double>` or `List<Integer>`.\
The compiler cannot guarantee that inserting `10` is safe.

Mental model: You can read safely as `T`, but writing is unsafe.

------------------------------------------------------------------------

## 3. `? super T` (Write Safe)

Example:

``` java
List<? super Integer> list;
```

You can:

``` java
list.add(10); // OK
```

You can only read as:

``` java
Object o = list.get(0);
```

Reason: The list might be `List<Object>` or `List<Number>`.\
The most specific safe read type is `Object`.

------------------------------------------------------------------------

## 4. Producer vs Consumer (Correct Interpretation)

View from the method perspective.

If the method READS from the list: → the list PRODUCES values → use
`? extends T`

If the method WRITES into the list: → the list CONSUMES values → use
`? super T`

Example:

``` java
static void copy(List<? extends Number> src,
                 List<? super Number> dest) {
    for (Number n : src) {
        dest.add(n);
    }
}
```

Flow:

src → method → dest\
(producer) (consumer)

------------------------------------------------------------------------

## 5. Why `<T>` Is Different from `?`

Wildcard (`?`) = unknown and NOT nameable.

Type parameter (`<T>`) = unknown BUT consistent and nameable. (aka raw type)

Example that works:

``` java
static <T> void swap(List<T> list, int i, int j) {
    T tmp = list.get(i);
    list.set(i, list.get(j));
    list.set(j, tmp);
}
```

This works because: - `get()` returns `T` - `set()` accepts `T` - The
type is consistent throughout the method

------------------------------------------------------------------------

## 6. Why This Does NOT Work

``` java
static void swap(List<?> list, int i, int j) {
    Object tmp = list.get(i);
    list.set(i, list.get(j)); // compile error
}
```

Reason:

`List<?>` has an unknown internal type (called "capture of ?").\
You cannot safely insert anything except `null` because the compiler
cannot verify type safety.

Even if `list.get(i)` comes from the same list, the compiler cannot
treat `?` as a concrete reusable type.

------------------------------------------------------------------------

## 7. Key Difference Summary

  Type                  Read As    Write
  --------------------- ---------- -------
  `List<T>`             `T`        `T`
  `List<? extends T>`   `T`        ❌
  `List<? super T>`     `Object`   `T`
  `List<?>`             `Object`   ❌

------------------------------------------------------------------------

## 8. Eclipse Practical Tips

### Enable strong compiler feedback

Project → Properties → Java Compiler\
Enable project-specific settings and use the correct JDK level (21).

Preferences → Java → Compiler → Errors/Warnings\
Set: - Raw types → Warning - Unchecked operations → Warning

### Use Ctrl+1 (Quick Fix)

When generics errors appear: - Place cursor on error - Press Ctrl+1 -
Study the suggestion instead of blindly accepting it

### Observe method availability

When using `List<?>`: - `get()` works - `add()` and `set()` are blocked

Use content assist (Ctrl+Space) to see what the compiler allows.

------------------------------------------------------------------------

## 9. Core Insight

`?` means:

"I know this is a list of some type, but I do not have the right to
manipulate that type."

`<T>` means:

"I do not know the type, but I promise it is consistent everywhere in
this method."

That is the conceptual difference between wildcard and generic type
parameter.
