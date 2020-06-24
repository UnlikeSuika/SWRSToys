# SWRSToys [![builds.sr.ht status](https://builds.sr.ht/~delthas/SWRStoys.svg)](https://builds.sr.ht/~delthas/SWRStoys?)

A modding framework for Touhou Hisoutensoku (12.3).

This repository was originally created from the original SWRSToys release by *Anonymous Coward* with the following goals:
- make sure the source code for SWRSToys is easy to find
- make a repository of all released modules and their source code, including ones that were not made by Anonymous Coward
- have up-to-date headers of the latest reverse-engineered addresses from the game, updated as new people find more addresses
- set up a CI for easy, reproducible builds and deployment of the latest release of SWRSToys.

Most of the code was not written by delthas:
- this repository (and most of this code) is forked off a source archive of SWRSToys, made by *Anonymous Coward*
- *Shinki* and *PC_volt* made ReplayInputView+
- *DPhoenix* made UPnPNat
- *fishshapedfish* made DPadFix
- delthas made all the plumbing: adding CMake, CI, formatting, ...

If you have made an SWRSToys module, do contact me either on GitHub or with a PM on Discord (`cc#6439`) so we can add it here, with proper credits!

*Due to a subtle issue with the CI, the ZIP packages the original SWRSToys DLL file (which is in `bin/`) rather than the one compiled during the CI build. All other modules in the ZIP are the ones compiled from the CI though.*

## Using

- Download the **[latest release](https://delthas.fr/swrstoys.zip)** and extract it in your game folder.
- Open SWRSToys.ini in Notepad and enable some modules by deleting their `;`, then save the file.
- Modify the `.ini` configuration files of modules you enabled (in the `modules/` folder)
- Run the game as usual.

## Modules

### BGMChanger

**Replace some of the game BGMs.**

*The only supported format is OGG Vorbis.*

### DPadFix

**Map the joystick DPad and trigger buttons to game inputs.**

### MemoryPatch

**Do some misceallenous patches to the game, such as disallowing spectating by default.**

Edit MemoryPatch.ini to enable/disable options.

Available patches:

- 16bitsColor: Enable 16 bit color.

- InputFreedom: Allow gamepad input even when the window is not active.

- DefaultDenyWatch: Disallow spectating by default.

- DefaultDenyBattle: Spectate by default.

- AllowMultiInstance: Allow running multiple instances of the game at once.

- DisableWeatherEffect: Disable all weather effects.

- AlwaysRandomMusic: always play random music regardless of stage choice

- NativeDPadFix: Alternative DPad fix without dinput8 hooking, but no circle pad support and XInput only.

### NetBattleCounter

**Display the number of consecutive online matches you play, and optionally play specific sounds on consecutive games played.**

### NetBellChanger

**Change the game start bell sound for online matches.**

### NetProfileView

**Display profile name for players in a game with a specific formatting (color, font, ...) (spectating and/or playing).**

### ReplayDnD

**Drag and drop a replay file to the game executable file to watch it immediately.**

*Dragging a replay to a running game window does not work; you need to drag it to the game exacutable file in Windows Explorer.*

### ReplayInputView *(deprecated)*

*This module is now deprecated, use ReplayInputView+ instead.*

**Display keystrokes in game replays in real time.**

*The replay speed can also be changed with hotkeys: F10 speeds up; F11 slows down; F12 returns to original speed; F8 and F9 cycle through different game inputs display, for the left and right player respectively.*

*This module does not have a configuration file.*

### ReplayInputView+

**Display keystrokes in game replays in real time, as well as hitboxes, ...**

*The replay speed can also be changed with configurable hotkeys: by default F10 speeds up; F9 slows down; F11 pauses and unpauses the game; F12 steps a single frame forward; F4 toggles hitboxes display; F6 displays additional debug information; F7 cycles through different game inputs display.*

### UPnPNat

**Automatically forward your ports every time the game runs.**

*This mod uses the UPnP NAT technology, which lets applications automatically request a port forwarding without user intervention. This technology is known to be disabled by default on most routers and might therefore not work for everyone.*

### WindowedFullscreen

**Make the game window fullscreen, but without stretching and with fast alt+tab.**

*This module does not have a configuration file, and is not compatible with SokuEngine.*

### WindowResizer

**Make the game window resizable.**

## Making a module

- Make a new folder in `modules/`. You can copy an existing module and adapt it.
- Edit the root `CMakeLists.txt` file accordingly.
- Your module will automatically be injected.

## Building

Install Visual Studio (or CMake and the Visual C++ Build Tools). 

If on VS2015 (or older?): Open a commmand prompt and enter `git submodule init && git submodule update && cmake .`

If on something newer: Import the directory into Visual Studio, it will be recognized automatically.

MinGW and Cygwin are not supported (`__thiscall` is needed in order to be compatible with the base game).

After building, run the install target, which will create an `install` folder with all the built files.

## License

- Files in `include/directx/` are licensed according to their license header
- `lib/dinput8.dll` is a pre-compiled archive copyrighted by Microsoft
- All other files are licensed according to the `LICENSE` file
