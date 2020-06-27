Download youtube videos
========================
// install youtube-dl, ffmpeg
$ pip install youtube-dl --user
Download, unzip, add to path for ffmpeg: https://ffmpeg.zeranoe.com/builds

```shell script
// get format list
youtube-dl -F video_url
// download with mp4 and aac
youtube-dl -f "137+140" --merge-output-format mp4 video_url

// download and merge to mp4
youtube-dl -f "bestvideo[height<=?1080][ext=mp4]+bestaudio[ext=m4a]" --merge-output-format mp4 video_url

// with subtitles
youtube-dl --write-auto-sub -f "bestvideo[height<=?1080][ext=mp4]+bestaudio[ext=m4a]" --merge-output-format mp4 https://www.youtube.com/watch?v=Y7VNk73qGRU

// audio only, m4a format: 140 (128kbps), 139 (48kbps)
youtube-dl -f 140 video_url
youtube-dl -f 139 video_url
```
