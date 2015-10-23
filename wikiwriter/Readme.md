Wikiwriter
==========
The Wikiwriter turns a Wikireader into a desktop writing prompt generator, capable of creating inspiring ideas for overall works, characters and settings.

![start screen](https://raw.githubusercontent.com/JohnEarnest/Wikireader-Adventures/master/wikiwriter/screenshots/writerstart.png) ![example story form](https://raw.githubusercontent.com/JohnEarnest/Wikireader-Adventures/master/wikiwriter/screenshots/writerexample.png)

To generate random ideas, this application loads a series of text files with "chunks" and assembles them together much like a madlib. The `rtable` defining word handles this data loading process and tracks how many of each chunk type exists in the provided text files. The word `any` can then pick one of these elements and leave a Forth string on the stack.

Random numbers are generated by a crude but sufficiently effective linear-congruential generator. The seed is written to the MicroSD card after every random number is picked, ensuring that if the device is powered off it will not repeat earlier selections. These constant writes to the MicroSD card may ultimately limit the lifespan of the device, but with casual use it shouldn't pose problems.

This program makes use of several full-screen bitmaps. Rather than write a decoder for a complex image format like PNG or even BMP, I made a Java program (`ImageConverter.java`) which prepares monochrome images in any common format in the raw format used by the Wikireader's memory-mapped display. The word `blit-image` can then very easily load a file from disk directly into this framebuffer. The framebuffer is padded to 32 bytes per scanline, and this is taken into account by the utility. I was pleasantly surprised at the speed of this routine with no particular effort to optimize its performance- it may well be possible to use a modified form of this technique to produce smooth animation.