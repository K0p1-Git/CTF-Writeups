# [DragonSectorCTF-2019] Baby PDF
<b><u> Challenge Text: </u></b>

![alt text](https://raw.githubusercontent.com/K0p1-Git/CTF-Writeups/master/DragonSectorCTF-2019/Baby-PDF/challenge.JPG "challenge text")

<b> Resource: </b> https://github.com/K0p1-Git/CTF-Writeups/blob/master/DragonSectorCTF-2019/Baby-PDF/babypdf.pdf

<i>note: The PDF contains an empty page (Part of the challenge, Duh!)</i>

<b><u> Solution: </u></b>
Looking at the <a href="https://github.com/K0p1-Git/CTF-Writeups/blob/master/DragonSectorCTF-2019/Baby-PDF/babypdf.pdf">PDF</a> given. I decided to use the standard command: 
```
root@kali:# pdf-parser [file]
```
Looking at the output of pdf-parser, "obj 6" in particular peaked my interest. There seems to be some graphic object within the PDF, but its empty ? hmmm
```
obj 6 0
 Type: 
 Referencing: 

  <<
    /Creator (cairo 1.15.2 (http://cairographics.org))
    /Producer (cairo 1.15.2 (http://cairographics.org))
  >>
```
After which, I proceeded to use the command:
```
root@kali:# binwalk -e [file]
```
Which got me the following:

![alt text](https://raw.githubusercontent.com/K0p1-Git/CTF-Writeups/master/DragonSectorCTF-2019/Baby-PDF/extracted.JPG "extracted")

Upon closer inspection of the file 4A, it seems to resemble that of a .SVG file. Just without the headers and closing tags: 
```
## File 4A
q
1 1 1 rg /a0 gs
1 1 1 RG 2.834646 w
2 J
2 j
[] 0.0 d
4 M q 1 0 0 -1 0 859.889771 cm
66.855 230.531 484.289 283.93 re B Q
1 1 1 rg 107.43 485.855 m 107.43 499.855 l 115.43 499.855 l 115.43 497.855 l 117.43
 497.855 l 117.43 495.855 l 119.43 495.855 l 119.43 489.855 l 117.43 489.855
 l 117.43 487.855 l 115.43 487.855 l 115.43 485.855 l h
111.43 487.855 m 113.43 487.855 l 113.43 489.855 l 115.43 489.855 l 115.43
 495.855 l 113.43 495.855 l 113.43 497.855 l 111.43 497.855 l h

...
...
...

513.43 499.855 m 513.43 497.855 l 515.43 497.855 l 515.43 493.855 l 517.43
 493.855 l 517.43 491.855 l 515.43 491.855 l 515.43 487.855 l 513.43 487.855
 l 513.43 485.855 l 509.43 485.855 l 509.43 487.855 l 511.43 487.855 l 511.43
 491.855 l 513.43 491.855 l 513.43 493.855 l 511.43 493.855 l 511.43 497.855
 l 509.43 497.855 l 509.43 499.855 l h
513.43 499.855 m f
Q
```


A quick search on the internet let me to a online tool that converts PDF to SVG. This is what i got:

![alt text](https://raw.githubusercontent.com/K0p1-Git/CTF-Writeups/master/DragonSectorCTF-2019/Baby-PDF/extracted-svg.JPG "SVG")
 
It seems like i manged to get the hidden SVG object out of the PDF, but where is the flag ?
I mess around for awhile more before deciding to try and edit the SVG file, which eventually got me the flag:

![alt text](https://raw.githubusercontent.com/K0p1-Git/CTF-Writeups/master/DragonSectorCTF-2019/Baby-PDF/flag.png "flag")

Flag: <i> DrgnS{TooBadWWWIsNotInPDF} </i>

<b><u>Reference:</u></b>

 1. Online Vector Editor
	https://vectr.com/


