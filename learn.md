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
