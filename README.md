# Steganography-with-Steghide-XAMPP
This project demonstrates how to use Steghide on Kali Linux to hide a secret message inside an image using steganography.
The hidden image is then transferred to a Windows host running XAMPP and displayed through a simple HTML web page.

The lab demonstrates:

Installing and verifying Steghide
Creating a secret text file
Embedding the secret into an image
Extracting the hidden message
Transferring the steganographic image to a Windows host
Serving the image using XAMPP
Displaying the image through HTML
Documenting the process with screenshots

⚠️ Lab disclaimer: This project is intended for educational purposes in a controlled environment. Only use files, systems, and web servers that you own or have permission to test.

🎯 Objectives

The objectives of this lab are to:

Understand the concept of steganography.
Verify that Steghide is installed on Kali Linux.
Create a text file containing a secret message.
Embed the secret message inside an image.
Verify that the message can be extracted.
Transfer the modified image to a Windows/XAMPP server.
Create an HTML page containing the image.
Serve the image using XAMPP.
Document the results with screenshots.
🧪 Lab Environment
Component	Description
Operating System	Kali Linux
Host Operating System	Windows
Web Server	XAMPP
Web Server Software	Apache
Steganography Tool	Steghide
Secret Message	gomycode
Image	index.jpeg
Secret File	my.txt
Lab Architecture
                  ┌─────────────────┐
                  │   Kali Linux    │
                  │                 │
                  │    Steghide     │
                  │       │         │
                  │       ↓         │
                  │  index.jpeg     │
                  │  + secret       │
                  └────────┬────────┘
                           │
                    Transfer Image
                           │
                           ↓
                  ┌─────────────────┐
                  │ Windows Host    │
                  │                 │
                  │     XAMPP       │
                  │      Apache     │
                  │        │        │
                  │        ↓        │
                  │   htdocs/       │
                  │   index.html     │
                  │   index.jpeg     │
                  └────────┬────────┘
                           │
                           ↓
                       Browser
                           │
                           ↓
                    Web Page Display
🧠 What Is Steganography?

Steganography is the practice of hiding information inside another file or medium so that the existence of the hidden information is not obvious.

For example:

Original Image
      +
Secret Message
      ↓
Steganography
      ↓
Image containing hidden message

The visible image can appear normal while containing additional hidden information.

Steganography vs Encryption

These are different concepts.

Encryption transforms readable information into ciphertext so that the information cannot easily be understood without the appropriate key.

Steganography attempts to hide the existence of the information itself.

They can also be used together:

Plaintext
   ↓
Encryption
   ↓
Ciphertext
   ↓
Steganography
   ↓
Image containing hidden ciphertext
🔧 1. Verify Steghide Installation

Open a terminal in Kali Linux and run:

steghide --version

If Steghide is installed, Kali should display its version information.

Example:

steghide version 0.5.1

The exact version displayed may differ depending on your Kali installation.

📦 2. Install Steghide

If Steghide is not installed, run:

sudo apt update

Then:

sudo apt install steghide

Verify the installation again:

steghide --version
📝 3. Create the Secret Message

Create a text file called:

my.txt

You can create it using:

nano my.txt

Enter:

gomycode

Save the file.

You can verify the contents with:

cat my.txt

Expected output:

gomycode
File Structure

At this point, your working directory should contain:

my.txt
index.jpeg
🖼️ 4. Choose an Image

Select an image supported by Steghide.

For this project, we use:

index.jpeg

Verify that the file exists:

ls -l index.jpeg

You can also check the file type:

file index.jpeg
🔐 5. Embed the Secret Message

The command in the original instructions appears to have a small syntax issue.

The standard Steghide syntax is:

steghide embed -cf index.jpeg -ef my.txt

Where:

Option	Meaning
embed	Embed data into a cover file
-cf	Specifies the cover file
index.jpeg	The image used to hide the data
-ef	Specifies the embedded file
my.txt	File containing the secret

Run:

steghide embed -cf index.jpeg -ef my.txt

Steghide may ask you to create a passphrase.

