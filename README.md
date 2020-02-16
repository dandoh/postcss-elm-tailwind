# postcss-elm-tailwind

[tailwind](https://tailwindcss.com) + [elm](http://elm-lang.org) = :rocket:

See the [demo](https://postcss-elm-tailwind-demo.onrender.com/) and [repo](https://github.com/monty5811/postcss-elm-tailwind/tree/master/demo).

[![Actions Status](https://github.com/monty5811/postcss-elm-tailwind/workflows/Node%20CI/badge.svg)](https://github.com/monty5811/postcss-elm-tailwind/actions)

```elm
view : Model -> Html Msg
view model =
    Html.div [ TW.h_screen, TW.w_screen, TW.flex, TW.justify_center, TW.items_center, TW.bg_gray_200 ]
        [ Html.div []
            [ Html.button
                [ E.onClick Decrement
                , TW.px_2
                , TW.px_4
                , TW.text_white
                , TW.bg_blue_500
                , TW.w_full
                ]
                [ Html.text "-" ]
            , Html.div
                [ TW.text_2xl
                , TW.text_center
                , TW.my_4
                ]
                [ Html.text (String.fromInt model) ]
            , Html.button
                [ E.onClick Increment
                , TW.px_2
                , TW.px_4
                , TW.text_white
                , TW.bg_blue_500
                , TW.w_full
                ]
                [ Html.text "+" ]
            ]
        ]
```

## Installation

```
yarn add postcss-elm-tailwind --dev

# OR

npm i -D postcss-elm-tailwind
```

## Usage

### No config

```js
module.exports = {
  plugins: [
    require("tailwindcss"),
    require("postcss-elm-tailwind")()
]
};
```

### With config

```js
module.exports = {
  plugins: [
    require("tailwindcss"),
    require("postcss-elm-tailwind")({
      prefix: "tw-", // you must tell us if you have set a prefix in your tailwind.config.js
      elmFile: "src/Tailwind.elm", // change where the generated Elm module is saved
      elmModule: "Tailwind", // this must match the file name or Elm will complain
      nameStyle: "snake" // "snake" for snake case, "camel" for camel case
    })
  ]
};
```

See the [demo](https://github.com/monty5811/postcss-elm-tailwind/tree/master/demo) for a full example.

## Other things to note

In order to get a small build, you'll need to build Tailwind twice - once
without purgecss to build `TW.elm` with all the classes and once with purgecss
so that all the unused classes are removed from your production CSS.
See how this is implemented in the [demo](https://github.com/monty5811/postcss-elm-tailwind/blob/master/demo/package.json#L20).
