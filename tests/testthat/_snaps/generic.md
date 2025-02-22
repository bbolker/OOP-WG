# new_generic checks its inputs

    Code
      new_generic(1)
    Error <simpleError>
      `name` must be a single string
    Code
      new_generic("")
    Error <simpleError>
      `name` must not be "" or NA
    Code
      new_generic("foo", 1)
    Error <simpleError>
      `dispatch_args` must be a character vector
    Code
      new_generic("foo", "x", function(x) { })
    Error <simpleError>
      `fun` must contain a call to `S7_dispatch()`

# check_dispatch_args() produces informative errors

    Code
      check_dispatch_args(1)
    Error <simpleError>
      `dispatch_args` must be a character vector
    Code
      check_dispatch_args(character())
    Error <simpleError>
      `dispatch_args` must have at least one component
    Code
      check_dispatch_args("")
    Error <simpleError>
      `dispatch_args` must not be missing or the empty string
    Code
      check_dispatch_args(NA_character_)
    Error <simpleError>
      `dispatch_args` must not be missing or the empty string
    Code
      check_dispatch_args(c("x", "x"))
    Error <simpleError>
      `dispatch_args` must be unique
    Code
      check_dispatch_args("...")
    Error <simpleError>
      Can't dispatch on `...`
    Code
      check_dispatch_args("y", function(x, ..., y) { })
    Error <simpleError>
      `dispatch_args` must be a prefix of the generic arguments

# S7_generic printing

    Code
      foo1
    Output
      <S7_generic> foo1(x, ...) with 2 methods:
      1: method(foo1, class_character)
      2: method(foo1, text)
    Code
      foo3
    Output
      <S7_generic> foo3(x, y, z, ...) with 3 methods:
      1: method(foo3, list(class_character, class_integer, class_character))
      2: method(foo3, list(class_character, class_integer, class_logical))
      3: method(foo3, list(class_character, text, class_character))

# S7_generic printing with long / many arguments

    Code
      foo
    Output
      <S7_generic> foo(a, b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u, v, w, x, y, z, ...) with 0 methods:

# check_generic produces informative errors

    Code
      check_generic("x")
    Error <simpleError>
      `fun` must be a function
    Code
      check_generic(function() { })
    Error <simpleError>
      `fun` must contain a call to `S7_dispatch()`
