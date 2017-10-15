FIASXMLDeltaLoader.xml represents NiFi flow for downloading delta of FIAS database in xml format packed with rar acrhicve. The archive itself can be found at https://fias.nalog.ru/Updates.aspx
Description: the flow invokes FIAS service to get a link to the newest archive with xml delta and download this archive to the local folder
To use this flow it is necessary to provide the following directory structure on the level of "bin" folder of NiFi (of course, you may edit processors as you want):
1. Create "soap" directory where request.xml to FIAS service must be placed
