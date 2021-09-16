This challenge reads
```
How are rocks permeable?
```
Download the zip file attatched to it and extract the contents.
we get two images,namely Mudstones.png,Sandstones.jpg.
There is nothing interesting about the results obtained from Mudstones image using exiftool,binwalk at first.
# exiftool
ran exiftool on the Sandstone image
```
ExifTool Version Number         : 12.16
File Name                       : Sandstones.jpg
Directory                       : .
File Size                       : 128 KiB
File Modification Date/Time     : 2021:08:29 03:49:20-05:00
File Access Date/Time           : 2021:09:11 11:14:15-05:00
File Inode Change Date/Time     : 2021:09:10 10:56:34-05:00
File Permissions                : rw-------
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 72
Y Resolution                    : 72
Current IPTC Digest             : 5d3c5901005e8c5614d69add00a3a2bd
Copyright Notice                : ©2021 all rights reserved 4MRXmZyIVNBp
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 11.88
Rights                          : Copyright-D8M7Y2020
Image Width                     : 780
Image Height                    : 434
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Image Size                      : 780x434
Megapixels                      : 0.339
```
that's some wierd name for copyright(4MRXmZyIVNBp)?.Let's note it down.
# binwalk
Ran binwalk on the Sandstones image,
```
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
461           0x1CD           Copyright string: "Copyright-D8M7Y2020</rdf:li>"
117388        0x1CA8C         Zip archive data, encrypted at least v2.0 to extract, compressed size: 1071, uncompressed size: 2239, name: 4y3
118536        0x1CF08         Zip archive data, encrypted at least v2.0 to extract, compressed size: 12122, uncompressed size: 14629, name: e2ba
130883        0x1FF43         End of Zip archive, footer length: 22
```
extract these files using the command
>binwalk -e Sandstones.jpg

we get a directory with a zip file in it,which asks for password if we try to unzip it.

I tried the wierd copyright name (4MRXmZyIVNBp) as password and it worked.
This inflates two files namely,4y3 which is text file and e2ba which turns out to be a Microsoft Excel 2007+ file.

we can unzip
>unzip e2ba 
```
Archive:  e2ba
  inflating: [Content_Types].xml     
  inflating: _rels/.rels             
  inflating: xl/_rels/workbook.xml.rels  
  inflating: xl/workbook.xml         
  inflating: xl/sharedStrings.xml    
  inflating: xl/theme/theme1.xml     
  inflating: xl/styles.xml           
  inflating: xl/worksheets/sheet1.xml  
  inflating: xl/vbaProject.bin       
  inflating: docProps/core.xml       
  inflating: docProps/app.xml
```
from these extracted files,vbaProject.bin is our hit. file command on this file gives
```
Composite Document File V2 Document, Cannot read section info
```
I searched a bit about what can be done to analyze these files and oletools came handy.
>olevba vbaProject.bin       
```  
olevba 0.60 on Python 3.9.2 - http://decalage.info/python/oletools
===============================================================================
FILE: vbaProject.bin
Type: OLE
-------------------------------------------------------------------------------
VBA MACRO Module1.bas 
in file: vbaProject.bin - OLE stream: 'VBA/Module1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Sub Note()
    Dim UserInput  As Long
    Dim Answer     As Integer
    
    UserInput = vbYesNo
    Answer = MsgBox("Embedded macros can be dangerous. Do you want to continue?", UserInput)
    If Answer = vbYes Then Process
End Sub
Function DistanceBetween(ByVal X1 As Single, ByVal Y1 As Single, ByVal X2 As Single, ByVal Y2 As Single) As Single
    
    DistanceBetween = Sqr((Abs(X2 - X1) ^ 2) + (Abs(Y2 - Y1) ^ 2))
    
    Dim Horizontal  As Single, Vertical As Single
    Horizontal = Abs(X2 - X1)
    Vertical = Abs(Y2 - Y1)
    DistanceBetween = Sqr((Horizontal * Horizontal) + (Vertical * Vertical))
End Function

Function Process()
    MsgBox ("Give me two points (X1,Y1) and (X2,Y2). I will calculate the distance between them for you:")
    Dim numberASInt As Integer
    
    X1 = InputBox("X1")
    Y1 = InputBox("Y1")
    X2 = InputBox("X2")
    Y2 = InputBox("Y2")
    
    If IsNumeric(X1) And IsNumeric(Y1) And IsNumeric(X2) And IsNumeric(Y2) Then
        result = DistanceBetween(X1, Y1, X2, Y2)
        If result >= 0 Then
            MsgBox ("The distance is " + Str(result))
        Else
            MsgBox ("Stegano is a pure python steganography module that can hide and reveal a text message with the red portion of a pixel. Try it now!")
        End If
    Else
        MsgBox ("Only digits are allowed!")
    End If
End Function
```
It appears to be a hint to use the stegano module.

This helps https://stegano.readthedocs.io/_/downloads/en/latest/pdf/

# stegano
>stegano-red reveal -i Mudstones.png
 ```
 TMUCTF{570n3_15_5m4
 ```
 we get the first part of our flag.

 **part-2 of flag will be updated!**
 