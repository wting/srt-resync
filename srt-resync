#!/usr/bin/env python3
"""
  Copyright (c) 2013, William Ting

  *  This program is free software; you can redistribute it and/or modify
  it under the terms of the GNU General Public License as published by
  the Free Software Foundation; either version 3, or (at your option)
  any later version.

  *  This program is distributed in the hope that it will be useful,
  but WITHOUT ANY WARRANTY; without even the implied warranty of
  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
  GNU General Public License for more details.

  *  You should have received a copy of the GNU General Public License
  along with this program; if not, write to the Free Software
  Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301, USA.
"""

import argparse
import datetime
import os
import re
import shutil
import sys

from io import FileIO as file

VERSION = "0.1"

def parse_options():
    global VERSION

    parser = argparse.ArgumentParser(
            description = 'Offset srt subtitles.')

    parser.add_argument('offset', type = float)
    parser.add_argument('srt_file', type = file)
    parser.add_argument('-o', '--overwrite', action = "store_true", default = False,
            help = "overwite original file")
    parser.add_argument('--version', action = "version", version = "%(prog)s " + VERSION,
            help = "show version information and quit")

    return parser.parse_args()

def rzeropad(ms):
    ms = str(int(ms))
    while len(ms) < 3:
        ms += "0"
    return ms

def offset_time(offset, time_string):
    #FIXME: does not support timestamps >= 24 hours
    ts = time_string.replace(',', ':').split(':')
    ts = [int(x) for x in ts]
    ts = datetime.datetime(2013, 1, 1, ts[0], ts[1], ts[2], ts[3] * 1000) # millisecond -> microsecond

    delta = datetime.timedelta(seconds = offset)
    ts += delta

    if ts.year != 2013 or ts.month != 1 or ts.day != 1:
        sys.exit("ERROR: invalid offset resulting timestamp overflow")

    return "%s,%s" % (ts.strftime("%H:%M:%S"), rzeropad(ts.microsecond / 1000)) # microsecond -> millisecond

def modify_file(options):
    if '.srt' not in options.srt_file.name:
        sys.exit("ERROR: invalid srt file")

    out_filename = os.path.splitext(options.srt_file.name)[0] + '-resync.srt'
    with open(out_filename, 'w', encoding = 'utf-8') as out:
        with open(options.srt_file.name, 'r', encoding = 'utf-8') as srt:
            for line in srt.readlines():
                match = re.search(r'^(\d+:\d+:\d+,\d+)\s+--\>\s+(\d+:\d+:\d+,\d+)', line)
                if match:
                    out.write("%s --> %s\n" % (
                        offset_time(options.offset, match.group(1)),
                        offset_time(options.offset, match.group(2))
                        ))
                else:
                    out.write(line)

    if options.overwrite:
        shutil.move(out_filename, options.srt_file.name)

if __name__ == "__main__":
    modify_file(parse_options())
