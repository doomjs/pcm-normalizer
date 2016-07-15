# PCM audio data normalizer

node.js Stream utility to normalize 16-bit or 32-bit PCM audio data.

## Usage

```javascript
var fs = require('fs');
var Normalizer = require('pcm-normalizer');

var reader = fs.createReadStream('./source.pcm');
var writer = fs.createWriteStream('./destination.pcm');
var normalizer = new Normalizer(32);

normalizer.on('normalization', function(){
    process.stdout.write('.');
});
normalizer.on('gain', function(gain){
    console.log('gain', gain);
});

reader.pipe(normalizer);
normalizer.pipe(writer);
```

## Class: Normalizer

```Normalizer``` is a Transformer stream, with extra events.

#### new Normalizer([bitDepth])

* ```bitDepth``` &lt;number&gt; optional bit depth, default is ```16```.

Create a new instance of a normalizer stream handler.

#### Event: 'normalization'

* &lt;number&gt;

The ```'normalization'``` event is emitted on audio normalization (if enabled) and returns the current current position of the normalization in percentage (from 0 to 100).

#### Event: 'gain'

* &lt;number&gt;

The ```'gain'``` event is emitted after normalization and returns the scale of normalization.