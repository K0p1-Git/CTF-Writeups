# [NACTF-2019] Phuzzy Photo
<b><u> Challenge Text: </u></b>
Joyce's friend just sent her this photo, but it's really fuzzy. She has no idea what the message says but she thinks she can make out some black text in the middle. She gave the photo to Oligar, but even his super eyes couldn't read the text. Maybe you can write some code to find the message?

Also, you might have to look at your screen from an angle to see the blurry hidden text
P.S. Joyce's friend said that part of the message is hidden in every 6th pixel

<b> Link: </b> https://raw.githubusercontent.com/K0p1-Git/CTF-Writeups/master/NACTF-2019/The_phuzzy_photo.png

![alt text](https://raw.githubusercontent.com/K0p1-Git/CTF-Writeups/master/NACTF-2019/Phuzzy-Photo/The_phuzzy_photo.png "Phuzzy Photo")

<b><u> Solution: </u></b>
Looking at the <a href="https://raw.githubusercontent.com/K0p1-Git/CTF-Writeups/master/NACTF-2019/The_phuzzy_photo.png">photo</a> given, along with the hint: 
```
 P.S. Joyce's friend said that part of the message is hidden in every 6th pixel 
```
It is clear that this challenge requires knowledge on splicing images and some sort of pixel manipulation. (Which at the time i did not have)

A quick search on the internet let me to a python library "PIL" which can be use to manipulate images, sounds like the right library for the job. 

I spent some time and came up with the following script: 
 
```python
## Solution to phuzzy photo chall
## Imported Image from PIL
from PIL import Image

## Reading in the given challange photo
im = Image.open('The_phuzzy_photo.png','r')

## Retriving RGBA values in the form: List of tuples [(R,G,B,A), ... ,(R,G,B,A)]
pixel_val = list(im.getdata())

## Initializing loop counter x && list new_pixel_val
x = 0
new_pixel_val = [(None)]*90000

## Looping through every tuple of pixel in the pixel_val list
for i in range(len(pixel_val)):
    if ((i % 6) == 0): ## Every 6th pixel gets copied into the new_pixel_val[]
        new_pixel_val[x] = pixel_val[i]
        x += 1

## Re-constructing new_pixel_val[] back into a photo and saving it as out.png
out = Image.new("RGBA", (900, 100))
out.putdata(new_pixel_val)
out.save('out.png')
``` 
After running my script, I ended up with the following output:

![alt text](https://raw.githubusercontent.com/K0p1-Git/CTF-Writeups/master/NACTF-2019/Phuzzy-Photo/out.png "out")

You can see that the output isn't perfect (flag is missing a closing tag), but i am still able to get the flag. 

Flag: <i> nactf{fuzzy_b0y5_un1t3} </i>

<b><u>Reference:</u></b>

 1. Extracting individual pixel values from an image
	https://www.hackerearth.com/practice/notes/extracting-pixel-values-of-an-image-in-python/
	  
 2. Reconstructing an image from an list of RGBA values
	https://www.reddit.com/r/learnpython/comments/2kkg0i/python_pil_library_saving_an_image_from_a_rgba/

