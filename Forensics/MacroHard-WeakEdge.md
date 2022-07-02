 # MacroHard WeakEdge
 
 ## Description
 I've hidden a flag in this file. Can you find it? Forensics is fun.pptm
 
 ## Solution
 
 We are given a .pptm file, which can be extracted (like a .zip) using `unzip`. 
 Looking at the extracted contents, we have various slides, themes, and layouts - but one file jumps out, called 'ppt/slideMasters/hidden'.
 Running `cat` on this file appears to bring up a base64 encoded string, with each character separated by a space.
 
 We can make this output readable using `base64`:
 
 ```bash
 $ cat ppt/slideMasters/hidden | tr -d ' ' | base64 -d
```

This prints the flag.
