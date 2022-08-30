## Valid version

|Feature|Version|
|----|----|
|Music Macro Language|0.9.18+|

## Description

MML (Music Macro Language) is a DSL to describe music.
PRK supports an [MSX](https://en.wikipedia.org/wiki/MSX)-like MML.

See also [[Sounder]].

## Instructions

All instructions are case insensitive.

|Instruction|Effect|Values|Example|
|----|----|----|----|----|
|T&lt;tempo&gt;|Specifies tempo of the song|tempo: `1` to any<br>(default: `120`)|`T200`, `T60`|
|O&lt;octave&gt;|Specifies octave of the notes after this instruction. Each octave starts from `C` and ends at `B`|octave: `0` to `9`<br>(default: `4`)|`O5`, `O8`|
|L&lt;fraction&gt;[&lt;dot&gt;]|Specifies the length of the notes after this instruction|fraction: `1` to any<br><nobr>dot: `.` (multiple dots allowed)</nobr>|`L2.`, `L16`|
|A to G[&lt;semitone&gt;][&lt;fraction&gt;][&lt;dot&gt;]|Specifies a note from the scale, optionally with a semitone and/or fraction and/or dot(s)|<nobr>`C` `D` `E` `F` `G` `A` `B`</nobr><br>semitone: `+` `-`<br>fraction: `1` to any<br><nobr>dot: `.` (multiple dots allowed)</nobr>|`C+8..`|
|R[&lt;fraction&gt;][&lt;dot&gt;]|Specifies a rest|fraction: `1` to any<br><nobr>dot: `.` (multiple dots allowed)</nobr>|`R`, `R1.`|
|&lt;|Increases one octave after this instruction||`O4 A < A` is equivalent to `O4 A O5 A`|
|&gt;|Decreases one octave after this instruction||`O4 A > A` is equivalent to `O4 A O3 A`|
|Q&lt;sustain&gt;|Specifies the ratio of the actual sounding length of the note length derived from the &lt;fraction&gt; value.<br><nobr>Formula: `<sustain> / 8`</nobr>|sustain: `1` to `8`<br>(default: `8`)|<nobr>`Q4 A4 A4` is equivalent to `Q8 A8 R8 A8 A8`</nobr><br><nobr>`Q8 A4 A4` is equivalent to `Q8 A2`</nobr>|

### Common operands

|Operand|Effect|Default|Example|
|----|----|----|----|
|&lt;fraction&gt;|Represents a fraction of a whole note to specify the length of a note or a rest. For example, `4` is a quarter note|`4`|`L8`, `C1`, `R3`|
|&lt;semitone&gt;|Optionally raises or lowers by a semitone the note just before it||`C-`, `A+`|
|&lt;dot&gt;|Optionally adds a half of the length to the note or rest just before it. Multiple periods are also valid||`L2.`, `C..`, `R8.`|
