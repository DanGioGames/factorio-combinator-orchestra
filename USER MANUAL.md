# Factorio Music Machine - User Manual

## General syntax

Virtual signals like ![](/images/screenshots/virtual-signal-R.png) are represented by their ingame image. Non-image, text letters like A, F, G represent **music notes** following the [English notes naming convention](https://en.wikipedia.org/wiki/Musical_note#12-tone_chromatic_scale).

## Arpeggiator
The Arpeggiator purpose is to generate and play arpeggios, given 4 circuit network input signals (see
[Chord](https://en.wikipedia.org/wiki/Chord_(music))) :
* ![](/images/screenshots/virtual-signal-R.png) sets **root-note**
* ![](/images/screenshots/virtual-signal-Q.png) sets **chord-type** (aka chord **quality**)
* ![](/images/screenshots/virtual-signal-P.png) sets the arpeggio **pattern** (arpeggio shape & length)
* ![](/images/screenshots/virtual-signal-O.png) sets a time **offset** for the arpeggio pattern

### Root note
Select a root note by setting the ![](/images/screenshots/virtual-signal-R.png) signal in Arpeggiator's input. It follows the chromatic scale starting from A, meaning that 1 = A ; 2 = A# ; 3 = B ; 4 = C etc...

You can go higher than 12 ; setting ![](/images/screenshots/virtual-signal-R.png) to 13, 25 or 37 will also set the root note to A (see [Chromatic scale](https://en.wikipedia.org/wiki/Chromatic_scale)). You can also go lower than 0 but it will break if you go too low.

*Note : the Arpeggiator has an automated chord inverter. It outputs an "inversion key" depending on root note, in order to provide better voice progressions when changing chords. If you're not happy with the chord inversion you get with a given root note, just add or substract 12 to ![](/images/screenshots/virtual-signal-R.png) and you'll get the same chord in a higher or lower inversion.*

### Chord type
Select a chord type by setting the ![](/images/screenshots/virtual-signal-Q.png) virtual signal in Arpeggiator's input. The *chord molder* will process **root-note**, **chord-type** and **inversion-key** into a **chord-mold** composed of 13 pitches.

Here are the 16 chord types included in the base Arpeggiator :

![](/images/screenshots/virtual-signal-Q.png) | Chord type | Base notes (root position on C)
----- | ----- | -----
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

*Note : the Arpeggiator doesn't only outputs the 3 or 4 notes showed in the Chord type table. Instead, it duplicates the 3 or 4 base notes in higher octaves multiple times to reach a total of 13 playable notes in the full chord. More Chord types can be added to the base Arpeggiator, see ???*

### Pattern & Offset
Select a pattern by setting the ![](/images/screenshots/virtual-signal-P.png) signal in Arpeggiator's input. The **pattern** determines which notes from the *chord mold* are to be played and when.

Select an offset by setting the ![](/images/screenshots/virtual-signal-O.png) signal in Arpeggiator's input. The **offset** offsets the arpeggio.

Here are the 16 included patterns in the base Arpeggiator :

![](/images/screenshots/virtual-signal-P.png) | Pattern length | 32 notes sample on Cmaj7 root position
----- | ----- | -----
1 | 4 | <img src="/images/patterns/arp-1.png" width="500" height="100" />
2 | 4 | <img src="/images/patterns/arp-2.png" width="500" height="100" />
3 | 4 | <img src="/images/patterns/arp-3.png" width="500" height="100" />
4 | 3 | <img src="/images/patterns/arp-4.png" width="500" height="100" />
5 | 3 | <img src="/images/patterns/arp-5.png" width="500" height="100" />
6 | 4 | <img src="/images/patterns/arp-6.png" width="500" height="100" />
7 | 4 | <img src="/images/patterns/arp-7.png" width="500" height="100" />
8 | 4 | <img src="/images/patterns/arp-8.png" width="500" height="100" />
9 | 6 | <img src="/images/patterns/arp-9.png" width="500" height="100" />
10| 8 | <img src="/images/patterns/arp-10.png" width="500" height="100" />
11| 8 | <img src="/images/patterns/arp-11.png" width="500" height="100" />
12| 8 | <img src="/images/patterns/arp-12.png" width="500" height="100" />
13| 16| <img src="/images/patterns/arp-13.png" width="500" height="100" />
14| 16| <img src="/images/patterns/arp-14.png" width="500" height="100" />
15| 16| <img src="/images/patterns/arp-15.png" width="500" height="100" />
16| 32| <img src="/images/patterns/arp-16.png" width="500" height="100" />

*Note : more patterns can be added to the base Arpeggiator, see ???*
