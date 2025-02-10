# ffmpeg

```shell
mkdir -p out

for i in *.MOV; do
    bname=$(basename "$i")
    bname="${bname%.*}"
    ffmpeg -i "$i" -movflags use_metadata_tags -map_metadata 0 \
      -vcodec libx264 -acodec aac "out/$bname.mp4"
done
```

```shell
out="fix_ts"
mkdir -p "$out"
for i in *.MOV; do
    ts=$(exiftool -T -DateTimeOriginal -n "$i")
    if [ "$ts" = "-" ]; then
        mv "$i" "$out"
        echo "moved $i"
    else
        echo "$ts, $i"
    fi
done
```

```shell
mkdir -p out

for i in *.MOV; do
    ts=$(exiftool -T -DateTimeOriginal -n "$i")
    lat=$(exiftool -T -GPSLatitude -n "$i")
    lon=$(exiftool -T -GPSLongitude -n "$i")
    zone=$(exiftool -T -EXIF:OffsetTime -n "$i")
    bname=$(basename "$i")
    bname="${bname%.*}"
    # echo "$i, $ts, $lat, $lon, $zone"
    out="out/${bname}.mp4"
    ffmpeg -i "$i" -movflags use_metadata_tags -map_metadata 0 \
      -vcodec libx264 -acodec aac "$out"
    exiftool -F -overwrite_original_in_place \
    "-DateTimeOriginal=$ts" \
    "-GPSLatitude=${lat}" \
    "-GPSLatitudeRef=${lat}" \
    "-GPSLongitude=${lon}" \
    "-GPSLongitudeRef=${lon}" \
    "-EXIF:OffsetTime=${zone}" \
    "$out"
done
```