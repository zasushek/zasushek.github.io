---
title: "We lost the flag"
date: 2025-04-28 9:52:00 +02:00
categories: [Writeups, CIT, forensics]
tags: [CIT_CTF, forensics]
---

# We Lost the Flag - Forensics Write-up

## Challenge Overview
In this forensics challenge, we were provided with a single file named `lost.png`. The goal was to recover the hidden flag concealed within the file. However, the file wouldn't open as a standard PNG image, hinting at a deeper issue with its format or structure.

## Initial Analysis
I began by downloading the file and attempting to open it with an image viewer, but it failed to render. This suggested that the file might not be a valid PNG or could be corrupted.

To investigate further, I used the `file` command to inspect the file's type:

```bash
file lost.png
```

The output revealed that the file was identified as `data` rather than a PNG image:

![File command output](images/CIT/we_lost_the_flag_2.png)

This discrepancy between the `.png` extension and the file's actual content indicated that the file extension was likely incorrect or intentionally misleading.

## Digging Deeper: Magic Bytes
To determine the true file format, I examined the file's **magic bytes**—the initial bytes that define a file's signature. Magic bytes are unique identifiers for specific file types (e.g., PNG, JPEG). A useful resource for file signatures is [Wikipedia's List of File Signatures](https://en.wikipedia.org/wiki/List_of_file_signatures).

Using `hexedit`, I opened the file to inspect its hexadecimal content:

```bash
hexedit lost.png
```

The first few bytes were:

![Hexedit initial bytes](images/CIT/we_lost_the_flag_3.png)

Comparing these bytes to known file signatures, they did not match the PNG signature (`89 50 4E 47 0D 0A 1A 0A`). Instead, the bytes suggested a different format. Upon closer inspection, I noticed the string `JFIF` in the decoded ASCII portion of the file:

![JFIF string in hexedit](images/CIT/we_lost_the_flag_4.png)

The presence of `JFIF` (JPEG File Interchange Format) strongly indicated that the file was actually a JPEG image, not a PNG. The correct magic bytes for a JPEG file are typically `FF D8 FF`.

## Fixing the File
To make the file recognizable as a JPEG, I modified the initial bytes to match the JPEG signature using `hexedit`. Alternatively, I could have simply renamed the file to `lost.jpg` to test if the image viewer could parse it correctly.

After renaming the file to `lost.jpg` (or correcting the magic bytes), I successfully opened the image:

![Correctly opened image](images/CIT/we_lost_the_flag_5.png)

The image revealed the flag, completing the challenge.

## Conclusion
This challenge tested our ability to identify and correct a mislabeled file format. By analyzing the file's magic bytes and recognizing the `JFIF` signature, we determined that `lost.png` was actually a JPEG image. Renaming the file or fixing its header allowed us to recover the flag. This is a classic forensics task that emphasizes the importance of understanding file signatures and using tools like `file` and `hexedit` to uncover hidden data.

**Flag**: `CIT{us1ng_m4g1c_1t_s33m5}`

## Tools Used
- `file`: To check the file type.
- `hexedit`: To inspect and modify the file's hexadecimal content.
- Image viewer: To verify the corrected image.

## Tips for Similar Challenges
- Always verify file extensions with the `file` command.
- Check magic bytes to confirm a file's true format.
- Use resources like the [List of File Signatures](https://en.wikipedia.org/wiki/List_of_file_signatures) to identify unknown file types.
- If a file doesn't open, consider renaming it to match its actual format or editing its header.