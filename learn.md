1. hls and dash does not have much difference apart being
   - dash does not runs on ios supported players like players of safari
2. hls is m3u8 based where as dash is xml based
3. hls also supported fmp4
4. command to convert an mp4 file to dash with manifest with mpd extension

```
ffmpeg -i input.mp4 -map 0 -map 0 -c:a aac -c:v libx264 -b:v:0 800k -b:v:1 300k -var_stream_map "v:0,name:800k v:1,name:300k" -f dash -dash_segment_type mp4 -single_file 1 classroom_manifest.mpd
```

5. command to convert an mp4 file to hls with manifest with m3u8 extension

```
ffmpeg -i input.mp4 -map 0 -map 0 -c:a aac -b:v:0 800k -b:v:1 300k -var_stream_map "v:0,name:800k v:1,name:300k" -master_pl_name classroom_manifest.m3u8 -f hls -hls_flags single_file -hls_playlist_type vod -hls_segment_filename "classroom_%v/classroom.ts" classroom_%v/index.m3u8
```

```
ffmpeg -re -i ~/Downloads/SampleVideo_1280x720_1mb.mp4 -map 0 -map 0 -c:a aac -c:v libx264 -b:v:0 800k -b:v:1 300k -s:v:1 320x170 -profile:v:1 baseline -profile:v:0 main -bf 1 -keyint_min 120 -g 120 -sc_threshold 0 -b_strategy 0 -ar:a:1 22050 -use_timeline 1 -use_template 1 -window_size 5 -adaptation_sets "id=0,streams=v id=1,streams=a" -f dash output_manifest.mpd
```

# ffmpeg

1. trim specific part of the video

```
ffmpeg -i input.mp4 -ss 10 -t 20 output.mp4
```

here

- -i is input,
- -ss is the seek duration in seconds, which says seek to 10th second of the video
- -t is the total duration till the video should be trimmed to, this is also in seconds

the output of this will create a 20 second video which is from 10th second of the original video to 30th second of the original video

```
ffmpeg -i input.mp4 -ss 00:00:10 -to 00:00:30 output.mp4
```

here

- -to is the end time

this command behaves exactly similar to the previous command

NOTE - if the time duration provided is only 00:10 then it will be mm:ss

2. trim and convert to different video format

```
ffmpeg -i input.mov -ss 00:00:10 -to 00:00:15 -c:v libx264 output.mp4
```

what is -c:v
what is libx264
what is the difference between mov and mp4

3. convert video to audio

```
ffmpeg -i input.mp4 output.mp3
```

4. merge multiple videos to a single video

```
ffmpeg -f concat -i input.txt -c copy output.mp4
```

here, input.txt will have contents like

```
file video1.mp4
file video2.mp4
file video3.mp4
```

- -c copy will copy the previous file's (first file's properties) and use the same for the next video

```
ffmpeg -f concat -i input.txt output.mp4
```

here, since we have not provided `-c copy` and input file have different formats like mp4, mkv, mov it will all be converted to the outputs format, in the above case mp4

# learning resources

https://docs.fileformat.com

![video format technical information](image.png)
