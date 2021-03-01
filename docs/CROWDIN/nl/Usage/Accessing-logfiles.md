# Logbestanden uitlezen

* Verbind je telefoon met een computer in bestandsoverdrachtsmodus
* Locate the log files in the AndroidAPS data directory
    
    * The folder will be at a location similar to ***Internal storage(1) / Android / data / info.nightscout.androidaps / files***
    * The naming of the root storage folder (1) may vary a little depending on the phone.

![logs](../images/aapslog.png)

* The current log is a .log file which can be viewed in a number of ways such as [LogCat](https://developer.android.com/studio/debug/am-logcat.html) within Android Studio, any Log Viewer android app, or simply as plain text. 
* Oudere logbestanden worden gezipt en in mappen opgeslagen op volgorde van datum/tijd. 
* If you are sharing your log file in [gitter](https://gitter.im/MilosKozak/AndroidAPS) to talk about a potential bug, please unzip and upload the file dated before the error occurred.