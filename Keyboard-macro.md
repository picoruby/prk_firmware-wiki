## Valid version

0.9.0+

## Description

`Keyboard#macro` will type your keyboard on your behalf.

## Usage

```ruby
kbd.add_layer :default, %i(MACRO_1 MACRO_2)
kbd.define_mode_key :MACRO_1, [ Proc.new { kbd.macro("Hello") }, nil, 200, nil]
kbd.define_mode_key :MACRO_2, [ Proc.new { kbd.macro("World!") }, nil, 200, nil]
```

These macros add a line feed.
If you want it not to add a line feed, add an empty array `[]` at the second argument:

```ruby
Proc.new { kbd.macro("Hello", []) }
```

The second argument accepts an array of the following symbols: `:ENTER` `:ESCAPE` `:BSPACE` `:TAB` `:PGUP` `:DELETE` `:END` `:PGDOWN` `:RIGHT` `:LEFT` `:DOWN` and `:UP`.

The default value of the second argument is `[:ENTER]`.
This is the reason that a line feed is added when you don't pass any second argument.
