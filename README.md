# Upload Files Sample App

This sample app demonstrates problem with uploading big files in ASP.NET Core when hosting application in IIS web server


## How to use the sample

In the *appsettings.json* file:

1. Set the path for stored files (`StoredFilesPath`).

   * The sample app sets the value to `d:\\temp\\CoreUpload`, which assumes that a folder named *CoreUpload* exists in the folder `temp`   D drive
   * The path must exist. Create a *d:\\temp\\CoreUpload* folder on the D: drive or set the path to a suitable location.
   * The app's process requires read/write permissions to the path.
   * **IMPORTANT!** Disable execute permissions for all users at the path.

2. Set the file size limit (`FileSizeLimit`) in bytes. The sample app's default value of `12884901888` (12,884,901,888 bytes) permits file uploads up to 12 GB.
3. Publish it to IIS
4. Modify web.config to have `hostingModel="outofprocess"` and add `requestLimits maxAllowedContentLength="4294967295"` to `requestFiltering` section
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
	    <remove name="aspNetCore" />
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath="dotnet" arguments=".\SampleApp.dll" stdoutLogEnabled="true" stdoutLogFile=".\logs\stdout" hostingModel="outofprocess" requestTimeout="00:02:00" />
	  <security> 
		<requestFiltering>
		 <requestLimits maxAllowedContentLength="4294967295" />
		</requestFiltering>
		</security>
    </system.webServer>
  </location>
</configuration>
```
5. Navigate to `http://localhost/StreamedSingleFileUploadPhysical` choose file greater then 2GB and click *Upload* button
