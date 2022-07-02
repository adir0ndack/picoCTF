# Matryoshka doll

## Description
Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one?
> Hint: Wait, you can hide files inside files? But how do you find them?

## Solution
We are given a file called dolls.jpg. Running `file` on the image reveals that it is not actually a JPG file.
```bash
$ file dolls.jpg 
dolls.jpg: PNG image data, 594 x 1104, 8-bit/color RGBA, non-interlaced
```

Let's see if there is anything else hidden about this image. 
Use `binwalk` to quickly extract embedded files.


```bash
$ binwalk -e dolls.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378954, uncompressed size: 383940, name: base_images/2_c.jpg
651612        0x9F15C         End of Zip archive, footer length: 22
```

Notice that there was an embedded .zip file - you can move to the extracted directory using `cd _dolls.jpg.extracted/`.

Run `ls` and then `cd` to the directory 'base_images' - there is another image inside, called '2_c.jpg'.

Use `binwalk -e` on this image as well, and then `cd` into the newly extracted directory to find yet another image, '3_c.jpg'.

> Note: you can run binwalk with the -M argument (literally for Matryoshka) to recursively scan all files and skip the repetition of these steps, e.g. `binwalk -eM dolls.jpg`


Repeat this process until you finally reach 'flag.txt'. Run `cat` on it to reveal the flag.

