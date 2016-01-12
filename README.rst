datamover
=========
Converts TIFF to JP2, generate thumbnails, and moves images them between directories.

Description
-----------
Moves and processes files. Modular. Flexible. Current prototype:

- moves file from incoming (microscope in production stage) directory to buffer
- converts them from TIFF to JP2 (using tiff2jp2.py during development stage)
- generates thumbnails (using tiff2jp2 during develpment stage)
- moves JP2 and thumbnails to destination directory

Usage
-----
Uses configuration file (datamover.ini) to set incoming directory, outgoing directory, buffer directory, and logfile names. Those option can be overwritten via command line arguments

Description of the code
-----------------------
- The code uses a conguration parse to set up the directories
- A scheduler sets up three jobs:
  - move tiff to buffer (using rsync)
  - image conversion (using tiff2jp2.py in this stage)
  - move jp2 to destination (using rsync)
-There is a logger system that registers every action in a rotating log file

Validation
----------
See Tiff2jp2.py for validation of the converted image.
Files moving tests are passed OK
