# GRR_some_Utils_bash

## create  a playlist with flac into a directory
`$ ls *.flac > "00 - `basename "$PWD"`.m3u" `


## copy stream from webm or mkv

https://stackoverflow.com/questions/9913032/how-can-i-extract-audio-from-video-with-ffmpeg

list all streams in container

`ffmpeg -i "input.webm" `

    ...
    Input #0, matroska,webm, from 'input.webm':
      Metadata:
        encoder         : no_variable_data
        creation_time   : 1970-01-01T00:00:00.000000Z
      Duration: 00:23:30.07, start: 0.000000, bitrate: 1392 kb/s
        *Stream #0:0:* Audio: aac (LC), 48000 Hz, stereo, fltp (default)
        Metadata:
    ...

`ffmpeg -i input.webm -map 0:0 -acodec copy audio.aac`

or older option -vn

`ffmpeg -i "input.webm" -vn -acodec copy "output.oga"`

## find if filename contains a certain string in bash script
You need space after [[ and before ]]:
`for file in *.out;do
  if [[ "$file" == *"$STRING"* ]];then
    printf '%s\n' "$file"
  fi
done`

or just

`for file in *"$STRING"*.out; do
    printf '%s\n' "$file"
done `

or

` printf '%s\n' *"$STRING"*.out `

