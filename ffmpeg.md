# Convert from 4K to 2K

- mp4 is just a placeholder for the file, output can be the same as input

```
ffmpeg -i input.mp4 \
  -c:v libx264 -crf 20 -preset slow \
  -vf scale=-2:1440 \
  -g 250 -keyint_min 25 -sc_threshold 40 \
  -pix_fmt yuv420p \
  -c:a aac -b:a 128k -ar 48000 \
  -movflags +faststart \
  output.mp4
```

# From video to audio

## all files in folder

```
for f in *.mp4; do
  ffmpeg -i "$f" -vn -acodec copy "${f%.mp4}-audio.mp4"
done
```

## single file

```
ffmpeg -i input.mp4 -vn -acodec copy output.m4a
```
