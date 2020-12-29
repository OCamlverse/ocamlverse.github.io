---
tags: [ecosystem]
---

# Game Development

## Game-related
* [TSDL](http://erratique.ch/software/tsdl):
An OCaml module providing thin bindings to the `SDL` 2.0 library.
[SDL](https://www.libsdl.org/) provides a cross-platform interface for graphics,
sound, fonts, and game controller input.
This library uses `ctypes`,
and therefore requires less work to track changes to the C SDL libraries.
  * [tsdl-ttf](https://github.com/tokenrove/tsdl-ttf):
  Support for SDL's truetype font library.
  * [tsdl-mixer](https://github.com/tokenrove/tsdl-mixer):
  Support for the sound mixer component of TSDL.
  * [tsdl-image](https://github.com/tokenrove/tsdl-image):
  Support for the image-loading component of SDL.
* [OcamlSDL2](https://github.com/fccm/OCamlSDL2):
Bindings to the `SDL` 2.0 library using C files rather than `ctypes`.
Bindings (possibly incomplete) exist also for `SDL_image` and `SDL_mixer`,
but not for `SDL_ttf`.
* [OcamlSDL](http://ocamlsdl.sourceforge.net/home.html):
Bindings to the older `SDL` v1.2 suite,
including `SDL_image`, `SDL_ttf`, and `SDL_mixer`.

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
* [A blog about game development in OCaml](http://cranialburnout.blogspot.ca/)
