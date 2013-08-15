---
title: Control Structures
has_toc: true
---

## Conditionals

### if / else

There's your traditional if, else if, else structure. The body should be either
a single statement, or a scope.

    #!ooc
    if (off) turnOn()

    if (stressed) {
        breatheIn()
        breatheOut()
    } else if (tired) {
        rest()
    } else {
        allGood()
    }

The condition can be of type `Bool` or a Pointer, in which case it will evaluate to
`true` if it is non-null.

### match / case

`match` is ooc's `switch`, loosely modelled after Scala's. In its simplest form, it tests for equality between an expression and several values:

    #!ooc
    match (numFeets) {
        case 1 => "Ouch"
        case 2 => "Normal"
        case =>
            // what?
            raise("Too many feet")
    }

Each case is a scope of its own - it doesn't require braces. A case with no
expression is a catch-all.

`match` also works with any class `T` that implements the method 'matches?: func -> (other: T) -> Bool'. Another way to get complex types to work in matches is simply to override the `==` operator. Hence, Strings work:

    #!ooc
    match (keyword) {
        case "if" =>
            Keyword IF
        case "match" =>
            Keyword MATCH
        case =>
            Keyword UNKNOWN
    }

A `match` is an expression, if every case ends with an expression. Hence, a match can be used as a return value, or in a function call, on the right hand side of a declaration-assignment (`:=`), etc.

## Loops

### while

