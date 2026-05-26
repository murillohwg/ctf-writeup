# Writeup - CanYouSee
> This challenge involved analyzing metadata hidden inside an image file.

---

## Files

```bash
ukn_reality.jpg
```

---

## Initial Analysis

The first step was simply opening the image.

![image](assets/1-ctf-image.jpg)

Nothing suspicious was visible directly in the image, so the next step was checking the metadata.

---

## Using ExifTool

To inspect the image metadata, I used:

```bash
exiftool ukn_reality.jpg
```

Output:

![image](assets/2-using-exiftool.png)

While inspecting the metadata, one field immediately stood out:

```txt
Attribution URL : cGljb0NURntNRTc0RDQ3QV9ISUREM05fNmE5ZjVhYzR9Cg==
```

The value looked like Base64.

---

## Decoding the String

I decoded the string using:

```bash
echo "cGljb0NURntNRTc0RDQ3QV9ISUREM05fNmE5ZjVhYzR9Cg==" | base64 -d
```

Result:

![image](assets/3-decode-base64-found-FLAG.png)

The decoded output revealed the flag.

---

## Flag

```txt
picoCTF{ME74D47A_H1DD3N_6a9f5ac4}
```

---

## Tools Used

- ExifTool
- base64
- Linux Terminal

---

## Concepts

- Metadata fields can hide sensitive or important information.
- `exiftool` is extremely useful for forensic and steganography-related CTF challenges.
- Base64 is commonly used to obfuscate flags in beginner challenges.
