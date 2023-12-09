# COMMON EXPERIENCE

## Downloading videos from Facebook

Chrome:

- Install SaveFrom.Net script with OrangeMonkey script manager at <https://en.savefrom.net>

- Firefox: Install extension Video DownloadHelper at <https://www.downloadhelper.net>

## Fixing conflict ffmpeg library with web browsers

Web browsers, such as Opera, sometimes get conflicts with ffmpeg lib, which causes the browers cannot play videos. I will guide you to fix the bug for Opera.

Go to github: <https://github.com/nwjs-ffmpeg-prebuilt/nwjs-ffmpeg-prebuilt/releases>

Download the zip file in the latest release, extract and we get file the `libffmpeg.so`. Move this so file into directory `/usr/lib64/opera`
(remember to backup the old so file first).
