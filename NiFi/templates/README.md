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
