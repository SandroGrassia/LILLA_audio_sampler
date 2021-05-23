![Lilla](/pics/logo.jpg)

Facebook: https://www.facebook.com/Lilla.audio.sampler

![Lilla](/pics/D3.jpg)

![Lilla](/pics/D9.jpg)


Overview
-----------------------

![Lilla](/pics/D11.jpg)

__LILLA__ is a polyphonic (__16 voices__) multitimbral and multi-midi audio sampler, based on __Teensy 4.1__. LILLA stores audio samples (__16 bit__, __44.1kHz__) in a flash memory (__32MB__), and plays them applying various playing mode, adding an ADSR envelope, changing length and pitch; LILLA allows the sound editing (e.g. slicing) during the performance without interruption, includes virtual multimode VCF, LFO, Delay modules together with Resolution and Downsampling effects; LILLA supports midi Pitch-bend, Vibrato and After Touch, besides can adopt any midi Control-Change to adjust inner parameters. Up to 8 parts can be used in the performance, with multi-layered distribution and also multi-midi control; the internal memory can store 25 presets (Session) and 90 parts.

Hardware
-----------------------
LILLA includes:

 devices/ICs:
 - n.1 Teensy 4.1 (ARM Cortex-M7 at 600 MHz, 1MB RAM; Flash memory: 8MB; EEPROM: 4284 bytes)
 - n.1 Teensy Audio Adaptor Rev.D
 - n.1 W25Q256FV (32Mbyte serial flash memory)
 - n.3 CD74HC4067 (16-channel analog multiplexer)
 - n.1 HCPL260 (optocoupler)

 UIs:
 - n.1 128x160 TFT color display
 - n.15 Rotary Encoders with pushbutton
 - n.9 Pushbuttons

 i/o interfaces:
 - micro-USB type-B (5V power supply - programming)
 - MIDI in (5-pin DIN)
 - line output (3.5mm stereo)
 - Headphones (3.5mm stereo)
 - micro-SD socket


 Dimensions
 -----------------------
252mm x 102mm x 38mm (LxWxH)


Audio files and presets
-----------------------
LILLA uses 44.1kHz 16bit mono .RAW (header-less) audio files, imported from micro-SD card.


Setups: Sessions and Sounds
 -----------------------
LILLA can store up to 25 setups called "Sessions"; a Session can include up to 8 parts (Sounds) that can be layered on each other.

 ![Performance page](/pics/D2.jpg)

 LILLA can store up to 90 Sounds; each Sound is described by these attributes:
 - midi channel
 - audio file
 - interval to be played: from 100 samples to full file length
 - play mode: once forward, once reverse, forward-loop, reverse-loop, bidirectional-loop
 - anti-click applied in case of forward-loop and reverse-loop
 - fine pitch
 - gain
 - L-R pan
 - ADSR parameters
 - ADSR attack ramp: fast, slow
 - root-key
 - keyboard allocation (first key - last key)
 - pitch-bend and effects shield (on/off)
 - VCF parameters

![Sound editing page](/pics/D5.jpg)


Sounds layering and multi-timbral
 -----------------------
This picture shows an example of a Session using 5 midi channels and 8 Sounds
![Session example](/pics/Sounds.jpg)


Anti-click feature
-----------------------
For forward-loop and reverse-loop play modes, LILLA offers an anti-click feature, obtained applying cross fade-in/fade-out to the beginning and the end of the snippet played.


 Effects and synth modules
 -----------------------
LILLA includes:
 - resolution: reduces the bit-resolution (16bit -> 1bit)
 - downsampling: reduces the sampling frequency (44.1KHz -> 344Hz)
 - n.16 multimode virtual VCF + LFO (one per voice)
 - n.2 (one per output channel) delay/reverb (delay modulated by a local LFO or by the incoming signal)
 - low-pass 12dB/oct filter

![Instrument Filter Page](/pics/D20.jpg)

![Player VCF LFO](/pics/D16.jpg)

![Delay Page](/pics/D14.jpg)

![Router LFO Delay Lowpass](/pics/D15.jpg)


 Tuning Tone tool
 -----------------------
 LILLA includes a sinusoidal oscillator (middle C: 261.6Hz) overlaid to other sounds.  


 Other features
 -----------------------
 - solo: temporary assigns a single Sound to the whole keyboard
 - midi pitch-bend support
 - midi vibrato support
 - midi aftertouch support


 Settings
 -----------------------
 ![Settings page](/pics/D6.jpg)

 LILLA allows the following settings:
 - first octave number (-2, -1, 0)
 - CC control: use Control Change messages to control some functionalities

 ![CC controllers](/pics/D7.jpg)

 - optimization: maximize polyphony or pitch-extension
 - MIDI Velocity response: 2 curves / 8 adjustment points

 ![Velocity response page](/pics/D8.jpg)


 Monitor
 -----------------------
 LILLA includes a MIDI monitor.

 ![MIDI monitor](/pics/D10.jpg)


 Live Sound Editing
 -----------------------
Sounds and Sessions are created by the user and edit using the context menu. LILLA's code is deeply focused on __live sound editing__: file slicing, root key, keyboard allocation, playing mode, anti-click window and so on.... All parameters can be modified while playing without introducing any "click" or lag: for all critical operations old and new waveforms are cross-mixed.


 Settings backup/restore
 -----------------------
 All settings are stored in the Teensy EEPROM memory; LILLA allows to backup/restore all settings using a micro-SD card.


 LILLA and Teensy Audio library
 -----------------------
 LILLA's firmware widely uses Teensy libraries, adding its specific library (fully published and documented but not integrated in Teensy ecosystem). Some relevant and specific LILLA objects are:
 - Lilla_Player: 16 Lilla_Player objects read audio samples from memory areas, apply ADSR, downsampling and resolution filters, perform cross-mix and L/R panning; among all procedures, these objects host the most CPU-intensive and time-demanding processes;
 - Lilla_Trigger: 2 instances of this pseudo audio-object call Lilla_midi_reader 2 times per cycle (2.9ms);
 - Lilla_Midi_Reader: this not-audio-object guarantees maximum precedence to midi read and play processes, above all other processes; Midi_Reader object reads incoming midi messages and UIs requests and acts as centralized critical parameters change-point; besides Midi_Reader acts as orchestrator for the 16 voices, 16 VCF/LFOs, and the couple of Delay/LFOs providing them all metadata, checking their state, and arranging their activity:

 ![timing good](/pics/TIMING_GOOD.JPG)


 Credits
-----------------------
- Napo Naps (C++ consulting & encouragement)
- Stefano Spada (functionalities, project evolution)
- Thomas Spada (functionalities, tests & usability)
- Stefano Tonti (logo)
