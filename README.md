# Neverending.site
Former hosting repository for the Neverending game website.

### Project status
Completed, pending any future legal updates.

### Video streaming (HLS)
Commands used to split the MP4s into HLS segments and enable chunked playback:

```bash
brew install ffmpeg
mkdir -p media/vid1 media/vid2
ffmpeg -y -i media/vid1.mp4 -c:v libx264 -preset veryfast -crf 24 -c:a aac -b:a 96k -ac 2 -g 60 -keyint_min 60 -sc_threshold 0 -hls_time 2 -hls_playlist_type vod -hls_flags independent_segments -hls_segment_filename media/vid1/segment_%03d.ts media/vid1/stream.m3u8
ffmpeg -y -i media/vid2.mp4 -c:v libx264 -preset veryfast -crf 24 -c:a aac -b:a 96k -ac 2 -g 60 -keyint_min 60 -sc_threshold 0 -hls_time 2 -hls_playlist_type vod -hls_flags independent_segments -hls_segment_filename media/vid2/segment_%03d.ts media/vid2/stream.m3u8
```

We also vendor HLS.js locally for dynamic loading:

```bash
mkdir -p scripts
curl -L -o scripts/hls.min.js https://cdn.jsdelivr.net/npm/hls.js@1.5.7/dist/hls.min.js
```
