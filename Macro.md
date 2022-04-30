## Valid version

0.9.0+

## Usage

```ruby
kbd.add_layer :default, %i(MACRO_1 MACRO_2)
kbd.define_mode_key :MACRO_1, [ Proc.new { kbd.macro("Hello") }, nil, 200, nil]
kbd.define_mode_key :MACRO_2, [ Proc.new { kbd.macro("World!") }, nil, 200, nil]
```

These macros add a line feed.
If you want it not to add a line feed, add an empty array `[]` at the second argument:

```
Proc.new { kbd.macro("Hello", []) }
```

The second argument accepts an array of the following symbols: `:ENTER` `:ESCAPE` `:BSPACE` `:TAB` `:PGUP` `:DELETE` `:END` `:PGDOWN` `:RIGHT` `:LEFT` `:DOWN` and `:UP`.

