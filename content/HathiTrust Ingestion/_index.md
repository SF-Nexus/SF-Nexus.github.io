---
title: "HathiTrust Ingestion"
description: "Uploading Texts to HathiTrust with Python"
cascade:
  featured_image: '/images/hathi_1.png'
menu:
  main:
    weight: 1
---
Temple has ingested over 300 science fiction texts into the [HathiTrust Digital Library](https://www.hathitrust.org/). Because HathiTrust requires specific file formats for upload, Python code was used to packaged all necessary files for the sf collection. Running the Python ingestion code in the command line generated the following files for upload to HathiTrust: 
- Image files (TIFF) for each page of each title (duplicated from server)
- OCR files for each page of each title (generated by Google Tesseract)
- Metadata file (YML) containing administrative and technical metadata
- Checksum file listing every file in package and its corresponding md5 hash value

The ingestion code and associated tutorial are available on the [HathiTrust-Ingestion-Scripts Github Repository](https://github.com/SF-Nexus/HathiTrust-Ingestion-Scripts). 

See a full list of HathiTrust ingestion requirements [here](https://www.hathitrust.org/submission-package-requirements-digitized-content-submitted-to-hathitrust)
