## Valid version

|Feature|Version|
|----|----|
|Sounder|0.9.18+|

## Description

PRK can not only make a beep sound but also a music.

As of 0.9.18, Piezoelectric sounder is supported by `Sound` class.

## Basic usage

```ruby
require 'sounder'
sounder = Sounder.new(2) # A pin number that connecs to the sounder
sounder.play "c d e f g a b < c"
```

This plays "Do Re Mi Fa So La Ti Do"

## API

### Sounder#create_song

It creates a new song but doesn't play it.
This method accepts variable-length arguments of String.

```ruby
sounder.create_song "c e g f", "e f d c"
```

### Sounder#replay

It plays the last created song.

```ruby
sounder.replay
```

### Sounder#play

A wrapper method for `Sounder#create_song` and `Sounder#replay`.
As in, it accepts variable-length arguments of String.

```ruby
sounder.play "c e g f", "e f d c"
```

## Preset songs

The list of preset songs:

|Name|
|----|
|beepo|
|pobeep|
|beepbeep|
|oneup|

```ruby
sounder.play Sounder::SONGS[:beepo]
```

## Examples

### Plays the intro of Super Mario at keyboard's start up

```ruby
sounder = Sounder.new(2)
sounder.play "T200 L8 O5 e16. r32 e r e r c e r g r4. > g"
```

### Beeps every time you hit a key

```ruby
sounder = Sounder.new(2)

kbd.before_report do
  if kbd.key_reporting?
    sounder.play Sounder::SONGS[:beepo]
  else
    sounder.playing = false
  end
end
```

## How to write a song?

See [[Music Macro Language]].
