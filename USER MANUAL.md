# Factorio Music Machine - User Manual

## Table of Contents
1. [Introduction](#introduction)
2. [Quick setup](#quick-setup)
3. [Components](#components)
    * [Clock](#clock)
    * [Score manager](#score-manager)
    * [Arpeggiator](#arpeggiator)

## <a name="introduction"></a>Introduction
The purpose of the Factorio Music Machine project is to make music creation in Factorio easier. It consists of multiple blueprints that work together as different components of a big customizable machine.

This user manual is meant to explain how to use each component to create music and how to expand them to suit your musical needs.

### Lexic & syntax rules
Virtual signals like <img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/> are represented by their ingame image. Non-image, text letters like A, F, G represent **music notes** following the <a href="https://en.wikipedia.org/wiki/Musical_note#12-tone_chromatic_scale" target="_blank">English notes naming convention</a>.

Some signals will be expressed as `variables` or grouped in `[arrays]` to improve this manual readability.

**Instrument** refers to the instrument selected in the programmable speaker GUI. **Component** refers a Music Machine part like the Arpeggiator.

## <a name="quick-setup"></a>Quick setup
- in Factorio, switch to editor mode by entering /editor in the console
- import and place the Clock blueprint and the Score manager blueprint in your game
- import and place any component base blueprint you want to try
- connect the Clock and the Score manager to the components inputs, with red wire and green wire respectively.
- manually set programs in the Score manager, see 

## <a name="components"></a>Components

### <a name="clock"></a>Clock
<img align="right" src="/images/screenshots/clock-overview.gif" alt="the Clock in its working state" width="240" height="240" />
The Clock is the  central component of the Factorio Music Machine. It outputs various signals which carry information about time structure (bars, beats, beat decomposition) to the other components.

4 variables are to be set in the input constant combinator (near the substation) :<br>
* <img src="/images/screenshots/virtual-signal-T.png" width="24" height="24"/> sets the `tempo` (expressed in beats per minute)
* <img src="https://wiki.factorio.com/images/thumb/Heavy_oil_barrel.png/48px-Heavy_oil_barrel.png" width="24" height="24"/> sets `beat-decomposition` : 4 for simple meter, 6 for compound meter (you can also set unusual decompositions like 5 or 11)
* <img src="https://wiki.factorio.com/images/thumb/Crude_oil_barrel.png/48px-Crude_oil_barrel.png" width="24" height="24"/> sets the `beats-per-bar` number
* <img src="https://wiki.factorio.com/images/thumb/Petroleum_gas_barrel.png/48px-Petroleum_gas_barrel.png" width="24" height="24"/> sets the length of the clock cycle in bars (this will basically define your tune length)

This constant combinator can also be used as a switch. When turned off, it effectively shuts down the Clock.

It outputs 11 different signals at once (referenced as `[clock]` in this manual), corresponding to various rhythmic informations :
* <img src="https://wiki.factorio.com/images/thumb/Automation_science_pack.png/48px-Automation_science_pack.png" width="24" height="24"/>  = 16th note count, goes from 1 to ... (end of clock cycle)
* <img src="https://wiki.factorio.com/images/thumb/Logistic_science_pack.png/48px-Logistic_science_pack.png" width="24" height="24"/> =  8th note count, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Military_science_pack.png/48px-Military_science_pack.png" width="24" height="24"/> =  beat count, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Chemical_science_pack.png/48px-Chemical_science_pack.png" width="24" height="24"/> =  group of 2 beats count, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Production_science_pack.png/48px-Production_science_pack.png" width="24" height="24"/> =  bar count, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Utility_science_pack.png/48px-Utility_science_pack.png" width="24" height="24"/> =  group of 2 bars count, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Space_science_pack.png/48px-Space_science_pack.png" width="24" height="24"/> =  group of 4 bars count, goes from 1 to ...
* <img src="https://wiki.factorio.com/images/thumb/Heavy_oil_barrel.png/48px-Heavy_oil_barrel.png" width="24" height="24"/> =  16th note count in one beat, goes from 1 to `beat-decomposition` over and over (eg. if there's 4 sixteenth notes per beat, it goes from 1 through 4)
* <img src="https://wiki.factorio.com/images/thumb/Empty_barrel.png/48px-Empty_barrel.png" width="24" height="24"/> =  beat count in group of 2 beats, goes from 1 to 2 over and over
* <img src="https://wiki.factorio.com/images/thumb/Crude_oil_barrel.png/48px-Crude_oil_barrel.png" width="24" height="24"/> =  beat count in one bar, goes from 1 to `beats-per-bar` over and over (eg. if there's 5 beats per bar, it goes from 1 through 5)
* <img src="https://wiki.factorio.com/images/thumb/Petroleum_gas_barrel.png/48px-Petroleum_gas_barrel.png" width="24" height="24"/> =  bar count in group of 4 bars, goes from 1 to 4 over and over

*This effectively means that programming complex tunes in the Factorio Music Machine should follow this time structure : x bars divided into y beats divided into z breves (or sixteenth notes)*

### <a name="score-manager"></a>Score manager
#### Overview
The Score manager sends instructions like `[arpeggio-ID]` via <img src="https://wiki.factorio.com/images/thumb/Green_wire.png/48px-Green_wire.png" width="24" height="24"/> to the different Music Machine components. Those instructions are referred here as *programs*.

The Score manager has 2 working modes :
- manual : set programs manually for each component, good for testing and playing around with components
- auto : write a series of programs to be sent following a timeline (`[clock]` signals)

#### Score timeline
The Score timeline is a *[x,y]* graph made from lights where *x* represent time measured in bars (<img src="https://wiki.factorio.com/images/thumb/Production_science_pack.png/48px-Production_science_pack.png" width="24" height="24"/>) and each *y* line represent one component.

Each light has 3 possible states :
* light off means that no program is set for that bar
* <img src="/images/misc/blue.png" width="20" height="16" />blue light means that a program is set for that bar # but not actually being sent
* <img src="/images/misc/cyan.png" width="20" height="16" /> cyan light means a `[program]` is being sent to the components

#### Expanding the Timeline

### <a name="arpeggiator"></a>Arpeggiator
#### Overview
The Arpeggiator generates and plays arpeggios when it receives `[arpeggio-ID]` and `[clock]` signals .

The Arpeggiator is mainly divided into 5 parts :

![](/images/screenshots/arpeggiator-overview.png)
<img src="/images/misc/yellow.png" width="20" height="16" /> Speakers : produce the sound from the `arpeggio` signal<br>
<img src="/images/misc/red.png" width="20" height="16" /> Chord inverter : send `[inversion]` signals to the Chord library when `root-note` increases to make chord changes less brutal<br>
<img src="/images/misc/magenta.png" width="20" height="16" /> Chord library : processes `root-note`, `chord-type` and `[inversion]` signals and outputs `[chord-mold]` (13 unique notes/signals)<br>
<img src="/images/misc/green.png" width="20" height="16" /> Loop maker : generates `arpeggio-loop` (<img src="https://wiki.factorio.com/images/thumb/Iron_gear_wheel.png/48px-Iron_gear_wheel.png" width="20" height="16" /> signal) from `pattern-length` and `[clock]` signals<br>
<img src="/images/misc/cyan.png" width="20" height="16" /> Pattern library : receive `pattern`, send back `pattern-length` to the Loop maker, and generates the final `arpeggio` signal from `arpeggio-loop` and `[chord-mold]`

#### Circuit network input

`[clock]` is sent by the [**Clock**](#clock) via <img src="https://wiki.factorio.com/images/thumb/Red_wire.png/48px-Red_wire.png" width="24" height="24"/>

`[arpeggio-ID]` is sent by the [**Score manager**](#Score-manager) via <img src="https://wiki.factorio.com/images/thumb/Green_wire.png/48px-Green_wire.png" width="24" height="24"/>.

Both wires <img src="https://wiki.factorio.com/images/thumb/Red_wire.png/48px-Red_wire.png" width="24" height="24"/><img src="https://wiki.factorio.com/images/thumb/Green_wire.png/48px-Green_wire.png" width="24" height="24"/> need to be connected to any of the 2 big power poles near the Speakers.

`[arpeggio-ID]` is defined by 4 signals (see <a href="https://en.wikipedia.org/wiki/Chord_(music)" target="_blank">Chord</a>) :
* <img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/> sets `root-note`
* <img src="/images/screenshots/virtual-signal-Q.png" width="24" height="24"/> sets `chord-type`
* <img src="/images/screenshots/virtual-signal-P.png" width="24" height="24"/> sets the arpeggio `pattern`
* <img src="/images/screenshots/virtual-signal-O.png" width="24" height="24"/> sets an `offset` for the arpeggio pattern

#### Root note
Select `root-note` by setting <img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/> in Arpeggiator's input. It follows the chromatic scale starting from A, meaning that 1 = A ; 2 = A# ; 3 = B ; 4 = C etc...

You can go higher than 12 ; setting <img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/> to 13, 25 or 37 will also set the `root-note` to A (see <a href="https://en.wikipedia.org/wiki/Chromatic_scale" target="_blank">Chromatic scale</a>). You can also go lower than 0 but going too low will result in out of range, silent notes from the Speakers.

*Note : the Arpeggiator has an automated Chord inverter. It outputs `[inversion]` signals depending on `root-note` value, in order to provide better voice progressions when changing chords. If you're not happy with the chord inversion you get with a given root note, just add or substract 12 to <img src="/images/screenshots/virtual-signal-R.png" width="24" height="24"/> and you'll get the same chord in a higher or lower inversion.*

#### Chord type
Select `chord-type` by setting <img src="/images/screenshots/virtual-signal-Q.png" width="24" height="24"/> in Arpeggiator's input. The chord type will determine 12 pitches starting from the `root-note`, all 13 unique pitches will form `[chord-mold]` signals.

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

*Note : the Chord library doesn't only outputs the 3 or 4 notes showed in the Chord type table. Instead, it duplicates the 3 or 4 base notes in higher octaves to reach a total of 13 chord notes including the root note. More Chord types can be added to the Chord library, see [Adding new chords](#adding-new-chords).*

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

*Note : more patterns can be added to the Pattern library, see [Adding new patterns](#adding-new-patterns).*

#### Offset

Select `offset` by setting <img src="/images/screenshots/virtual-signal-O.png" width="24" height="24"/> in Arpeggiator's input. The offset will delay or advance the pattern by given amount of breves (sixteenth notes).

#### <a name="adding-new-chords"></a>Adding new chords
To add new chords to the Chord library, you need to place the arpeggiator-chord-library-extension blueprint. Placing this blueprint adds 8 new `chord-type` entries in the Chord-library, referenced as 17-24.

#### <a name="adding-new-patterns"></a>Adding new patterns
To add new patterns to the Pattern library, you need to place the arpeggiator-pattern-library-extension blueprint.
