## NAME

srt-resync - shift subtitles in .srt files by a given offset in seconds

## SYNOPSIS

    srt-resync [seconds] [srt_file]

    srt-resync -o [seconds] [srt_file]

## EXAMPLE

    srt-resync -o -1.3 video.srt

## DESCRIPTION

Shifts subtitles timing in an .srt file by a given offset in seconds. Negative
numbers and partial seconds are supported.

## OPTIONS

    -o, --overwrite          overwrite original srt file

    --version                show version number and exit

## MISC

To calculate delay, the easiest method is to open the video file using VLC with
the appropriate subtitles. Use the `g`/`k` keyboard shortcuts to modify the
subtitle timing until it's correct. Note the subtitle offset time, then run
`srt-resync` passing the offset as an parameter.

## LICENSE

Copyright (c) 2013, William Ting. License GPLv3+: GNU GPL
version 3 or later <http://gnu.org/licenses/gpl.html>. This is free
software: you are free to change and redistribute it. There is NO
WARRANTY, to the extent permitted by law.
