---
layout: "language"
page_title: "coalesce - Functions - Configuration Language"
sidebar_current: "docs-funcs-collection-coalesce-x"
description: |-
  The coalesce function takes any number of arguments and returns the
  first one that isn't null nor empty.
---

# `coalesce` Function

-> **Note:** This page is about Terraform 0.12 and later. For Terraform 0.11 and
earlier, see
[0.11 Configuration Language: Interpolation Syntax](../../configuration-0-11/interpolation.html).

`coalesce` takes any number of arguments and returns the first one
that isn't null or an empty string.

All of the arguments must be of the same type. Terraform will try to
convert mismatched arguments to the most general of the types that all
arguments can convert to, or return an error if the types are incompatible.
The result type is the same as the type of all of the arguments.

## Examples

```
> coalesce("a", "b")
a
> coalesce("", "b")
b
> coalesce(1,2)
1
```

To perform the `coalesce` operation with a list of strings, use the `...`
symbol to expand the list as arguments:

```
> coalesce(["", "b"]...)
b
```

Terraform attempts to select a result type that all of the arguments can
convert to, so mixing argument types may produce surprising results due to
Terraform's automatic type conversion rules:

```
> coalesce(1, "hello")
"1"
> coalesce(true, "hello")
"true"
> coalesce({}, "hello")

Error: Error in function call

Call to function "coalesce" failed: all arguments must have the same type.
```

## Related Functions

* [`coalescelist`](./coalescelist.html) performs a similar operation with
  list arguments rather than individual arguments.
