%title: Functional Programming with Elm
%author: andys8 - jambit.com
%date: 2019

# Agenda

- Elm
  - Purpose
  - Features
- JavaScript to Elm
  - Function
  - Types
- Getting started
  - The Elm Architecture
  - Ellie
  - create-elm-app
- Vim in Elm
  - The Vim editor
  - Implementation
  - Tests

---

-> MMMMMMMMNmhysooo+oosyhdNMMMMMMMM
-> MMMMMNds+++osyhhhhysoo++shNMMMMM
-> MMMNho+osdNMMMMMMMMMMNdyo++yNMMM
-> MMmo++ymMMMMMNmhyoooooMMNho+odMM
-> Mdo+odMMMMMds/:::::::yMNNMms++hM
-> No++dMMMMd+::::::::+hho+/hMNo++m
-> d++sMMMNs::::::::+o+/::::dMMh++y
-> h++yMMMs::::::/++/::::::oMMMd++s
-> d++sMMm::::/os+/:::::::sNMMMh++y
-> No++dMm+oshdo::::::::+dMMMMmo++m
-> Mmo+odMMMMh/::::::+ymMMMMMdo++hM
-> MMms++sdMMyssssydNNMMMMMmy++odMM
-> MMMMdo++ohmNMMMMMMMMNmhs++ohNMMM
-> MMMMMMmyo++oosyyyysoo++oydNMMMMM
-> MMMMMMMMMNdhyssoossyydmMMMMMMMMM

-------------------------------------------------

# Elm - A delightful language

For reliable webapps

---

Generate JavaScript with

_*great performance*_ and _*no runtime exceptions*_.

---

## Elm

A pure functional language
Everything is immutable
Functions have no side effects

---

## Risks

Small ecosystem
Learning curve
How will we hire people?

---

## Rewards

Fewer rendering bugs
More maintainable code
Growing as developers

[From Rails to Elm and Haskell](https://youtu.be/5CYeZ2kEiOI)
by Richard Feldman


---

## Pure functions

`input -> function -> output`

Data in, data out

- No side effects
- Referential transparency
- Testable

---

## Static typing

At compile time

---

## Known for nice error messages

~~~
This `user` record does not have a `naame` field:

17| myUser = user.naame
                  ^^^^^

This is usually a typo.
Here are the `user` fields that are most similar:

    { name : String
    }

So maybe naame should be name?
~~~

---

# Immutable data

by default

-------------------------------------------------

# From JavaScript to Elm

---

TODO: Javascript Code -> Strikethrough -> Elm Code + Types
TODO: In JS add is exception or undefined, in Elm it's Int
TODO: Example with maybe, extend to be Result

---

# Tuples

---

# Records

---

# Aliases

---

# Immutable data

Explicit data flow

---

# Currying

---

# Pipeline Operator

---

# Union types

---

# Safety

Maybe

---

# RemoteData

As an example

```
type RemoteData e a
    = NotAsked
    | Loading
    | Failure e
    | Success a
```

[RemoteData package](https://package.elm-lang.org/packages/krisajenkins/remotedata/latest/RemoteData)

---

- NotAsked - We haven't asked for the data yet.
- Loading - We've asked, but haven't got an answer yet.
- Failure - We asked, but something went wrong.
- Success - Everything worked, and here's the data.

---

# HTML

Comparison to JSX

-------------------------------------------------

# Getting started

- The Elm Architecture
  - Compare with React/Redux
- Ellie
- create-elm-app

---

# Counter Example with Elm Architecture

An Elm program contains:

- Model
- Update
- View

---

## Model

```
type alias Model =
    { count : Int }


initialModel : Model
initialModel =
    { count = 0 }
```

---

## Update

~~~
type Msg
    = Increment
    | Decrement


update : Msg -> Model -> Model
update msg model =
    case msg of
        Increment ->
            { model | count = model.count + 1 }

        Decrement ->
            { model | count = model.count - 1 }
~~~

---

## View

```
view : Model -> Html Msg
view model =
    div []
        [ div [] [ text <| String.fromInt model.count ]
        , button [ onClick Decrement ] [ text "-1" ]
        , button [ onClick Increment ] [ text "+1" ]
        ]
```

---

## Program

```
main : Program () Model Msg
main =
    Browser.sandbox
        { init = initialModel
        , view = view
        , update = update
        }
```

---


## Example: Counter

[Ellie link with implementation](https://ellie-app.com/5zM2FXJ69KYa1)

## Counter: Possible Refactorings

- Add *Reset* button
- Add Msg `ChangeWith (Int -> Int)`
- Refactor buttons to use ChangeWith
- Add *Double* button

-------------------------------------------------

# Vim in Elm

---

## The Vim editor

Known for "HJKL" keybindings

> Vim is a highly configurable _text editor_
> for _efficiently_ creating and changing any kind of text.

<https://www.vim.org/>

---

## Implementation in Elm

Demo: Implementation and Tests

- [Demo](https://andys8.github.io/vim-emulation/)
- [Code](https://github.com/andys8/vim-emulation)

-------------------------------------------------

# Summary

TODO

---

# Alternatives

PureScript
TypeScript
ClojureScript
ReasonML

---

# Talks

- [Toward a Better Front End Architecture](https://www.youtube.com/watch?v=EDp6UmaA9CM)
- [Richard Feldman - Scaling Elm Apps](https://www.youtube.com/watch?v=DoA4Txr4GUs)

TODO: Elm Guide
TODO: Evan Talk
TODO: Feldman Course

---

[@tpflug on twitter](https://twitter.com/tpflug/status/908770909305090048)

> “If only I had a job writing <Haskell|purescript|Elm|X>”
>
> *STOP!*
>
> If you ❤️ that language start teaching it.
> Get people involved. Own it!