Enter a passphrase when prompted.

The image now contains the hidden file.

📸 6. Screenshot — Embedding Process

Take a screenshot showing the terminal and the Steghide embedding process.

Recommended screenshot filename:

screenshots/steghide-embed.png

GitHub Markdown:

## Steghide Embedding


![Steghide Embedding](screenshots/steghide-embed.png)
🔍 7. Verify the Embedded Data

Before transferring the image to the XAMPP server, verify that Steghide recognizes the embedded data.

Run:

steghide info index.jpeg

You should see information indicating that an embedded file exists.

For example:

embedded file "my.txt"

The exact output may vary depending on your Steghide version and image.

🔓 8. Extract the Hidden Message

To test the reverse operation, use:

steghide extract -sf index.jpeg

Where:

Option	Meaning
extract	Extract embedded data
-sf	Specifies the stego file
index.jpeg	Image containing the hidden data

If you created a passphrase during embedding, Steghide will ask you to enter it.

After successful extraction, check:

cat my.txt

Expected result:

gomycode

This confirms that the hidden message can be recovered from the image.

📸 9. Screenshot — Extraction

Take a screenshot showing the extraction process.

Recommended filename:

screenshots/steghide-extract.png

Example:

## Extracting the Hidden Message


![Steghide Extraction](screenshots/steghide-extract.png)
🌐 10. Serve the Steganographic Image Using XAMPP

The next stage of the project is to transfer the steganographic image from Kali Linux to the Windows host.

The Windows machine will use XAMPP/Apache to serve the image through a web page.

Workflow
Kali Linux
    |
    | index.jpeg
    ↓
Windows Host
    |
    ↓
XAMPP
    |
    ↓
Apache
    |
    ↓
htdocs
    |
    ↓
Browser
📁 11. Transfer the Image to Windows

Transfer:

index.jpeg

from Kali Linux to your Windows host.

Possible methods include:

VMware shared folders
Drag and drop
Shared folders
SCP/SSH
Other authorized file-transfer methods

After transferring the image, confirm that it exists on Windows.

🗂️ 12. Copy the Image to XAMPP

Locate the XAMPP web root.

A common Windows XAMPP installation uses:

C:\xampp\htdocs\

Copy:

index.jpeg

into:

C:\xampp\htdocs\

Your directory should look similar to:

C:\xampp\htdocs\
│
├── index.html
└── index.jpeg
🚀 13. Start Apache in XAMPP

Open the XAMPP Control Panel.

Start:

Apache

The Apache service should show as running.

Example:

Apache    Running

If Apache does not start, check whether another application is already using port 80 or the configured Apache port.

📝 14. Create the HTML Page

Create or edit:

C:\xampp\htdocs\index.html

Example HTML:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Steganography Project</title>
</head>


<body>


    <h1>Your Name</h1>


    <h2>AES Encrypted Message</h2>


    <p>
        Your AES encrypted message goes here.
    </p>


    <h2>Steganographic Image</h2>


    <img src="index.jpeg"
         alt="Steganographic image"
         width="600">


</body>
</html>

Replace:

Your Name

with your name.

Replace the placeholder:

Your AES encrypted message goes here.

with the AES-encrypted message required by your assignment.

🌍 15. Open the Web Page

Open a browser on the Windows host and navigate to:

http://localhost

Alternatively:

http://127.0.0.1

Apache should serve the index.html file from the XAMPP htdocs directory.

🖥️ Expected Web Page

The page should contain:

┌─────────────────────────────────────┐
│           Your Name                 │
│                                     │
│     AES Encrypted Message           │
│                                     │
│     [Encrypted Message]             │
│                                     │
│     Steganographic Image            │
│                                     │
│        ┌───────────────┐            │
│        │               │            │
│        │   index.jpeg  │            │
│        │               │            │
│        └───────────────┘            │
│                                     │
└─────────────────────────────────────┘

The image displayed by the browser is the same image containing the hidden my.txt data.

📸 16. Final Screenshot

Take a screenshot of the rendered webpage.

