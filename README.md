# GRR_some_Utils_bash

## create  a playlist with flac into a directory
$ ls *.flac > "00 - `basename "$PWD"`.m3u"


##copy stream from webm or mkv
ffmpeg -i "input.webm" 
list all streams in container
ffmpeg -i "input.webm" -vn -acodec copy "output.oga"
