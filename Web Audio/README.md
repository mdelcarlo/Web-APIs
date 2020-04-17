# Web Audio
The Web Audio API provides a powerful and versatile system for controlling audio on the Web, allowing developers to choose audio sources, add effects to audio, create audio visualizations, apply spatial effects (such as panning) and much more.

## Usage
The Web Audio API involves handling audio operations inside an audio context, and has been designed to allow modular routing. Basic audio operations are performed with audio nodes, which are linked together to form an audio routing graph. Several sources — with different types of channel layout — are supported even within a single context. This modular design provides the flexibility to create complex audio functions with dynamic effects.

Audio nodes are linked into chains and simple webs by their inputs and outputs. They typically start with one or more sources. Sources provide arrays of sound intensities (samples) at very small timeslices, often tens of thousands of them per second. These could be either computed mathematically (such as OscillatorNode), or they can be recordings from sound/video files (like AudioBufferSourceNode and MediaElementAudioSourceNode) and audio streams (MediaStreamAudioSourceNode). In fact, sound files are just recordings of sound intensities themselves, which come in from microphones or electric instruments, and get mixed down into a single, complicated wave.

Outputs of these nodes could be linked to inputs of others, which mix or modify these streams of sound samples into different streams. A common modification is multiplying the samples by a value to make them louder or quieter (as is the case with GainNode). Once the sound has been sufficiently processed for the intended effect, it can be linked to the input of a destination (AudioContext.destination), which sends the sound to the speakers or headphones. This last connection is only necessary if the user is supposed to hear the audio.

A simple, typical workflow for web audio would look something like this:

1 - Create audio context

2 - Inside the context, create sources — such as ```<audio>```, oscillator, stream

3 - Create effects nodes, such as reverb, biquad filter, panner, compressor

4 - Choose final destination of audio, for example your system speakers

5 - Connect the sources up to the effects, and the effects to the destination.

![audio context](https://user-images.githubusercontent.com/20034230/79268779-68472d00-7eef-11ea-8e22-8e93e9fa95f4.png)

Timing is controlled with high precision and low latency, allowing developers to write code that responds accurately to events and is able to target specific samples, even at a high sample rate. So applications such as drum machines and sequencers are well within reach.

The Web Audio API also allows us to control how audio is spatialized. Using a system based on a source-listener model, it allows control of the panning model and deals with distance-induced attenuation induced by a moving source (or moving listener).

## Examples

#### Boombox

[<img width="813" alt="Captura de Pantalla 2020-04-17 a la(s) 07 50 29" src="https://user-images.githubusercontent.com/20034230/79500176-27325280-8080-11ea-990c-332baa095082.png">](https://jsfiddle.net/87wmed6h/25/)