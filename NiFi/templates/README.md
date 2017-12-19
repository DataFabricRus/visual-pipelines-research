<h3>FIASXMLDeltaLoader</h3>
<p>FIASXMLDeltaLoader.xml represents NiFi flow for downloading delta of FIAS database in xml format packed with rar acrhicve. The archive itself can be found at https://fias.nalog.ru/Updates.aspx</p>
<h4>Description</h4>
<p>The flow invokes FIAS service to get a link to the newest archive with xml delta and download this archive to the local folder. The flow is set to download archive once in ten days without (!) checking if the base has been advanced or not.</p>
<h4>Usage</h4>
<p>To use this flow it is necessary to provide the following folder structure on the level of "bin" folder of NiFi (of course, you may edit processors as you want):</p>
<ol>
<li>Create "soap" folder where request.xml to FIAS service must be placed. The service description can be found at http://fias.nalog.ru/WebServices/Public/DownloadService.asmx?op=GetLastDownloadFileInfo. The following request is used:</li>

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetLastDownloadFileInfo xmlns="http://fias.nalog.ru/WebServices/Public/DownloadService.asmx" />
  </soap:Body>
</soap:Envelope>
```
<li>Create "in" folder where archive will be stored.</li>
</ol>

<h3>FIASXMLDeltaUnpacker</h3>
<p>FIASXMLDeltaUnpacker.xml represents flow for unpacking rar archive.</p>
<h4>Description</h4>
<p>The flow unpacks localy store archive to another folder</p>
<h4>Usage</h4>
<p>To use this flow it is necessary to provide the following folder structure on the level of "bin" folder of NiFi (of course, you may edit processors as you want):</p>
<ol>
<li>Checks that there is "in" folder where rar archive cand be foud;</li>
<li>Create "out" folder where unpacked files will be stored.</li>
</ol>

<h3>GroupFilesOnCopy</h3>
It is a group processor that encapsulate functionality to copy files from some source to some destination. While coping files are grouped in chunks (groups). When any group of files is written to the destination the group signal is arisen that can be used to work on that group of files.

How to use:
<ol>
  <li>Filenames that read from the source with some "List'er" are sent on `source-origin-filename` in port;</li>
  <li>Filenames are merged in groups (chunks). The result can be taken from `source-grouped-filename` out port. There will be   flowfiles with original filenames + the name of the group;</li>
  <li>The recived flowfiles are used to get files from the source with some "Fetch'er";</li>
  <li>Fetched files are sent back but on `source-grouped-file` in port;</li>
  <li>As a result a list of files with new group names can be received from `destination-grouped-file` out port. The original filename of a file is change on the following `[group-name.[merge.index].[merge.count]]`;</li>
  <li>Received list of files is stored at destination with some "Put'er";</li>
  <li>To get a singal when a group files is written to the destination it is necessary to do the follofing. Firstly, to provide `destination-filename` in port with a list of filenames at the destination gotten wiht some "List'er". And secondly, to connect processor that is wainting for files to `group-signal` out port. The signal is a flowfile with some group name.</li>
</ol>

To main setting of the group processor is the size of the bin and the bin lifetime that are set for MergeProcessor inside the group.
