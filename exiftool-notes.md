# EXIFTOOL NOTES

## 1. Installation

Download from [exiftool.org](exiftool.org) and unzip.

## 2. Read

### Read all metadata

- Rename the `.exe` file to `exiftool(-k).exe`
- Drag and drop image file to the `.exe`

### Read GEO location [🔗 Reference](https://exiftool.org/geolocation.html#Read)

- Rename the `.exe` file to `exiftool.exe`
- Replace `FILENAME` and run in command line:
  ```shell
  ./exiftool.exe -api geolocation "-geolocation*" FILENAME
  ```
- Example prompt:
  ```shell
  Geolocation City                : Muenchen
  Geolocation Region              : Bayern
  Geolocation Subregion           : Regierungsbezirk Oberbayern
  Geolocation Country Code        : DE
  Geolocation Country             : Bundesrepublik Deutschland
  Geolocation Time Zone           : Europe/Berlin
  Geolocation Feature Code        : PPLA
  Geolocation Feature Type        : Seat Of A First-order Administrative Division
  Geolocation Population          : 1300000
  Geolocation Position            : 48.1375, 11.5755
  ```

## 3. Write

### Copy GPS [🔗 Reference](https://exiftool.org/forum/index.php?topic=6512.0)

- Rename the `.exe` file to `exiftool.exe`
- Run in command line:
  ```shell
  ./exiftool.exe -tagsfromfile SOURCE_FILE -gps:all -wm cg TARGET_FILE
  ```
- `-wm cg` option makes existing tags unchanged

### Modify GPS position [🔗 Renference](https://exiftool.org/faq.html#Q14)

- Replace numbers with desired latitude and longitude

```shell
./exiftool.exe -gpsposition="-12.34567890, -12.34567890" TARGET_FILE
```

### Reset file date [🔗 Reference](https://exiftool.org/forum/index.php?topic=12216.0)

```shell
./exiftool.exe "-FileCreateDate<Exif:CreateDate" TARGET_FILE
./exiftool.exe "-FileModifyDate<Exif:CreateDate" TARGET_FILE
```
