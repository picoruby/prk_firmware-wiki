## Valid version

0.9.0+

## Description

`Keyboard#send_key` will report a keycord according to the argument:

## Usage

```ruby
kbc.send_key :KC_A
```

You can pass multiple keycodes:

```ruby
kbc.send_key :KC_LSFT, :KC_A
```

An array of Symbol can also be used:

```ruby
kbc.send_key %i[KC_LSFT KC_A]
```

See [[Rotary-encoder]] to find an actual example.
