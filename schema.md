# Home Assistant UI Schema

With Home Assistant UI, people can define a user interface to render their entities.

## Root

Type: `object`

### `views`

Type: `array` of [`ViewType`](#ViewType).

A list of defined views. Each view will be rendered in it's own tab.

## ViewType

Type: `object`

### `columnWidth`

Type: `float` specifying the width of the column in pixels.
Default: leave up to UI?
Required: no

TODO: Should this be limited to pixels? What about `em`, `%` ?

### `columnCount`

Type: `integer > 0` or `auto`
Default: `auto`
Required: no

The number of columns for this UI. Can be hardcoded or set to auto. When set to `auto`, use the
`columnWidth` property combined with the current screen width of the user to decide the number
of columns.

### `theme`

| Type | `string` |
| Required | no |

The theme to apply to the view component.

More info: [Home Assistant theme docs](https://www.home-assistant.io/components/frontend/#themes)

### `cards`

Type `array` of [`CardType`](#CardType)

A list of cards to show in the UI.

TODO: How do we handle which cards go into which columns?

## CardType

Type: `object`

Defines a card to be shown in the UI. The only thing that `CardType` mandates is the `type`
property. Each card will extend `CardType` and define extra allowed properties.

### `type`

Type: `string`. Valid values: `entities` or string starting with `custom:`.
Required: yes

The type of the card to be shown. If the type starts with `custom:`, that is the web component
tag that will be used.

## CardType - entities

Show a card with a list of entities and the primary way to control them. Tapping on the card
will open the more info dialog.

### `entities`

Type: `array` of [`EntityRowType`](#EntityRowType)
Required: yes

A list of the entities to render.

## EntityRowType

Type: `string` or `object`. If defined as a string, will be transformed into an object with
the string set as entity_id key value: `light.kitchen` -> `{ entity_id: "light.kitchen" }`.

Define the entity that has to be rendered as a row in a list.

### `type`

Type: `string`. Valid values are `default` or string starting with `custom:`.
Required no
Default: `"default"`

The type of the card to be shown. If the type starts with `custom:`, that is the web component
tag that will be used.
