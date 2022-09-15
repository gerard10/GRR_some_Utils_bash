# GRR_some_Utils_bash

## create  a playlist with flac into a directory
`$ ls *.flac > "00 - `basename "$PWD"`.m3u" `


## copy stream from webm or mkv
`ffmpeg -i "input.webm" `

list all streams in container

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

