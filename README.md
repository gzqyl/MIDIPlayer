# R9MIDISequencer

[![Platform support](https://img.shields.io/badge/platform-ios-lightgrey.svg?style=flat-square)](https://github.com/glassonion1/R9MIDISequencer/blob/master/LICENSE.md)
[![License MIT](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](https://github.com/glassonion1/R9MIDISequencer/blob/master/LICENSE.md)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![CocoaPods Compatible](https://img.shields.io/cocoapods/v/ReSwift.svg?style=flat-square)](https://cocoapods.org/pods/R9MIDISequencer)

MIDI Sequencer for iOS on swift.

# Feature

## Sequencing

R9MIDISequencer now features a full MIDI Sequencer with EXS24 and SoundFont samplers which can be tied to your instruments for awesome, accurate playback.

## Example Code

Play note using the sampler:

```
import R9MIDISequencer

let url = Bundle.main.url(forResource: “Sound Font File Name”,
        withExtension: "sf2",
        subdirectory: "Sounds")
        
let sampler = Sampler(bankURL: url!, program: 0, bankMSB: 0x79, bankLSB: 0, channelNumber: 1)

// Play the note C
sampler.startNoteWithNumber(36)
// Play the note G
sampler.startNoteWithNumber(43)
```

Play MIDI file using the Sequencer:

```
let sequencer = Sequencer(sampler: sampler, enableLooping: true)

let midiUrl = Bundle.main.url(forResource: “MIDI File",
        withExtension: "mid")
sequencer.playWithMidiURL(midiUrl)
```

Callback from MIDI message

```
class GameScene: SKScene, MIDIMessageListener {
    override func didMoveToView(view: SKView) {
        
        ...Initialize sampler
        
        let sequencer = Sequencer(sampler: sampler, enableLooping: true)
        sequencer.addListener(self)
        
        ...Play MIDI
        
    }
    
    func midiNoteOn(note: UInt32, velocity: UInt32, channel: UInt32) {
        // Call back of note on message.
    }
    func midiNoteOff(note: UInt32, channel: UInt32) {
        // Call back of note off message.
    }
    func midiSequenceDidFinish() {
        // Call back of finish MIDI sequence.
    }
}
```

# Installation

## CocoaPods

You can install R9MIDISequencer via CocoaPods by adding it to your Podfile:

```
use_frameworks!

source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '9.0'

pod 'R9MIDISequencer'
```

## Carthage

You can install R9MIDISequencer via [Carthage](https://github.com/Carthage/Carthage) by adding the following line to your Cartfile:

```
github "glassonion1/R9MIDISequencer"
```

R9MIDISequencer is enabled the Bitcode.
