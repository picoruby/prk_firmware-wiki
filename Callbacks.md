## Valid version

|Feature|Version|When it runs|
|----|----|----|
|`Keyboard#before_report`|0.9.0+|Every time a key tapped|
|`Keyboard#output_report_changed`|0.9.14+|When the status of "Num Lock", "Caps Lock" and "Scroll Lock" in the host device is changed|
|`Keyboard#on_start`|0.9.18+|On start up of the keyboard|
|`Keyboard#signal_partner`|0.9.18+|When a specific key is tapped|

## Description

Callbacks are kind of hook methods to get called at certain moments of the keyboard's event.

## Usage

Take a good look at the difference in parameters.

```ruby
# Neither method parameter nor block parameter
kbd.before_report do
  # Do something
end
```

```
# Gets a block variable `output`
kbd.output_report_changed do |output|
  # Do something
end
```

```ruby
# Neither method parameter nor block parameter
kbd.on_start do
  # Do something
end
```

```ruby
# Takes a parameter (`:KEYCODE` in this case) before the block
kbd.signal_partner :KEYCODE do
  # Do something on the partner half when :KEYCODE is tapped
  # Naturally, this works only if kbd.split == true
end
```

You can find examples on [[Sounder]] and [[Num Lock, Caps Lock and Scroll Lock]].

