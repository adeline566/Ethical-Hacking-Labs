                                  Steganography Using Steghide 



# Overview

In this lab, I explored steganography techniques using Steghide in Kali Linux. The objective was to hide a secret text file inside an image, verify file integrity using hash values, extract the hidden data, and modify image metadata using ExifTool. This exercise demonstrated how information can be concealed within seemingly innocent files and how metadata changes affect file integrity.


## Step 1: Install Gedit

I opened the Kali Linux terminal and installed Gedit using:

* sudo apt install gedit


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/1f2f76ff-4d68-466a-8cc4-7bfd377c18d7" />



## Step 2: Create a Working Directory

I created a new directory named stegDir to store all files used throughout the lab.

* mkdir stegDir

<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/4a30c45f-d828-4887-b584-60e1b3741bcd" />


## Step 3: Create a Secret Text File

I navigated to the new directory and created a file named testfile.txt.

* cd stegDir
* touch testfile.txt

<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/20c89128-aefb-46d2-bd73-b82d2767b366" />



## Step 4: Add a Secret Message

I opened the text file using Gedit and entered a secret message that would later be hidden inside an image.

* gedit testfile.txt


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/4bc53e3b-6d31-4092-a1f2-8bcc60de6730" />



## Step 5: Download an Image

I downloaded a dog image using Firefox and saved it as dog.jpeg.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/efe61d9b-801d-49bc-b499-a405f90b34a4" />



## Step 6: Copy the Image to the Working Directory

I copied the image from the Downloads folder into the stegDir directory.

* cp ~/Downloads/dog.jpeg .
* ls

##### The directory now contained:

* testfile.txt
* dog.jpeg


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/3acc5986-c44c-42a1-958a-ae572fc85b54" />



## Step 7: Generate Initial MD5 Hashes

I generated MD5 checksums for both files.

* md5sum testfile.txt dog.jpeg


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/6fbbea0e-6220-4be0-9a32-e997e5260ee0" />



## Step 8: Embed the Secret File into the Image

Using Steghide, I embedded the text file into the image and protected it with a passphrase.

* steghide embed -cf dog.jpeg -ef testfile.txt

After entering a passphrase, Steghide successfully hid the text file inside the image.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/3b688f38-fa6b-4e7a-916d-bff5cde0e510" />



## Step 9: Verify the Image Hash After Embedding

I generated a new MD5 hash for the image.

* md5sum dog.jpeg

The hash value changed after embedding the hidden file, confirming that the image data had been modified.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/bbd3dd13-e55c-4a9b-83ae-7a594c51cfad" />


#### Hash Comparison

Stage	MD5 Hash

* Before Embedding	710893b83fc1186f2827b9fc1b2b1449
* After Embedding	71faff68e3f03eb657189f79f49b8cd7

The difference in hashes confirms that the image contents changed after the hidden file was embedded.



## Step 10: View Embedded File Information

I used the Steghide info command to inspect the image.

* steghide info dog.jpeg

The output showed that the image contained embedded data.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/82af1fc4-008c-49f0-80cb-36214f29a312" />



## Step 11: Delete the Original Text File

To demonstrate successful recovery later, I deleted the original text file.

* rm testfile.txt
* ls

Only the image remained in the directory.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/5b190dac-570f-497a-9e90-61dd17ecf4a7" />



## Step 12: Extract the Hidden File

I extracted the hidden file from the image.

* steghide extract -sf dog.jpeg

After entering the correct passphrase, the file was successfully recovered.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/9f8e3c9f-e183-492c-a223-af7733e71236" />



## Step 13: Verify File Recovery

I listed the directory contents again.

* ls

The extracted file testfile.txt reappeared in the directory.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/f3ed1f54-1d48-48ba-9a9a-ba0ec8b0fb63" />



## Step 14: View the Extracted Message

I opened the recovered file to verify that the secret message remained intact.

* gedit testfile.txt

The original message was successfully restored.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/f3a5789c-7b04-4643-ad2d-7cdc358c5e29" />


## Step 15: Examine Image Metadata

I viewed the metadata stored within the image using ExifTool.

* exiftool dog.jpeg


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/0ee22b34-3039-46c3-b6d2-591511d3f260" />




## Step 16: Modify the Author Metadata

I changed the image author information using ExifTool.

exiftool -Author="Your Name" dog.jpeg

<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/1d027b5d-1ffc-4707-9298-b8232e1bef11" />


## Step 17: Verify Updated Metadata

I displayed the metadata again to verify the change.

exiftool dog.jpeg

The Author field reflected the new value.

<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/825cc2f3-51f3-46c2-b3a3-d54d9caa4810" />


## Step 18: Verify Hash Changes After Metadata Modification

I generated another MD5 hash for the image.

* md5sum dog.jpeg

The hash value changed again because modifying metadata alters the file contents.

#### Final Hash Comparison

* Stage	MD5 Hash

#### Before Embedding	
<img width="400" height="112" alt="image" src="https://github.com/user-attachments/assets/e10bb76b-64e2-46c6-be64-c57af3bd1034" />



#### After Embedding	
<img width="365" height="74" alt="image" src="https://github.com/user-attachments/assets/94dbcfd5-edf5-48f8-b661-a43d5a8d7c9c" />



The results demonstrate that both embedded data and metadata modifications affect the file's hash value.





# Lessons Learned

This lab taught me that steganography allows information to be hidden inside ordinary files such as images without making the hidden content immediately visible. I learned how to use Steghide to securely embed and extract files using a passphrase. I also observed that changes made to a file, whether through hidden data insertion or metadata modification, result in different hash values. This reinforced the importance of hashing as a method for verifying file integrity. Additionally, I learned how metadata can be viewed and modified using ExifTool, which highlighted the role metadata plays in digital forensics investigations. Overall, this lab provided practical experience with steganography, file integrity verification, and metadata analysis within a Kali Linux environment.