Recommended filename:

screenshots/final-webpage.png

Add it to your README:

## Final XAMPP Web Page


![Final Web Page](screenshots/final-webpage.png)
🔬 17. Verification

The project should be verified at several stages.

Verification 1 — Steghide Installation
steghide --version

Result: Steghide is installed and available.

Verification 2 — Secret File
cat my.txt

Expected:

gomycode
Verification 3 — Embedded Data
steghide info index.jpeg

Result: The image contains embedded data.

Verification 4 — Extraction
steghide extract -sf index.jpeg

Then:

cat my.txt

Expected:

gomycode
Verification 5 — Web Server

Open:

http://localhost

Result: The HTML page and steganographic image are displayed.

🔐 Security Analysis

This lab demonstrates an important security concept: a file can contain information that is not immediately visible to a user.

The image can look like an ordinary JPEG while containing an embedded file.

Visible Layer
     ↓
┌───────────────┐
│    IMAGE      │
└───────────────┘


Hidden Layer
     ↓
┌───────────────┐
│   my.txt      │
│   gomycode    │
└───────────────┘

The hidden information is not visible simply by opening the image normally.

🛡️ Security Considerations

Steganography can be used for legitimate purposes, such as:

Digital watermarking
Copyright protection
Privacy research
Security research
Educational demonstrations

It can also be abused to conceal information inside seemingly harmless files.

For this reason, organizations may use security monitoring and file-analysis tools to detect suspicious files.

Defensive Measures

Organizations can consider:

File-type validation
Malware scanning
Email attachment scanning
Endpoint Detection and Response (EDR)
Data Loss Prevention (DLP)
Network monitoring
File integrity monitoring
User awareness training
🧪 Complete Command Reference
Check Steghide
steghide --version
Install
sudo apt update
sudo apt install steghide
Create Secret
nano my.txt

Contents:

gomycode
Verify Secret
cat my.txt
Embed
steghide embed -cf index.jpeg -ef my.txt
Check Embedded Data
steghide info index.jpeg
Extract
steghide extract -sf index.jpeg
Verify Extracted Message
cat my.txt
📁 Recommended GitHub Repository Structure
steghide-xampp-lab/
│
├── README.md
│
├── files/
│   └── my.txt
│
├── images/
│   └── index.jpeg
│
├── web/
│   └── index.html
│
└── screenshots/
    ├── steghide-version.png
    ├── steghide-embed.png
    ├── steghide-info.png
    ├── steghide-extract.png
    └── final-webpage.png

Do not commit real passwords, private keys, confidential messages, or sensitive data to GitHub. For this lab, gomycode is fine as a demonstration secret.

📊 Project Workflow
                 START
                   │
                   ▼
          Check Steghide
                   │
                   ▼
            Create my.txt
                   │
                   ▼
          Add "gomycode"
                   │
                   ▼
          Select index.jpeg
                   │
                   ▼
        Steghide Embed
                   │
                   ▼
       Hidden Message Created
                   │
                   ▼
        Steghide Extraction
                   │
                   ▼
        Verify "gomycode"
                   │
                   ▼
       Transfer index.jpeg
                   │
                   ▼
          Windows Host
                   │
                   ▼
             XAMPP/Apache
                   │
                   ▼
             htdocs/
                   │
                   ▼
            index.html
                   │
                   ▼
              Browser
                   │
                   ▼
        Final Web Page
                   │
                   ▼
                  END
📝 Conclusion

This project demonstrated how Steghide can be used to embed a secret text file inside a JPEG image and subsequently extract the hidden information.

The steganographic image was then transferred to a Windows host and served through XAMPP/Apache as part of an HTML webpage.

The complete process was:

Create Secret
      ↓
Embed Secret
      ↓
Verify Hidden Data
      ↓
Extract Secret
      ↓
Transfer Image
      ↓
XAMPP
      ↓
Apache
      ↓
HTML
      ↓
Browser

This lab provides practical experience with steganography, Linux security tools, file transfer, Apache/XAMPP, HTML, and basic security analysis
