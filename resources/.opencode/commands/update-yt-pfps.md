---
name: update-yt-pfps
description: Update YouTube channel profile pictures for listed channels
---

# Synopsis

This command updates missing or outdated YouTube channel profile pictures (PFPs). It ensures each channel listed under a header has a linked PFP image.

Output is **exclusively for `youtube-channels.md`**. Do NOT edit `./youtube-videos.md`

# Steps

1. Identify YouTube channel links located under each listed header.
2. For each channel, obtain the PFP URL by running the following command in the terminal (replace `@RationalAnimations` with the actual channel handle):
   `curl -s "https://www.youtube.com/@Handle" | grep -oP 'https://yt3\.googleusercontent\.com/[^" *=]+(?=.*AVATAR_SIZE_XL)' | head -n 1`
3. Link the resulting image URL directly in the document. **Do not save the image file locally.**
    - Links for the PFP should be right after the header of the associated youtube channel
4. Repeat for all channels until all have a valid PFP link.

# Avoid:

- Do not download or save the image files to the filesystem; use the direct URL.
- Do not remove any existing text, metadata, or commentary associated with the channel headers.