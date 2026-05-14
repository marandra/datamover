# datamover

Python pipeline that ingests TIFF microscopy images, converts them to
JP2, generates thumbnails, and moves the products to a destination
directory.

Originally developed at sciCORE (University of Basel) in 2016 as part
of an image-management pipeline for robotic-microscopy data; preserved
here for reference.

## What it does

`datamover` sits between an *incoming* directory (typically the
location where a microscope drops new TIFF files in production) and a
*destination* directory (the long-term storage location):

```
incoming/ ──► buffer/ ──► destination/
   TIFF         TIFF + JP2     JP2 + thumbnails
```

A scheduler runs three jobs in sequence:

1. **Ingest** — move new TIFFs from `incoming/` to a working `buffer/`
   using `rsync`.
2. **Convert** — turn each TIFF into a JP2 file and generate a
   thumbnail (via `tiff2jp2.py`).
3. **Publish** — move JP2 files and thumbnails from `buffer/` to
   `destination/` using `rsync`.

Every action is recorded in a rotating log file.

## Configuration

All paths and logfile names are read from an INI file (`datamover.ini`).
Each setting can be overridden via command-line arguments.

```ini
[paths]
incoming     = /data/microscope/in
buffer       = /data/microscope/buffer
destination  = /data/microscope/out
logfile      = /var/log/datamover.log
```

## Status

Developed in 2016 as a prototype for sciCORE's image-ingestion
pipeline. Kept here as a record of the approach.

## License

See `LICENSE`.
