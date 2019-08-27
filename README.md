## NAME

srt-resync - shift subtitles in .srt files by a given offset.

## SYNOPSIS

    srt-resync time [time] [...] [srt_file]

## EXAMPLE

    srt-resync -o -1.3 video.srt
    srt-resync 20.5 32.3 video.srt
    srt-resync 0:0:16.4 11.3 1:34:42.5 1:36:22.2 video.srt

## DESCRIPTION

Adjusts subtitle timing in an .srt file by given offset or factors.  Negative
numbers and partial seconds are supported, as are multi-segment interpolation
from unlimited points.

## OPTIONS

    -o, --overwrite          overwrite original srt file

    --version                show version number and exit

## MISC

To calculate delay, the easiest method is to open the video file using VLC with
the appropriate subtitles. Use the `g`/`k` keyboard shortcuts to modify the
subtitle timing until it's correct. Note the subtitle offset time, then run
`srt-resync` passing the offset as an parameter.

To find multi-point sync points, note the times of speech matching particular
subtitles, then look in the original .srt file for the original time of those
subtitles, and provide the matched old and new timestamps on the command line.
Times are linearly interpolated between specified points.

## LICENSE

Copyright (c) 2013, William Ting, 2019 Evan Harris. License GPLv3: GNU GPL
version 3 or later <http://gnu.org/licenses/gpl.html>. This is free
software: you are free to change and redistribute it. There is NO
WARRANTY, to the extent permitted by law.
