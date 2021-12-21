## Valid version

0.9.9+

## Feature
- Supports direct scan, switches connected to separate pins and ground.

## In your `keymap.rb`

```ruby
kbd.set_scan_mode = :direct
kbd.init_pins(
  [],
  [ 8, 27, 28, 29, 9, 26 ]
)
```

or

```ruby
kbd.init_direct_pins(
  [ 8, 27, 28, 29, 9, 26 ]
)
```
