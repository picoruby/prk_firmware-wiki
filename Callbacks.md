## Valid version

|Feature|Version|When it runs|
|----|----|----|
|`Keyboard#before_report`|0.9.0+|Every time a key tapped|
|`Keyboard#on_start`|0.9.18+|On start up of the keyboard|
|`Keyboard#signal_partner`|0.9.18+|When a specific key is tapped|

## Usage

```ruby
kbd.before_report do
  # Do something
end
```

```ruby
kbd.on_start do
  # Do something
end
```

```ruby
kbd.signal_partner :KEYCODE do
  # Do something on the partner half when :KEYCODE is tapped
  # Naturally, this works only if kbd.split == true
end
```

You can find good examples on [[Sounder]] page.

