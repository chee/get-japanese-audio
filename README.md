# ja

get the japanese audio urls for a word from jisho.org

## installation

this isn't on `npmjs.com`, so if you want to install it you'll need to do this:

```
$ npm i -g https://github.com/chee/ja
```

## librarial interface
```js
const ja = require('ja')

ja({
  term: '犬',
  reading: 'いぬ'
}).then(results => {
  console.log(results[0])
  // => http://d1vjc5dkcd3yh2.cloudfront.net/audio/10ce3f5eb7b4a9a03c4dafce2af60e28.mp3
})
```

you can pass `raw: true` to get a newline separated list as
a string, instead of an array

## command line interface

```sh
# everything
$ ja dog
http://d1vjc5dkcd3yh2.cloudfront.net/audio/10ce3f5eb7b4a9a03c4dafce2af60e28.mp3
http://d1vjc5dkcd3yh2.cloudfront.net/audio_ogg/10ce3f5eb7b4a9a03c4dafce2af60e28.ogg
http://d1vjc5dkcd3yh2.cloudfront.net/audio/45bac2d853cf192d099f3f0fddfdba31.mp3
http://d1vjc5dkcd3yh2.cloudfront.net/audio_ogg/45bac2d853cf192d099f3f0fddfdba31.ogg
http://d1vjc5dkcd3yh2.cloudfront.net/audio/cec22fd7beaa43340c378e17a98fb298.mp3
http://d1vjc5dkcd3yh2.cloudfront.net/audio_ogg/cec22fd7beaa43340c378e17a98fb298.ogg

# by reading
$ ja 犬 -r いぬ
http://d1vjc5dkcd3yh2.cloudfront.net/audio/10ce3f5eb7b4a9a03c4dafce2af60e28.mp3
http://d1vjc5dkcd3yh2.cloudfront.net/audio_ogg/10ce3f5eb7b4a9a03c4dafce2af60e28.ogg

# by filetype
$ ja dog | grep [.]ogg$
http://d1vjc5dkcd3yh2.cloudfront.net/audio_ogg/10ce3f5eb7b4a9a03c4dafce2af60e28.ogg
http://d1vjc5dkcd3yh2.cloudfront.net/audio_ogg/45bac2d853cf192d099f3f0fddfdba31.ogg
http://d1vjc5dkcd3yh2.cloudfront.net/audio_ogg/cec22fd7beaa43340c378e17a98fb298.ogg

# as json (for piping to jq/jshon)
$ ja inu -r いぬ -j
["http://d1vjc5dkcd3yh2.cloudfront.net/audio/10ce3f5eb7b4a9a03c4dafce2af60e28.mp3","http://d1vjc5dkcd3yh2.cloudfront.net/audio_ogg/10ce3f5eb7b4a9a03c4dafce2af60e28.ogg"]

# when there are no results
$ ja pleased to meet you
$ echo $?
1
```

## jag

in the bin directory there is also a script called `jag`, which is macos only
and will only really work if you have the japanese speech to text installed on
your macintosh and set up as your default speech to text.

everyone should do that and enable notification reading so she says
アレルト！　ロウ　バテリ！ to you. it warms.

anyway it will fetch the first word it finds for your term and optional reading
as an ogg and save it, then open finder with that new file highlighted. then you
can drag it into anki or burn it to cd or put it on your zip drive.

if it can't find a file for you on the interconnected network of computers, it
will create one with `say(1)`.

thanks kyoko

interface is like:

```sh
$ jag $term $reading

# like

$ jag あれ

# now you'll have a file called あれ.ogg

# you can force it to use say by setting the env variable SAY to
# something truthy

$ SAY=下さい jag 犬
```

it's not installed when you install this repo with npm, you'd have to download
it yourself

## todo

* more sources
