# Drawing primes

## Background

Inspired by the graphics used in [Prime Climb](https://mathforlove.com/games/prime-climb/), specifically the [colouring sheet](https://mathforlove.com/lesson/prime-climb-color-chart/), I did some playing around with LuaTeX and made this. It uses Lua to generate TikZ code in a LuaTeX document. Build using lualatex.

The code takes a number `target` and draws and coloured circles for numbers up to `target`. Primes are coloured different colours (see caveat below) and then composite numbers are divided into sections coloured using the colours of their prime factors. 

## Instructions

Either 
1. set `target` and let the next line set `rowlength` to be the square root of `target` rounded down, for a rougly-square grid; or,
2. set `rowlength` and set `target` to be some multiple of `rowlength`, for example to create a rectangle grid of fixed row length.

## Issues

### Colours

A bunch of colours are hard-coded into a list which are used to colour the primes in sequence. Issues with this:
1. there are fewer colours than there are prime numbers (hard to fix);
2. colours could be checked to be more distinct and in a better order, so adjacent primes are definitely differently-coloured. 

A partial-fix for 1. is that when the list of colours is exhausted, the code uses `runoutofcolour` for all remaining primes. An issue with this is that if primes p<sub>1</sub> and p<sub>2</sub> are coloured the same, their product p<sub>1</sub>p<sub>2</sub> (if it appears in the grid) will be coloured in two halves using the same colour for each half. 

Things that could be done:
- sort out the colours that are used;
- add more colours to the list;
- come up with a programmatic way to generate distinct colours for new primes to replace this list.

### Order of factors

This colours segments in numerical order starting at the top of the circle and moving anticlockwise, e.g. 100 is coloured using the colours for 2, 2, 5, 5 in that order. If you are hoping for children to understand prime factors, it may be better to colour differently, e.g. colouring 100 as 2, 5, 2, 5 would more clearly indicate it is 10^2. Also you might like to colour in numerical order going clockwise instead of anticlockwise.

### Display

Actual Prime Climb doesn't always start drawing segments at the top of the circle. For example, compare 4, 8 and 16. I don't know if this really matters, because I am not trying to duplicate Prime Climb graphics, just playing around with colouring in. 

