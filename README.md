# Upload Files Sample App

This sample app demonstrates problem with uploading big files in ASP.NET Core when hosting application in IIS web server


## How to use the sample

In the *appsettings.json* file:

1. Set the path for stored files (`StoredFilesPath`).

   * The sample app sets the value to `d:\\temp\\CoreUpload`, which assumes that a folder named *CoreUpload* exists in the folder `temp`   D drive
   * The path must exist. Create a *d:\\temp\\CoreUpload* folder on the D: drive or set the path to a suitable location.
   * The app's process requires read/write permissions to the path.
   * **IMPORTANT!** Disable execute permissions for all users at the path.

1. Set the file size limit (`FileSizeLimit`) in bytes. The sample app's default value of `12884901888` (12,884,901,888 bytes) permits file uploads up to 12 GB.
