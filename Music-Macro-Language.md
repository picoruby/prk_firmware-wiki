## Valid version

|Feature|Version|
|----|----|
|Music Macro Language|0.9.18+|

## Description

MML (Music Macro Language) is a DSL to describe music.
PRK supports an [MSX](https://en.wikipedia.org/wiki/MSX)-like MML.

## Instructions

All instructions are case insensitive.

|Instruction|Effect|Values|Default|Example|
|----|----|----|----|----|
|T&lt;tempo&gt;|Specifies tempo of the song after this instruction|any|`120`|`T200`, `T60`|
|O&lt;octave&gt;|Specifies octave of the notes after this instruction. Each octave starts from `C` and ends at `B`|`0` to `9`|`4`|`O5`, `O8`|
|L&lt;fraction&gt;[&lt;period&gt;]|Specifies the length of the notes after this instruction|`1` to any|`4`|`L2.`, `L16`|
|A to G[&lt;semitone&gt;][&lt;fraction&gt;][&lt;period&gt;]|Specifies a note from the scale, optionally with a semitone and/or fraction and/or period(s)|`C` `D` `E` `F` `G` `A` `B`||`C+8..`|
|R[&lt;fraction&gt;][&lt;period&gt;]|Specifies a rest|||`R`, `R1.`
|&lt;fraction&gt;|Optionally represents a fraction of a whole note to specify the length of a note or a rest. For example, `4` is a quarter note|||`L8`, `C1`, `R3`|
|&lt;semitone&gt;|Optionally raises or lowers by a semitone the note just before it|`+` or `-`||`C-`, `A+`|
|&lt;period&gt;|Optionally adds a half of the length to the note or rest just before it. Multiple periods are also valid|||`L2.`, `C4..`, `R8.`|
|&lt;|Increases one octave after this instruction|||`O4 A < A` (440 Hz and 880 Hz)|
|&gt;|Decreases one octave after this instruction|||`O4 A > A` (440 Hz and 220 Hz)|
