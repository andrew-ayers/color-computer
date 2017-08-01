Truchet Tiles
-------------

see [https://en.wikipedia.org/wiki/Truchet_tiles]

I was always kinda intrigued by the one-liner for the Commodore 64
which could generate a diagonal-style line maze pattern using two
opposing diagonal line characters in a random Truchet tile manner:

```
10 PRINT CHR$(205.5+RND(1));:GOTO 10
```

I wanted to have this kind of program on the Color Computer, but I
was pretty certain that it didn't have those characters in its
character set. But it did have the semi-graphics "diagonal pixel"
characters - so I tried that:

```
10 PRINT CHR$(246+(RND(2)-1)*3);:GOTO 10
```

Ok - so that sorta worked - but with the resolution so low, it doesn't
really look like a maze of any sorts. If you could keep track of
positioning and such, and make the "tiles" larger in some manner, that
might work - but I don't think you could fit it in a one-liner.

Then I recalled the "forward and backslash" characters (probably should
have tried those first?):

```
10 PRINT CHR$(47+(RND(2)-1)*45);:GOTO 10
```

Still - because of inter-line and inter-character spacing of regular
characters - it still doesn't look like anything. So, without a greater
development effort, a one-liner COLOR BASIC version was not going to
be possible.

Enter EXTENDED COLOR BASIC.

While you can't get an easy scrolling action like the original, you can
get an 8x8 tile to fill the high resolution (256x192x1) screen, then 
refresh and start again:

```
10 PMODE 4:SCREEN 1:PCLS
20 FOR Y=0 TO 191 STEP 8
30 FOR X=0 TO 255 STEP 8
40 T=(RND(2)-1)*7
50 LINE(X,Y+T)-(X+7,Y+7-T),PSET
60 NEXT
70 NEXT
80 GOTO 10
```

I think there is a lot of room to explore here. I think it still might be
possible to do a COLOR BASIC version using the semi-graphics tiles, but
with a bit more complex coding, perhaps doing a "look-up" using PEEK on
the text mode screen memory to look at prior character positions of the
previous line, and every other line draw the "extension" of the characters
above, such that you are drawing a 2x2 tile in effect - this would reduce
the number of tiles on the screen, but would likely make the maze more
visible.

The forward and backslash version is "out", because you can't change the
font of the VDG - but a CoCo 3 version should be possible; if a set of
characters isn't already a part of the font (I'm not sure, and it's been
a long while since I last played with my real CoCo 3), ones can be easily
created and POKE'd into memory. Because the characters are 8x8, they should
tile nicely.

Alternatively, the high-res graphic version for the CoCo 2 ECB mode could
be updated with little effort for the CoCo 3 Super-Hires graphics modes.
Also - maybe - with the GIME chip it might be possible to vertical scroll
the screen in some manner, shift things around, and do it fast enough
(likely with a bit of machine code involved) to make an "infinite scroll"
version with the graphics screen.

Well - all of this is something to play with...

Enjoy!

Andrew L. Ayers - August 1, 2017