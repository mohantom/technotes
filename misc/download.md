Download youtube videos
========================
// install youtube-dl, ffmpeg
$ pip install youtube-dl --user
add python scripts folder to path
Download, unzip, add to path for ffmpeg: https://ffmpeg.zeranoe.com/builds

```shell script
// get format list
youtube-dl -F https://www.youtube.com/watch?v=kjHQbNwSDHo
// download with mp4 and aac
youtube-dl -f "137+140" --merge-output-format mp4 video_url

// download and merge to mp4
youtube-dl -f "bestvideo[height<=?1080][ext=mp4]+bestaudio[ext=m4a]" --merge-output-format mp4 https://www.youtube.com/watch?v=IzWpimjJ8FI

// with subtitles
youtube-dl --write-auto-sub -f "bestvideo[height<=?1080][ext=mp4]+bestaudio[ext=m4a]" --merge-output-format mp4 https://www.youtube.com/watch?v=IzWpimjJ8FI

// audio only, m4a format: 140 (128kbps), 139 (48kbps)
youtube-dl -f 140 video_url
youtube-dl -f 139 video_url
```


## Economist
https://audiocdn.economist.com/sites/default/files/AudioArchive/2020/20201121/Issue_9221_20201121_The_Economist_Full_edition.zip
https://audiocdn.economist.com/sites/default/files/AudioArchive/2020/20201128/Issue_9222_20201128_The_Economist_Full_edition.zip
https://audiocdn.economist.com/sites/default/files/AudioArchive/2020/20201205/Issue_9223_20201205_The_Economist_Full_edition.zip

https://audiocdn.economist.com/sites/default/files/AudioArchive/2020/20201212/Issue_9224_20201212_The_Economist_Full_edition.zip
https://audiocdn.economist.com/sites/default/files/AudioArchive/2020/20201219/Issue_9225_20201219_The_Economist_Full_edition.zip


