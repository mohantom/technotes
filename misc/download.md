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

youtube-dl -f "140" https://www.youtube.com/watch?v=B-yHoIUGreY

// download and merge to mp4
youtube-dl -f "bestvideo[height<=?1080][ext=mp4]+bestaudio[ext=m4a]" ^
--merge-output-format mp4 https://www.youtube.com/watch?v=khgFBPihapo

// with subtitles in "cmd" with ^ (use \ for linux)
youtube-dl --write-auto-sub -f "bestvideo[height<=?1080][ext=mp4]+bestaudio[ext=m4a]" ^
--merge-output-format mp4 https://www.youtube.com/watch?v=veO8DcF1ITM

// audio only, m4a format: 140 (128kbps), 139 (48kbps)
youtube-dl -f 140 video_url
youtube-dl -f 139 video_url
```


## Economist
https://audiocdn.economist.com/sites/default/files/AudioArchive/2021/20210123/Issue_9230_20210123_The_Economist_Full_edition.zip
https://audiocdn.economist.com/sites/default/files/AudioArchive/2021/20210130/Issue_9231_20210130_The_Economist_Full_edition.zip
https://audiocdn.economist.com/sites/default/files/AudioArchive/2021/20210213/Issue_9232_20210213_The_Economist_Full_edition.zip
https://audiocdn.economist.com/sites/default/files/AudioArchive/2021/20210213/Issue_9232_20210213_The_Economist_Full_edition.zip
https://audiocdn.economist.com/sites/default/files/AudioArchive/2021/20210220/Issue_9233_20210220_The_Economist_Full_edition.zip


