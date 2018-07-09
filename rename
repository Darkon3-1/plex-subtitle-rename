#!/usr/bin/python
import os, re, sys, getopt
args = getopt.getopt(sys.argv, " ")[1]

# check if correct number of arguments were passed
if len(args) < 4:
    print('Incorrect format.')
    print('rename.py directory season episodes')
    sys.exit()

# add the correct extension with lang code
subExtenstion = '.en.srt' if len(args) == 4 else ".%s.srt" % args[4]

# create the season
season = "0"+ args[2] if len(args[2]) == 1 else args[2]
directory = args[1]

# Get list of files
srtlist = [ f for f in os.listdir(directory) if f.endswith('.srt') ]
mkvlist = [ f for f in os.listdir(directory) if ( not f.endswith('.srt')) ]

# go through both files, find the correct files
# and rename the subtitles correctly
for x in range(1, int(args[3]) + 1):
    episode = "0" + str(x) if x < 10 else str(x)
    search = "S%sE%s" % (season,episode)

    r = re.compile('.*' + search)
    try:
        mkv = filter(r.match, mkvlist)[0]
        srt = filter(r.match, srtlist)[0]
        dirWithPath = os.path.join( directory + '/' + os.path.splitext(mkv)[0] + subExtenstion)
        os.rename(directory + '/' + srt, dirWithPath)
    except IndexError:
        print(search + ' is not found for subtitle or video files')
