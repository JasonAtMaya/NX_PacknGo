# NX_PacknGo
This is intended to be a replacement for UGZipC a UG Zip Components utility
used to package assemblies into a zip file.

This program assumes 7-Zip is installed as either C:\Program Files\7-Zip\7z
or "C:\Program Files (x86)\7-Zip\7z".  If it is somewhere else then the "path7z"
variable will need to be changed to be able to find it.

It is designed to be run from an NX Command Prompt command line using the
run_journal command like this:

    run_journal NXZip.vb -args "<path to assembly>.prt"

If you have an NX Open for .Net Author or NX Open Toolkits Author license,
this source can also be built into an executable which you would run like this:

    NXZip.exe "<path to assembly>.prt"

Just like NX, this utility will use a load_options.def file in the current
folder to find the full paths to the component parts, wave parents and other
interpart reference parts.  It does not load the components, but it does try to
load interpart data parent parts.  If no load_options.def file exists, the
default load options will be used.

This same source code can also be used to process the current work part in
interactive NX using Tools-> Journal-> Play.  When used this way all partially
or fully loaded parts are included in the zip file along with all of the
components of the work part.  Make sure that you have closed all parts that are
not part of the work assembly that you do not want to be included and that you 
have loaded all wave parent parts that are not components of the work assembly
that you do want to be included.

The paths to the parts included in the zip file are written to a temporary text
file.  This file can be modified if necessary and used again from any command
prompt window like this:

    7z <another>.7z @<temp file>.txt

NOTE:  In NX6, there is a problem with the method TranslateVariable which may
cause the journal to fail and/or crash the NX session, so please beware!  To
work around simply comment out the line which calls this method by adding a
single quote (') at the beginning of the line.  This issue has been fixed for
NX7.5.  See PR 6271239.

Q.  How do I use it?
A.  Copy/Paste the lines below starting with "Option Strict Off" through "End
Module" to a text file named NXZip.vb or select the link to download the zip
file containing the NXZip.vb source file.

Q.  This makes a .7z file, how can I get a .zip instead?
A.  Change the line which defines the "archive" to end in ".zip" instead of ".7z".

Q.  Does this work for CAE .sim, .fem and .afm parts?
A.  No, the "assembly" relation between the .fem and _i.prt is not currently
recognized.

Q.  Does this work in NX Manager mode?
A.  No.  In NX Manager mode use File-> Export Assembly Outside of Teamcenter...
to export the files to a new folder.  Then manually zip the contents of that
folder.
