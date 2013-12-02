osu-parser
==========
[![Build Status](https://travis-ci.org/nojhamster/osu-parser.png?branch=master)](https://travis-ci.org/nojhamster/osu-parser)

A parser that converts osu files into javascript objects. Feel free to comment if you are interested !

- [Installation](#installation)
- [Usage](#usage)
- [The resulting object](#the-resulting-object)
- [Methods](#methods)
	- [parseFile(filepath, callback)](#parsefilefilepath-callback)
	- [parseStream(stream, callback)](#parsestreamstream-callback)
	- [parseContent(content)](#parsecontentcontent)
- [TODO](#todo)

## Installation

```
npm install osu-parser
```

## Usage

```javascript
  var parser = require('osu-parser');
  
  parser.parseFile('path/to/map.osu', function (err, beatmap) {
    console.log(beatmap);
  });
```

## The resulting object

It contains all key/value pairs with a **lowercased** key :
```
...
PreviewTime: 42860
...
```
```
beatmap: {
  ...
  previewtime: 42860,
  ...
}
```

### Additionnal attributes :  
`fileformat` : osu file format (v7, v12...).  
`nbcircles` : number of circles.  
`nbsliders` : number of sliders.  
`nbspinners` : number of spinners.  
`bpm` : a single number if constant (ex `150`), or min~max (ex `140~180`).  
`totaltime` : total time in seconds (between the first timing point and the last object).  
`drainingtime` : draining time in seconds.  


## Methods

### parseFile(filepath, callback)
Parse the given file. The callback returns (error, beatmap).
```javascript
  var parser = require('osu-parser');
  
  parser.parseFile('path/to/map.osu', function (err, beatmap) {
    console.log(beatmap);
  });
```

### parseStream(stream, callback)
Parse a stream containing a file content. The callback returns (error, beatmap).
```javascript
  var parser = require('osu-parser');
  var fs     = require('fs');
  var stream = fs.createReadStream('path/to/map.osu');
  
  parser.parseStream(stream, function (err, beatmap) {
    console.log(beatmap);
  });
```

### parseContent(content)
Parse the content of a file as a string or a buffer.
```javascript
  var parser  = require('osu-parser');
  var fs      = require('fs');
  var content = fs.readFileSync('path/to/map.osu');
  
  var beatmap = parser.parseContent(content);
```

## TODO
- put timing points into an array
- put hit objects into an array
- put events into an array
- evaluate map difficulty ? (probably too complicated)
- add a synchronous version of parseFile
- make it usable in a browser ? (not sure that would be useful)
- ...

Feel free to post an issue if you want something else !
