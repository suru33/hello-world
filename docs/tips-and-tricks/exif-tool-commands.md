Installation instruction are [here](https://exiftool.org/)

## Update details

!!!note

    All commands should tail by image path or directory path

```shell
lat=""
lon=""

exiftool -F -overwrite_original_in_place \
  "-DateTimeOriginal=2025:02:05 21:33:45" \
  "-GPSLatitude=${lat}" "-GPSLatitudeRef=${lat}" \
  "-GPSLongitude=${lon}" "-GPSLongitudeRef=${lon}" 
```

## Update file crated time

```shell
exiftool -F -overwrite_original_in_place \
  "-DateTimeOriginal=2025:02:05 21:33:45" 
```

## Update file crated time with timezone

```shell
exiftool -F -overwrite_original_in_place \
  "-DateTimeOriginal=2024:11:23 17:20:09+05:30" 
```

## Update file time timezone

```shell
exiftool -F -overwrite_original_in_place "-EXIF:OffsetTime=+05:30"  
```

# Move files with no created timestamp to a directory

In this example the dir name is `fix_ts`

```shell
exiftool -if 'not $DateTimeOriginal' -Directory=fix_ts 
```

## Copy files to dates based directory

This will create `sorted/2025/01/29` directory

```shell
exiftool -o . -d "%Y/%m/%d" '-Directory<./sorted/$DateTimeOriginal' .
```