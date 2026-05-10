|==============================================================|
| normandyCTF Writeup [Steganography and Forensics Task 2 & 3] |
|      Lochan Thanigai Murugan Padmashree (void.null.id)       |
|==============================================================|

Tip: The hints are quite useful, but it is better to do some of your own exploration/research. Also keep handy tools like CyberChef saved some place.


### Task 2 : Steganography and Forensics [Part 1] ###


Q1.  The given document is sneakily hiding a flag, find it.
Hint: Document editor has options that you don't know.

	After downloading and extracting the attached task files, you will find all the files required to find the required flags for each of the questions.
	For the first question, considering the question mentions a document, we need to look at 'sneakyPeaky.docx'. The first thing I did was selecting all the text just to see if there is any white hidden text. Since I could not find anything, I did a quick search on google on how to find hidden text on word files and found that there exists an option to see hidden text under File->Options->Display. I enabled both the hidden text related check boxes just in case. After clicking okay, there the flag was under the paragraph!!
Obtained Flag: CBITS{y0u_c4n_h1d3_1n_d0cs!?!?!?}


Q2. Why is the image named info??? I don't see any info on the image, that is just some crocodile or alligator!!!
Hint: The flag is CBITS{<what you discovered in the image>}

	The first thing to do when it comes to steganography is to view the exif/metadata of any file. I used an online metadata viewer. Going through it, I found a string under Composer as well as Keywords. It looked like it had been encode, so I opened up CyberChef and pasted the string. Then using the Magic operation I was able to figure out that it was a base32 encoded message, and conveniently CyberChef had also decoded the string. The decoded message was the inside part of the flag required for this question.
Obtained Flag: CBITS{i_am_n0t_n33d3d}


Q3. What did the cat say to be in that position??? Oh, there's some clue left behind, my Python knowledge will come in handy!!!
Hint: Wouldn't reversing the process work?

	For this question there were two files provided, an image (theCat.png) and a python script (theCatHides.py). Upon analyzing the python script, it seemed to function as a least significant bit image encoder that allows you to hide text within an image. Reverse engineering the program to take the image as input and decode the text will give you the flag (might be with a bit of junk values).
Obtained Flag: CBITS{W3lc0m3_t0_Scr1pt1ng}


Q4. Computer understands only Binary, its either a yes or it's a no. Is there a possibility that these random yes and no can store more than yes and no???
Hint: If only we could extract the string from the binaries...

	This question refers to 'YesOrNo.exe'. Something I usually do to any file for a ctf is open it up in notepad and use the find button to search for what I'm looking for. In this case I knew the flag was of the form CBITS{<flag text>} so I searched for 'CBITS' and got the flag. There were some junk characters in between though, which i had to remove. I am not sure if this was the right way to do it but if it works, it works! :p
Obtained Flag: CBITS{h1dd3n_1n_7h3_b1nar135}


### Task 3 : Steganography and Forensics [Part 2] ###


Q1. I downloaded a BTS album for the first time and it was trash as expected! There's just beeps and boops. Can you help me translate it?
Hint: A painter and a grieving widower.

	Upon listening to the audio file and based on the question, it was obviously morse code. I opened up an online morsecode audio decode (morsecode.world), uploaded the file and ran it through. When the audio ended, the decoded text was obtained.
Obtained Flag: CBITS{M0RS3C0D3W4SC00L}


Q2. Another Album, Another Trash! Looks like the entire music industry has lost its soothing spectrum!
Hint: Made with a bump.

	The same website as the one in question one can be used for this audio file as well. Opening up the Audio Decoder (Expert), uploading the file and playing it gives you the flag (scroll down to find it). This ended up being a spectogram decode.
Obtained Flag: CBITS{th3_4ud4c1ty}


Q3. We have this weird file, no extension, doesn't even execute anything. We need to find out what file type this is if we want to find the flag!!!
Hint: Extensions dictate how a file is read by your system.

	Looking at the hint, i renamed it by giving it a '.txt' extension. Upon opening the file, I saw 'Rar' at the top most line. Seeing this i renamed the file with '.rar' extension and extracted the compressed file. Opening the file, we can see XML code. Using the Find feature on notepad, we can obtian the flag. Also, on renaming the file with '.xml' extension and opening it, you will find a handsome penguin.
Obtained Flag: CBITS{f1L3_3x73n5i0N_f0unD}


Q4. Someone stole one '7b', three '48' and three '58' from my file and now they are ZERO ZERO. Helppp meee!!! Keep trying until you get my file back... I mean when it makes sense!
Hint: No Hint

	Convert the provided hex characters from hex to ascii. The obtained characters are '{', 'H' and 'X'. Placing these characters based on the number of each characters within the contents of the 'myfile.txt' file, we obtain the flag.
Obtained Flag: CBITS{H3X_H3X_H3X}


Q5. I retrieved an image from an alien spaceship and guess what? It was the same image that we had sent out in space 55 years ago, but something is not right with the image. I believe it was manipulated! Help me find out!
Hint: No Hint

	An image with just blue background. How suspicious! Trying any of the previous methods, I was unable to obtain any results. But I often mess with images to see if I can improve visibility or enhance colours, etc. That gave me the idea of opening it in an image editor and playing around with the various parameters (contrast, brightness and such). Thus, I was able to obtain the flag.
Obtained Flag: CBITS{1_4m_H1dd3n}


Q6. These two files contain the best villain movies ever gave us! But why is it two files?... isn't it supposed to be hello world; just one file. Anyways. I am told the 512 checksum of the villain is the flag.
Hint: png

	The link provided to a Google Drive folder contains two blank files with no extension. Opening both files in text editor shows us hexadecimal characters only. The hint suggest we need to obtain a png image. I took help from one of the other competitors for this one as I am not very experienced. Step 1 was to  combine the contents of both the binary files into one using the following command 'cat hello.bin world.bin > helloworld.bin' and then using the xxd tool to convert the binary file into a png file using the command 'xxd -p helloworld.bin > combined.png'. I don't remember if we convert from bin to hex and then hex to png file or bin to png directly. Just try out different things, eventually you will be able to open and see the villain. Step 2 is to obtain the 512 checksum which can be done using 'sha512sum helloworld.png', the obtained checksum is the flag.
Obtained Flag: CBITS{ccec28a5ac52e4ea856df8b74d0dd63537125f10984c3304f70f15415dd41bfd666571bfec10f046a2af98edf2f1266d4fddb955350be706b9afd9b4955b3e55}
