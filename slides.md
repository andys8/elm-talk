%title: Functional Programming with Elm
%author: andys8 - jambit.com
%date: 2019

# Agenda

- Elm
  - Purpose
  - Features
- JavaScript to Elm
  - Functions
  - Types
  - Syntax
- Getting started
  - The Elm Architecture
  - Ellie
  - create-elm-app
- Vim in Elm
  - The Vim editor
  - Implementation
  - Tests

---

~~~

                     .://+ooosoo++/:-`
                `:+ssssssoooooossssss+:.
              .+sssso/-.``     `.-/+ossso:`
            .+ssso:.           ```  `:+ssso-
           :ssso:`       `.:+osyyys:   .+sss+`
          /sss+`      `:oyhhhhhhhhy.     :ssso`
         :sss+`     .+yhhhhhhhhhho..-/+:  -sss+
        `osso`    `/yhhhhhhhhhhs:/shhhhs   /sss-
        -sss/    `shhhhhhhhhys+shhhhhhh+   -sss/
        -sss:    shhhhhhhhyooyhhhhhhhhy`   .sss+
        .sss/   :hhhhhhyo+syhhhhhhhhhs.    -sss/
         osso`  +hhhyo/:ohhhhhhhhhhy/`     +sss.
         -sss+` `::.``+hhhhhhhhhhy+.      :sss/
          :sss+.    `shhhhhhhhs+-`      `/sss+`
           -osso/.  .+oooo+/-.`       `:osss/`
            `/ssso/-`               ./osss+.
              ./ossso+:-..`````.-:+ossss/.
                `./osssssssoossssssso/-`
                    `.-:/++++++//:.`

~~~

-------------------------------------------------

# Elm - A delightful language

For reliable webapps

---

Generate JavaScript with

_*great performance*_ and _*no runtime exceptions*_.

---

## Alternatives

- PureScript
- TypeScript
- ClojureScript
- ReasonML

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

Data *in*, data *out*


\     Input   +--------------+  Output
\ +---------->+   Function   +---------->
\             +--------------+


- No side effects
- Referential transparency
- Testable

---

## Strong type system

Errors at _compile time_

"If it compiles, it works"

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

# Elm 0.19

## Small asset size (RealWorld app)

- 100kb Vue 2.5
- 93kb Angular 6
- 77kb React 16.4
- 29kb Elm 0.19

## Fast compilation

Under 2 seconds for 50k lines of code
From scratch

[Source Blog](https://elm-lang.org/blog/small-assets-without-the-headache)

---

# Elm 0.19: Dead code elimination

*Function-level* dead code elimination.

Possible because:

- Elm functions cannot be redefined or removed at runtime.
- Every package is written entirely in Elm

-------------------------------------------------

## From JavaScript to Elm

[JavaScript to Elm](https://elm-lang.org/docs/from-javascript)

---

## In JavaScript

~~~elm
const name = "my-name";

function add(x, y) {
  return x + y;
}

const result = add(1, 2);
~~~

## In Elm

~~~elm
name = "my-name"

add x y = x + y

result = add 1 2
~~~

---

## Elm (with optional type annotations)

~~~elm
name : String
name =
    "my-name"

add : Int -> Int -> Int
add x y =
    x + y

result : Int
result =
    add 1 2
~~~

---

## A bit more syntax

---

## Records (like Objects)

```elm
type alias Point = { x:Float, y:Float }

origin : Point
origin =
  { x = 0, y = 0 }
```

---

## Tagged Union Types

```elm
type User
  = Regular String Int
  | Visitor String
```

---

## Parameterized Types

```elm
type RemoteData e a
    = NotAsked
    | Loading
    | Failure e
    | Success a
```

[RemoteData package](https://package.elm-lang.org/packages/krisajenkins/remotedata/latest/RemoteData)

---

_NotAsked_
We haven't asked for the data yet.

_Loading_
We've asked, but haven't got an answer yet.

_Failure_
We asked, but something went wrong.

_Success_
Everything worked, and here's the data.

-------------------------------------------------

# Getting started

- The Elm Architecture
- Ellie
- Create-Elm-App

---

# Counter Example with Elm Architecture

An Elm program contains:

- Model
- Update
- View

---

~~~

       Model                     Message
                +-------------+
         +----->+    View     +-----+
         |      +-------------+     |
         |                          |
         |                          |
         |                          v
       +-+--------------------------+-+
       |          Elm Runtime         |
       +-+--------------------------+-+
         ^                          |
         |                          |
         |                          |
         |      +-------------+     |
         +------+    Update   +<----+
                +-------------+
    New Model                   Prev. Model
    + Side-Effects              + Message

~~~

---

## Model

~~~elm
type alias Model =
    { count : Int }


initialModel : Model
initialModel =
    { count = 0 }
~~~

---

## Update

~~~elm
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

```elm
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

```elm
main : Program () Model Msg
main =
    Browser.sandbox
        { init = initialModel
        , view = view
        , update = update
        }
```

---

## Demo: Counter

[Ellie: Counter implementation](https://ellie-app.com/5zSqhMHGcTya1)

Possible Changes:

- Add *Reset* button
- Add Msg `ChangeWith (Int -> Int)`
- Refactor buttons to use ChangeWith
- Add *Double* button

---

## Create-Elm-App

[Create-Elm-App User Guide](https://github.com/halfzebra/create-elm-app/blob/master/template)

- No build configuration
- Like `create-react-app`
- Webpack based
- Hot module reloading
- Assets, CSS, and JS
- Tests

-------------------------------------------------

# Vim in Elm

- The Vim editor
- Vim in Elm

---

## The Vim editor

[Vim](https://www.vim.org) is known for *HJKL* keybindings

> Vim is a highly configurable _text editor_
> for _efficiently_ creating and changing any kind of text.

---

## Demo: Vim in Elm

Implementation and Tests

- [Demo](https://andys8.github.io/vim-emulation/)
- [Code](https://github.com/andys8/vim-emulation)

-------------------------------------------------

# Summary

- Purpose and language features
- JavaScript to Elm
- The Elm Architecture
- Ellie
- create-elm-app
- Vim in Elm

---

## Learning Resources

Guides, Talks and Workshops

- [Elm Guide](https://guide.elm-lang.org)
- [Sporto Elm Workshop](https://sporto.github.io/elm-workshop)
- [Feldman Workshop](https://frontendmasters.com/courses/intro-elm)
- [Toward a Better Front End Architecture](https://youtu.be/EDp6UmaA9CM)
- [Richard Feldman - Scaling Elm Apps](https://youtu.be/DoA4Txr4GUs)
- [Life of a file](https://youtu.be/XpDsk374LDE)

---

## Help

- [Slack](https://elmlang.herokuapp.com)
- [Discourse](https://discourse.elm-lang.org)
- Usually good documentation

---

> “If only I had a job writing <Haskell|purescript|Elm|X>”
>
> *STOP!*
>
> If you ❤️ that language start teaching it.
> Get people involved. Own it!

[@tpflug (twitter)](https://twitter.com/tpflug/status/908770909305090048)

---

## Controlled Experiment

_Try out_ Elm.

1. Find a *low-risk project* that's a good fit
2. Get it *into production*
3. *Expand* incrementally or *back out*
