# Big Zip

>  Description
>  Unzip this archive and find the flag.
>  Download zip file

We are given a zip file, and prompted to use 'grep' to find the flag.

Use 'wget' to download the zip, and 'unzip' to extract.

'''bash
grep -nr 'picoCTF{'
'''


