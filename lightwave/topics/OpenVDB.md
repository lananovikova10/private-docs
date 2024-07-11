# OpenVDB V11.0

The OpenVDB Library has been updated to Version 11 (http://www.openvdb.org).

## Changes

This version introduces ABI changes relative to older major releases, so to preserve ABI compatibility it might be
necessary to define the macro OPENVDB_ABI_VERSION_NUMBER=N.

OpenEXR 2 and Python 2 are no longer supported.

### OpenVDB:

* Improvements:
    * Removed use of boost::any in favor of std::any. [Contributed by Brian McKinnon]
* Bug Fixes:
    * Fix potential crash reading corrupt .vdb files with invalid blosc or zip
      chunks. [Contributed by Matthias Ueberheide]


