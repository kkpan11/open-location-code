# Open Location Code Reference API

## Version History

- Version 1.0.0 / 2014-10-27 / [Doug Rinckes](https://github.com/drinckes), Google / Philipp Bunge, Google
  - Initial public release

## Public methods

The following public methods should be provided by any Open Location Code implementation, subject to minor changes caused by language conventions.

Note that any method that returns an Open Location Code should return upper case characters.

Methods that accept Open Location Codes as parameters should be case insensitive.

### `isValid`

The `isValid` method takes a single parameter, a string, and returns a boolean indicating whether the string is a valid Open Location Code sequence or not.

To be valid, all characters must be from the Open Location Code character set with exactly one separator.
There must be an even number of at most eight characters before the separator.
(Zero characters before the separator is valid.)

### `isShort`

The `isShort` method takes a single parameter, a string, and returns a boolean indicating whether the string is a valid short Open Location Code or not.

A short Open Location Code is a sequence created by removing an even number of characters from a full Open Location Code.
The resulting code must still include the separator character.

### `isFull`

Determines if a code is a valid full Open Location Code.

Not all possible combinations of Open Location Code characters decode to valid latitude and longitude values.
This checks that a code is valid and also that the latitude and longitude values are legal.
Full codes must include the separator character and it must be after eight characters.

### `encode`

Encode a location into an Open Location Code. 
This takes a latitude and longitude and an optional length.
If the length is not specified, a code with 10 digits and an additional separator character will be generated.

### `decode`

Decodes an Open Location Code into the location coordinates. This method takes a string.
If the string is a valid full Open Location Code, it returns an object with the lower and upper latitude and longitude pairs, the center latitude and longitude, and the length of the original code.

### `shorten`

Passed a valid full Open Location Code and a latitude and longitude this removes as many digits as possible (up to a maximum of six) such that the resulting code is the closest matching code to the passed location.
A safety factor may be included.

If the code cannot be shortened, the original full code should be returned.

Since the only really useful shortenings are removing the first four or six characters, this method may be replaced with methods such as `shortenBy4` or `shortenBy6`.

### `recoverNearest`

This method is passed a valid short Open Location Code and a latitude and longitude, and returns the nearest matching full Open Location Code to the specified location.

