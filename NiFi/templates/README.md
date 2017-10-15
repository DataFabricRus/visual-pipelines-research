<h3>FIASXMLDeltaLoader</h3>
<p>FIASXMLDeltaLoader.xml represents NiFi flow for downloading delta of FIAS database in xml format packed with rar acrhicve. The archive itself can be found at https://fias.nalog.ru/Updates.aspx</p>
<h4>Description</h4>
<p>The flow invokes FIAS service to get a link to the newest archive with xml delta and download this archive to the local folder. The flow is set to download archive once in ten days without (!) checking if the base has been advanced or not.</p>
<h4>Usage</h4>
<p>To use this flow it is necessary to provide the following directory structure on the level of "bin" folder of NiFi (of course, you may edit processors as you want):</p>
<ol>
<li>Create "soap" directory where request.xml to FIAS service must be placed. The service description can be found at http://fias.nalog.ru/WebServices/Public/DownloadService.asmx?op=GetLastDownloadFileInfo. The following request is used:</li>

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetLastDownloadFileInfo xmlns="http://fias.nalog.ru/WebServices/Public/DownloadService.asmx" />
  </soap:Body>
</soap:Envelope>
```
<li>Create "in" direcory where archive will be stored</li>
</ol>
