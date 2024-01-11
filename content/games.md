---
tags: [ecosystem]
---

# Game Development

## Game-related Libraries

* [TSDL](http://erratique.ch/software/tsdl):
An OCaml module providing thin bindings to the `SDL` 2.0 library.
[SDL](https://www.libsdl.org/) provides a cross-platform interface for graphics,
sound, fonts, and game controller input.
This library uses `ctypes`,
and therefore requires less work to track changes to the C SDL libraries.
  * [tsdl-ttf](https://github.com/sanette/tsdl-ttf):
  Support for SDL's truetype font library.
  * [tsdl-mixer](https://github.com/sanette/tsdl-mixer):
  Support for the sound mixer component of TSDL.
  * [tsdl-image](https://github.com/sanette/tsdl-image):
  Support for the image-loading component of SDL.
* [OCamlSDL2](https://github.com/fccm/OCamlSDL2):
Bindings to the `SDL` 2.0 library using the traditional C ffi rather than `ctypes`,
and therefore will produce warnings and errors if there are API changes.
Bindings (possibly incomplete) exist also for:
  * [OCamlSDL2_TTF](https://github.com/fccm/OCamlSDL2_TTF):
  Support for SDL2's truetype font library.
  * [OCamlSDL2_Mixer](https://github.com/fccm/OCamlSDL2_Mixer):
  Support for the sound mixer component of OCamlSDL2.
  * [OCamlSDL2_Image](https://github.com/fccm/OCamlSDL2_Image):
  Support for the image-loading component of SDL2.
  * [OCamlSDL2_Gfx](https://github.com/fccm/OCamlSDL2_Gfx):
  Support for graphics primitives for SDL2.
  * [OCamlSDL2_Net](https://github.com/fccm/OCamlSDL2_Net):
  Support for the network library for SDL2. (Currently only provides UPD.)
* [OCamlSDL](http://ocamlsdl.sourceforge.net/home.html):
Bindings to the older `SDL` v1.2 suite,
including `SDL_image`, `SDL_ttf`, `SDL_mixer` and `SDL_net`.

## Graphics
See [Graphics](graphics.md)

## Game Engines

* [ocaml-orx](https://github.com/orx/ocaml-orx):
Bindings to the [orx](https://orx-project.org/) game engine.
* [raylib](https://github.com/tjammer/raylib-ocaml):
Bindings to the [raylib](https://www.raylib.com/) game library.
* [Reprocessing](https://github.com/Schmavery/reprocessing):
A Reason 2d graphics library inspired by Processing.
*Requires `esy`*.
* [gocaml](https://github.com/CharlesAverill/gocaml/): A lightweight Go engine
* [camlcards](https://github.com/CharlesAverill/camlcards/): A card game engine

## Games

* [OCaml Invader](https://github.com/marmelab/ocaml-invader):
Hackathon Space Invader clone written in OCaml and OpenGL.
    * [Article](https://marmelab.com/blog/2020/02/21/ocaml-and-opengl-in-practice.html)
* [Shatter](https://github.com/hcarty/shatter):
Simple game written using the `Orx` engine.
* [Wanderers](https://github.com/a-nikolaev/wanderers):
A rogue-like written in OCaml using SDL.
* [WeiDU](https://github.com/WeiDUorg/weidu):
A program used to mod Infinity Engine games such as Baldur's Gate.
* [CamlBoy](https://github.com/linoscope/CAMLBOY/):
GameBoy emulator written purely in OCaml.
  * [Fascinating article](https://linoscope.github.io/writing-a-game-boy-emulator-in-ocaml/#gadts-to-the-rescue) on the emulator.
* [Flappy](https://github.com/rand00/flappy):
A demonstration of a Flappy-bird like game using FRP.
* [A blog about game development in OCaml](http://cranialburnout.blogspot.ca/)
* [Snóke](https://github.com/sanette/snoke), a snake game with new ideas

## Awesome Repositories

* [Awesome OCaml Gamedev](https://github.com/fccm/awesome-gamedev-ocaml)
