A JHOVE Use Case – JPEG-HUL at Archives NZ
=====
*2016-06-24: By Ross Spencer*

Archives New Zealand has, at present, successfully completed four born-digital deposits. Because we use Ex-Libris’ Rosetta Digital 
Preservation system, part of the workflow allows us to send our digital objects via JHOVE as part of a validation step where we 
look for two simple words, ‘Well-formed, and valid’. 

When our files fail this test, we have to inspect the files manually and understand if we can fix them under strict pre-conditioning 
rules (changes must be reversibly documented), or whether we have to accept the file as not-valid and ingest as-is until we have 
the capacity to be able to create a second preservation master correcting the issue.

An example of our tests failing appeared early in our second deposit with a JPEG failing in JHOVE with the following errors:

[image]

At first, to see three messages like was quite overwhelming. Any issues that arise during a transfer that we haven’t 
seen before will take an undetermined amount of time to fix, and we hadn’t yet come up against this issue. 

Opting to tackle the messages, one error at a time, we manage to fix all three with a single byte stream change, all driven 
by reading a JPEG specification we were able to find via the Just Solve It wiki [(1)](#1). The second error message described plainly 
to us in that documentation:

[image]

With the error reading ‘APP0 marker not at beginning of file’ it was noted that other offsets JHOVE might be looking for 
may be displaced. And so we set about fixing this problem (all the time testing fixes against our potential to do it under 
pre-conditioning.)

On searching around for documents that would help us to understand what an APP0 marker looks like [(2)](#2), we were able to see the 
displaced segment inside the bitstream (fortunately the APP0 marker was still there!) 

Taking an extract of the file header we can see side-by-side how we modified the file to make it valid:

[image]

Testing this as a fix meant first checking it against JHOVE – it was ‘Well-formed and valid’ – our APP0 change had the desired 
cascade effect on the other errors. 

For our pre-conditioning provenance note we could accurately describe the fix with the following paragraph:

    PRECONDITIONING BYTESTEAM 001: Bytes Swapped. JFIF application segment (18 bytes, beginning 0xFFE0) moved directly in front of Photoshop IRB segment (beginning 0xFFDB) and directly after the start of image marker (0xFFD8). MD5 (Original): 02a1b0254fe08cf07e03dde6819a63a9 becomes MD5 (pre-conditioned): 7f0b14e62afb8a02fe101faee39a324c. Modified Date (original) 10 March 2004 becomes modified date (pre-conditioned)

Finally, working closely with our digital archivist, we could demonstrate clearly, no change to the display of the record. 

The file was ingested into Rosetta without issue and made available December 2014, see record number 
[R24684315](https://www.archway.archives.govt.nz/ViewFullItem.do?code=24684315) in Archive New Zealand’s Archway Catalogue. 

**------**

###Footnotes

<a name="1">[1]</a> http://fileformats.archiveteam.org/wiki/JPG - Just Solve It entry for JPG, accessed 24 June 2016 <br/>
<a name="2">[2]</a> http://www.ozhiker.com/electronics/pjmt/jpeg_info/app_segments.html – for example, via http://www.ozhiker.com/ - Accessed 24 June 2016

**------**

###License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
