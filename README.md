# caddraw

CadDraw is a work in progrss to create a PB-700 plotter magic drawing program.

The ultimate goal is to produce a program that can be run on a PB-700 with a FA-10 plotter, and produce an image from an input text.

There are a few challenges, but all of them can be overcome.

The objective is to create such images, it is understood that it will absolutely not be practical at all.

# Architecture

The pb-700 will need to be connected to a linux PC by a two-way audio transmition, with the PC acting like a tape recorder. (Note: it should be possible to save drawing programs on tape).

The first operation will be to execute a ``LOAD,A`` on the PB-700, and start the server on the PC.

The server will serve a BASIC program doing the prompting on the machine, and listen to the audio input.

User will enter its short prompt, and the basic program will use a ``PUT A$`` to write it to the PC. It will then use a ``CHAIN,A`` to execute the next basic program read.

The PC will read and decode the input, and use midjourney to generate a suitable image, with the following prompt:

``<<SOMETHING>> black and white line art constant thickness simple children coloring book``

The top left resulting image will the be transformed into a series of BASIC programs that will draw that exact shape.

The basic programs will then be encoded and played back to the computer. Each basic program but the last end up with a ``CHAIN,A`` command. As the server goes back to the main loop, it will serve the initial basic program, enabling the slighlt older user to perform another drawing.

# Challenges

* Fixing my CA-10
* Writing programs to the pb-700
* Decoding input from pb-700
* Generating the basic instructions
* Interfacing with midjourney

# Architecture

While it would be better to have a nice self-contained software, the current end result is probably going to be a mix of bash shell scripts, python command lines, ``casutil`` commands, and various linux specific commands, meaning it will be quite fragile.

# Challenge 1: Fixing my CA-10s

*In Progress*

# Challenge 2: Writing programs to the pb-700

The following ``casutil``` commands can write a program to the PB-700

```
	casutil/linux/bas850 -b prog.bas prog.bin
	casutil/linux/wave850 -b prog.bin prog.wav
    play prog.wav
```

# Challenge 3: Decoding input from pb-700

*In Progress*

# Challenge 4: Generating the basic instructions

The test.py program does the generation from the top-left quarter of a midjourney supplied 2048x2048 image.

# Challenge 5: Interfacing with midjourney

It seems that the "midjourney API" is discord. Which is quite a WTF. *In Progress*.
