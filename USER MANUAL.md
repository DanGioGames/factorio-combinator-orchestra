# Factorio Music Machine - User Manual

## Arpeggiator
The Arpeggiator purpose is to generate and play arpeggios, given 4 circuit network input signals (see
[Chord](https://en.wikipedia.org/wiki/Chord_(music))) :
* ![](/images/screenshots/virtual-signal-R.png) sets the **root note**
* ![](/images/screenshots/virtual-signal-Q.png) sets the chord **type** (or **quality**)
* ![](/images/screenshots/virtual-signal-P.png) sets the arpeggio **pattern** (arpeggio shape & length)
* ![](/images/screenshots/virtual-signal-O.png) sets a time **offset** for the arpeggio pattern

### Root note
Select a root note by setting the ![](/images/screenshots/virtual-signal-R.png) signal in Arpeggiator's input. It follows the chromatic scale starting from A, meaning that 1 = A ; 2 = A# ; 3 = B etc...

You can go higher than 12 ; setting ![](/images/screenshots/virtual-signal-R.png) to 13, 25 or 37 will also set the root note to A (see [Chromatic scale](https://en.wikipedia.org/wiki/Chromatic_scale)). You can also go lower than 0 but it will break if you go too low.

*Note : the Arpeggiator has a automated chord inverter. Its purpose is to invert chords when their Root note gets too high, in order to provide better voice progressions when changing chords. If you're not happy with the chord inversion you get with a given root note, just add or substract 12 to ![](/images/screenshots/virtual-signal-R.png) and you'll get the same chord in a higher or lower inversion.*

### Chord type
Select a chord type by setting the ![](/images/screenshots/virtual-signal-Q.png) virtual signal in Arpeggiator's input. It will be sent to the Chord molder which will then output 13 notes corresponding to the chord type & root note provided.

Here's the 16 types included in the Chord molder :

Q signal | Chord type | Notes (root position on C)
-------- | ---------- | ------------
1 | Major triad | <img src="/images/chords/maj.png" width="333" height="100" />
2 | Minor triad | <img src="/images/chords/min.png" width="333" height="100" />
3 | Diminished triad | <img src="/images/chords/dim.png" width="333" height="100" />
4 | Augmented triad | <img src="/images/chords/aug.png" width="333" height="100" />
5 | Major seventh | <img src="/images/chords/maj7.png" width="333" height="100" />
6 | Minor seventh | <img src="/images/chords/min7.png" width="333" height="100" />
7 | Dominant seventh | <img src="/images/chords/7.png" width="333" height="100" />
8 | Half-diminished seventh | <img src="/images/chords/min7b5.png" width="333" height="100" />
9 | Diminished seventh | <img src="/images/chords/dim7.png" width="333" height="100" />
10| Rootless altered seventh | <img src="/images/chords/7alt.png" width="333" height="100" />
11| Dominant seventh suspended fourth | <img src="/images/chords/7sus4.png" width="333" height="100" />
12| Dominant seventh suspended second | <img src="/images/chords/7sus2.png" width="333" height="100" />
13| Minor major seventh | <img src="/images/chords/minmaj7.png" width="333" height="100" />
14| Augmented major seventh | <img src="/images/chords/augmaj7.png" width="333" height="100" />
15| Major add second | <img src="/images/chords/majadd2.png" width="333" height="100" />
16| Minor add second | <img src="/images/chords/minadd2.png" width="333" height="100" />

*Note : the Arpeggiator doesn't limit itself to the 3 or 4 notes showed in the Chord type table. Instead, it duplicates the 3 or 4 base notes to higher octaves, to reach a total of 13 playable notes in the full arpeggio.*

### Pattern & Offset

The pattern decide which notes are to be played and when within the 13 chord notes provided by the Chord molder.
