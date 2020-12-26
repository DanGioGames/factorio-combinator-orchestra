# Factorio Music Machine - User Manual

## Table of Contents
1. [Introduction](#introduction)
2. [Components](#components)
    * [Clock](#clock)
    * [Arpeggiator](#arpeggiator)

## <a name="introduction"></a>Introduction
The purpose of the Factorio Music Machine project is to make music creation in Factorio easier. It consists of multiple blueprints that work together as different components/instruments of a big customizable machine.

This user manual is meant to explain how to use each component to create music and how to expand them to suit your musical needs.

### Syntax rules
Virtual signals like <img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/> are represented by their ingame image. Non-image, text letters like A, F, G represent **music notes** following the [English notes naming convention](https://en.wikipedia.org/wiki/Musical_note#12-tone_chromatic_scale).

## <a name="components"></a>Components

### <a name="clock"></a>Clock
<img align="right" src="/images/screenshots/clock-overview.gif" alt="the Clock in its working state" width="240" height="240" />
The Clock is a key component of the Factorio Music Machine. It outputs various signals which command all the instruments of the Music Machine.


4 variables are to be set in the constant combinator near the substation :<br>
* <img src="/images/screenshots/virtual-signal-T.png" width="24" height="24"/> sets the `tempo` (expressed in beats per minute)
* <img src="https://wiki.factorio.com/images/thumb/Heavy_oil_barrel.png/48px-Heavy_oil_barrel.png" width="24" height="24"/> sets `beat-decomposition` :  2 or 4 for simple meter, 3 or 6 for compound meter (you can also set weird decompositions like 5 or 11 if you want)
* <img src="https://wiki.factorio.com/images/thumb/Crude_oil_barrel.png/48px-Crude_oil_barrel.png" width="24" height="24"/> sets the `beats-per-bar` number
* <img src="https://wiki.factorio.com/images/thumb/Petroleum_gas_barrel.png/48px-Petroleum_gas_barrel.png" width="24" height="24"/> sets the length of the clock cycle in bars (this will basically define your tune length)

This constant combinator can also be used as a switch. When turned off, it effectively shuts down the Clock.

The Clock outputs 11 different signals at once, corresponding to various rhythmic values :
* <img src="https://wiki.factorio.com/images/thumb/Automation_science_pack.png/48px-Automation_science_pack.png" width="24" height="24"/> =  16th notes, goes from 1 to ... (end of clock cycle)
* <img src="https://wiki.factorio.com/images/thumb/Logistic_science_pack.png/48px-Logistic_science_pack.png" width="24" height="24"/> =  8th notes, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Military_science_pack.png/48px-Military_science_pack.png" width="24" height="24"/> =  beats, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Chemical_science_pack.png/48px-Chemical_science_pack.png" width="24" height="24"/> =  groups of 2 beats, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Production_science_pack.png/48px-Production_science_pack.png" width="24" height="24"/> =  bars, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Utility_science_pack.png/48px-Utility_science_pack.png" width="24" height="24"/> =  groups of 2 bars, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Space_science_pack.png/48px-Space_science_pack.png" width="24" height="24"/> =  groups of 4 bars, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Heavy_oil_barrel.png/48px-Heavy_oil_barrel.png" width="24" height="24"/> =  16th notes, goes from 1 to `beat-decomposition` over and over (eg. if there's 4 sixteenth notes per beat, it goes from 1 through 4)
* <img src="https://wiki.factorio.com/images/thumb/Empty_barrel.png/48px-Empty_barrel.png" width="24" height="24"/> =  beats, goes from 1 to 2 over and over
* <img src="https://wiki.factorio.com/images/thumb/Crude_oil_barrel.png/48px-Crude_oil_barrel.png" width="24" height="24"/> =  beats, goes from 1 to `beats-per-bar` over and over (eg. if there's 5 beats per bar, it goes from 1 through 5)
* <img src="https://wiki.factorio.com/images/thumb/Petroleum_gas_barrel.png/48px-Petroleum_gas_barrel.png" width="24" height="24"/> =  bars, goes from 1 to 4 over and over


### <a name="arpeggiator"></a>Arpeggiator
#### Overview
The Arpeggiator is meant to generate and play arpeggios, given 4 circuit network input signals (see
[Chord](https://en.wikipedia.org/wiki/Chord_(music))) :
* <img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/> sets `root-note`
* <img src="/images/screenshots/virtual-signal-Q.png" width="24" height="24"/> sets `chord-type`
* <img src="/images/screenshots/virtual-signal-P.png" width="24" height="24"/> sets the arpeggio `pattern`
* <img src="/images/screenshots/virtual-signal-O.png" width="24" height="24"/> sets an `offset` for the arpeggio pattern

<img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/><img src="/images/screenshots/virtual-signal-Q.png" width="24" height="24"/><img src="/images/screenshots/virtual-signal-P.png" width="24" height="24"/><img src="/images/screenshots/virtual-signal-O.png" width="24" height="24"/> input can be automated via the Score, or set manually via a constant combinator. Although, it needs to be connected to the [Clock](#clock) to work.

The Arpeggiator is mainly divided into 5 parts :

![](/images/screenshots/arpeggiator-overview.png)
<img src="/images/misc/yellow.png" width="20" height="16" /> Speakers : produce the sound from the `arpeggio` signal<br>
<img src="/images/misc/red.png" width="20" height="16" /> Chord inverter : send various inversion signals to the Chord bank when `root-note` increases to make chord changes less brutal<br>
<img src="/images/misc/magenta.png" width="20" height="16" /> Chord bank : processes `root-note`, `chord-type` and inversion signals and outputs 13 unique notes/signals (`chord-mold`)<br>
<img src="/images/misc/green.png" width="20" height="16" /> Loop maker : generates `arpeggio-loop` signal from active `pattern-length` & various Clock signals<br>
<img src="/images/misc/cyan.png" width="20" height="16" /> Pattern bank : generates the final `arpeggio` signal from `arpeggio-loop` and `chord-mold`, in the form of a varying signal sent to the Speakers

#### Root note
Select `root-note` by setting <img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/> in Arpeggiator's input. It follows the chromatic scale starting from A, meaning that 1 = A ; 2 = A# ; 3 = B ; 4 = C etc...

You can go higher than 12 ; setting <img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/> to 13, 25 or 37 will also set the `root-note` to A (see [Chromatic scale](https://en.wikipedia.org/wiki/Chromatic_scale)). You can also go lower than 0 but going too low will result in out of range, silent notes by the Speakers.

*Note : the Arpeggiator has an automated Chord inverter. It outputs inversion signals depending on `root-note` value, in order to provide better voice progressions when changing chords. If you're not happy with the chord inversion you get with a given root note, just add or substract 12 to <img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/> and you'll get the same chord in a higher or lower inversion.*

#### Chord type
Select `chord-type` by setting <img src="/images/screenshots/virtual-signal-Q.png" width="24" height="24"/> in Arpeggiator's input. The chord type will determine the pitch of 12 unique `chord-mold` notes, relative to the `root-note`.

Here are the 16 chord types included in the base Arpeggiator :

![](/images/screenshots/virtual-signal-Q.png) | Chord type | Base notes (root position on C)
----- | ----- | -----
1 | Major triad | <img src="/images/chords/maj.png" width="250" height="75" />
2 | Minor triad | <img src="/images/chords/min.png" width="250" height="75" />
3 | Diminished triad | <img src="/images/chords/dim.png" width="250" height="75" />
4 | Augmented triad | <img src="/images/chords/aug.png" width="250" height="75" />
5 | Major seventh | <img src="/images/chords/maj7.png" width="250" height="75" />
6 | Minor seventh | <img src="/images/chords/min7.png" width="250" height="75" />
7 | Dominant seventh | <img src="/images/chords/7.png" width="250" height="75" />
8 | Half-diminished seventh | <img src="/images/chords/min7b5.png" width="250" height="75" />
9 | Diminished seventh | <img src="/images/chords/dim7.png" width="250" height="75" />
10| Rootless altered seventh | <img src="/images/chords/7alt.png" width="250" height="75" />
11| Dominant seventh suspended fourth | <img src="/images/chords/7sus4.png" width="250" height="75" />
12| Dominant seventh suspended second | <img src="/images/chords/7sus2.png" width="250" height="75" />
13| Minor major seventh | <img src="/images/chords/minmaj7.png" width="250" height="75" />
14| Augmented major seventh | <img src="/images/chords/augmaj7.png" width="250" height="75" />
15| Major add second | <img src="/images/chords/majadd2.png" width="250" height="75" />
16| Minor add second | <img src="/images/chords/minadd2.png" width="250" height="75" />

*Note : the Chord bank doesn't only outputs the 3 or 4 notes showed in the Chord type table. Instead, it duplicates the 3 or 4 base notes in higher octaves to reach a total of 13 chord notes including the root note. More Chord types can be added to the Chord bank, see [Adding new chords](#adding-new-chords).*

#### Pattern
Select `pattern` by setting <img src="/images/screenshots/virtual-signal-P.png" width="24" height="24"/> in Arpeggiator's input. The pattern will determine which of the 13 `chord-mold` notes are played and when.

Here are the 16 included patterns in the base Arpeggiator :

![](/images/screenshots/virtual-signal-P.png) | Pattern length | 32 notes sample on Cmaj root position
----- | ----- | -----
1 | 4 | <img src="/images/patterns/arp-1.png" width="375" height="75" />
2 | 4 | <img src="/images/patterns/arp-2.png" width="375" height="75" />
3 | 4 | <img src="/images/patterns/arp-3.png" width="375" height="75" />
4 | 3 | <img src="/images/patterns/arp-4.png" width="375" height="75" />
5 | 3 | <img src="/images/patterns/arp-5.png" width="375" height="75" />
6 | 4 | <img src="/images/patterns/arp-6.png" width="375" height="75" />
7 | 4 | <img src="/images/patterns/arp-7.png" width="375" height="75" />
8 | 4 | <img src="/images/patterns/arp-8.png" width="375" height="75" />
9 | 6 | <img src="/images/patterns/arp-9.png" width="375" height="75" />
10| 8 | <img src="/images/patterns/arp-10.png" width="375" height="75" />
11| 8 | <img src="/images/patterns/arp-11.png" width="375" height="75" />
12| 8 | <img src="/images/patterns/arp-12.png" width="375" height="75" />
13| 16| <img src="/images/patterns/arp-13.png" width="375" height="75" />
14| 16| <img src="/images/patterns/arp-14.png" width="375" height="75" />
15| 16| <img src="/images/patterns/arp-15.png" width="375" height="75" />
16| 32| <img src="/images/patterns/arp-16.png" width="375" height="75" />

*Note : more patterns can be added to the Pattern bank, see [Adding new patterns](#adding-new-patterns).*

#### Offset

Select `offset` by setting <img src="/images/screenshots/virtual-signal-O.png" width="24" height="24"/> in Arpeggiator's input. The offset will delay or advance the pattern by given amount of breves (sixteenth notes).

#### <a name="adding-new-chords"></a>Adding new chords

#### <a name="adding-new-patterns"></a>Adding new patterns
