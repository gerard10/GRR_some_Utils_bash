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


## find -exec with multiple commands

A find+xargs answer.

The example below finds all .html files and creates a copy with the .BAK extension appended (e.g. 1.html > 1.html.BAK).

Single command with multiple placeholders

    find . -iname "*.html" -print0 | xargs -0 -I {} cp -- "{}" "{}.BAK"
    
Multiple commands with multiple placeholders

    find . -iname "*.html" -print0 | xargs -0 -I {} echo "cp -- {} {}.BAK ; echo {} >> /tmp/log.txt" | sh

     if you need to do anything bash-specific then pipe to bash instead of sh
 
This command will also work with files that start with a hyphen or contain spaces such as -my file.html thanks to parameter quoting and the -- after cp which signals to cp the end of parameters and the beginning of the actual file names.

    -print0 pipes the results with null-byte terminators.

    for xargs the -I {} parameter defines {} as the placeholder; you can use whichever placeholder you like; -0 indicates that input items are null-separated.


