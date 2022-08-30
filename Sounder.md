## Valid version

|Feature|Version|
|----|----|
|Sounder|0.9.18+|

## Description

PRK can not only make a beep sound but also play music.

As of 0.9.18, Piezoelectric sounder is supported by `Sounder` class.

## Basic usage

```ruby
require "sounder"
sounder = Sounder.new(2) # A pin number that connecs to the sounder
sounder.play "c d e f g a b < c"
```

This plays "Do Re Mi Fa So La Ti Do"

## API

### Sounder#compile

It creates a new song but doesn't play it.

```ruby
sounder.compile "c e g f e f d c"
```

You can also pass variable-length arguments like this:

```ruby
sounder.compile "c e g f", "e f d c"
```

### Sounder#replay

It plays the last played (compiled) song.

```ruby
sounder.replay
```

### Sounder#play

A wrapper method for `Sounder#compile` and `Sounder#replay`.
As in, it accepts variable-length arguments of String.

```ruby
sounder.play "c e g f", "e f d c"
```

### Sounder#add_song

See [Examles](#examples).

## Preset songs

The list of preset songs:

|Name|
|----|
|beepo|
|pobeep|
|beepbeep|
|oneup|

```ruby
sounder.play :beepo
```

## Examples

### Plays the intro of Super Mario Bros. when the keyboard starts up

```ruby
sounder = Sounder.new(2)
sounder.play "T200 L8 O5 e16. r32 e r e r c e r g r4. > g"
```

You can add your song to the list:

```ruby
sounder = Sounder.new(2)
sounder.add_songs :mario, "T200 L8 O5 e16. r32 e r e r c e r g r4. > g"
sounder.play :mario
```

### Beeps every time you hit a key

```ruby
sounder = Sounder.new(2)

kbd.before_report do
  if kbd.key_reporting?
    sounder.play :beepo
  else
    sounder.playing = false
  end
end
```

Alternatively, the code below is more effective regarding CPU performance:

```ruby
sounder = Sounder.new(2)

sounder.compile :beepo

kbd.before_report do
  if kbd.key_reporting?
    sounder.replay
  else
    sounder.playing = false
  end
end
```

## BTW, how to write a song?

See [[Music Macro Language]].
