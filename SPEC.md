# Window Candy - Specification

## Project Overview
- **Project name**: Window Candy
- **Type**: Web-based synthesizer with authentic Windows 95 UI
- **Core functionality**: A fully playable polyphonic synthesizer with multiple component windows, styled to look exactly like Windows 95
- **Target users**: Musicians and retro UI enthusiasts

## UI/UX Specification

### Window System
All windows use Windows 95 styling:
- Title bar with gradient (dark blue to lighter blue)
- Window title (center), minimize/maximize/close buttons (right)
- Classic gray (#c0c0c0) window body with 3D beveled borders
- Inset content area with raised/beveled controls
- Windows are draggable and can overlap
- Overflow handling to prevent content spilling
- Auto-scroll for window bodies

### Color Palette
- Window title bar: #000080 to #1084d0 gradient
- Window body: #c0c0c0 (classic Windows 95 gray)
- Button face: #c0c0c0
- Button highlight: #ffffff
- Button shadow: #808080
- Button dark shadow: #000000
- Inset background: #ffffff
- Text: #000000
- Selected text: #ffffff on #000080

### Typography
- Font: "MS Sans Serif", Tahoma, sans-serif
- Font size: 11px for controls, 12px for titles

### Menu Bar (Main Window)
- **File**: New, Open, Save, Save As, Panic, Exit
- **Edit**: Undo, Redo, Copy Patch, Paste Patch, Init Pluck, Init Pad
- **Options**: MIDI Setup, Audio Settings, Full Screen
- **Help**: Help Topics, About Window Candy
- Keyboard shortcuts displayed in menus

### Taskbar
- Start button with Windows logo (⊞)
- Start menu with Programs, Panic, Keyboard Shortcuts, About, Shut Down
- Window task items for switching between windows
- Real-time clock display
- System tray with volume icon

### Desktop Icons
- Window Candy icon (opens main windows)
- My Computer icon (opens Filter, LFO, Pitch windows)
- Arpeggiator icon (opens Arpeggiator window)
- Scope icon (opens Oscilloscope window)
- Recycle Bin icon (Panic - all notes off)
- Click to open corresponding windows

### Status Bar
- Three-section display showing: Waveform, Octave, Voice count

### Windows Components

1. **Main Control Window** (Oscillator & Voice)
   - Menu bar (File, Edit, Options, Help)
   - Waveform selector (sine, square, sawtooth, triangle)
   - Octave buttons (+/-) with display
   - On-screen keyboard (C to C5)
   - Volume slider
   - Status bar with waveform, octave, polyphony

2. **ADSR Window**
   - Visual envelope display (canvas)
   - Horizontal sliders: Attack, Decay, Sustain, Release
   - Preset buttons: Pluck, Pad, Lead, Bass

3. **Filter Window**
   - Visual filter curve (canvas)
   - Filter type radio buttons: Low Pass, High Pass, Band Pass
   - Cutoff frequency slider
   - Resonance slider

4. **LFO Window**
   - Visual LFO waveform display (canvas)
   - Wave shape buttons: Sine, Square, Saw, Triangle
   - Rate slider
   - Depth slider
   - Destination checkboxes: Pitch, Filter

5. **Effects Window**
   - Reverb mix slider (default: 0%)
   - Delay: Mix, Time, Feedback sliders (default: 0%)

6. **Osc Mixer Window**
   - Osc 1 (Main): Level slider
   - Osc 2: Level, Detune, Octave sliders
   - Osc 3: Level, Detune sliders

7. **Pitch Window**
   - Pitch Bend: Range slider, bend display
   - Portamento: Time slider
   - Vibrato: Amount, Rate sliders

8. **Oscilloscope Window**
   - Real-time waveform display (canvas)
   - Time base slider
   - Trigger level slider
   - Freeze and Clear buttons

9. **Arpeggiator Window**
   - On/Off toggle checkbox
   - BPM slider (30-240)
   - Pattern: Up, Down, Up/Down, Down/Up, Random, Chord
   - Octave range slider (1-4)
   - Hold toggle

### Visual Effects
- 2px inset borders for panels
- Raised button effect with highlight/shadow
- Classic slider/thumb styling (horizontal and vertical)
- Checkboxes with classic checkbox icons
- Radio buttons with classic circle icons
- Title bar hover brightness effect
- Menu dropdowns with hover states

## Functionality Specification

### Audio Engine
- Web Audio API based
- Polyphonic (8 voices)
- 3 oscillators with individual level, detune, and octave controls
- Oscillator waveforms: sine, square, sawtooth, triangle
- ADSR envelope per voice
- Filter: Low Pass, High Pass, Band Pass with cutoff and resonance
- LFO modulating pitch and/or filter
- Reverb (convolver-based) and Delay effects
- Master compressor for dynamics
- Vibrato with rate and amount controls
- Portamento for glide between notes
- Pitch bend with configurable range
- Arpeggiator with multiple patterns and hold mode

### Interactions
- Click and drag to move windows
- Click notes on keyboard to play
- Keyboard play: A-L keys for white keys, W,E,T,Y,U for black keys
- Z/X keys for octave up/down
- Arrow keys for pitch bend
- Escape for panic (all notes off)
- ` key to toggle arpeggiator
- 1-4 keys for waveform selection
- Ctrl+S to save preset
- Ctrl+O to load preset
- Real-time slider adjustments
- Waveform selection changes sound immediately
- All controls affect audio in real-time

### Start Menu
- Toggle on Start button click
- Programs submenu with presets (two-column grid layout)
- Panic, Keyboard Shortcuts, About, Features Guide, Shut Down options
- Click outside to close
- Windows 95 header with flag logo

### Preset System
- 30 built-in Windows 95 themed presets:
  - System Sounds: Startup Chime, Shutdown Tone, Error Beep, Exclamation!, Question Mark, Clicky Button, Bubble Pop
  - Retro Game: Typewriter, 8-Bit Coin, Jump Sound, Laser Shot, Explosion, Power Up
  - Instruments: Piano 95, Organ Keys, Synth Bass, Brass Hit, Strings Swell, Whistle, Flute, Trombone
  - Percussion/Bells: Synth Bell, Marimba
  - Effects: Sci-Fi Sweep, Echo Pulse, Ambient Pad, Arpfunk, Retro Stab, Hard Lead, Soft Lead
- Programs menu opens upward
- Save Current... option to save custom presets
- Presets stored in localStorage

### Preset System
- Save/load presets using localStorage
- Stores all synth settings (waveform, ADSR, filter, LFO, effects, etc.)
- Prompt dialog for preset name entry

### Keyboard Shortcuts Dialog
- Modal dialog showing all available shortcuts
- Categories: Playing, Waveform, Other

### Edge Cases
- Handle audio context initialization on user interaction
- Resume suspended audio context on mobile
- Prevent audio clicks on note start/stop (linear ramps)
- Handle overlapping window dragging
- Touch support for mobile devices
- Visibility change handling (stop notes on tab switch)
- Error handling for Web Audio API not supported

## Acceptance Criteria
1. All windows render with authentic Windows 95 styling
2. Title bars have working close buttons (close individual windows)
3. Windows are draggable
4. Synth produces sound when notes are clicked
5. ADSR controls affect envelope
6. Filter controls work
7. LFO modulates sound
8. Effects audible
9. Multiple notes can play simultaneously
10. UI feels authentically Windows 95
11. Menu bar with keyboard shortcuts works
12. Start menu opens and functions
13. Arpeggiator sequences played notes
14. Oscilloscope displays real-time waveform
15. Touch support works on mobile devices
16. Preset save/load works
17. Keyboard shortcuts listed in Start menu
18. About dialog displays properly
19. Desktop icons open corresponding windows
20. Programs submenu shows presets in two columns
21. Initial minimized windows: Filter, LFO, Pitch, Scope, Arpeggiator
22. Initially open windows: Oscillator, ADSR, Effects, Osc Mixer