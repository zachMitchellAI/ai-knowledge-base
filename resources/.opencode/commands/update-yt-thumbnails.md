---
name: update-yt-thumbnails
description: For the resources section, update any videos that do not have thumbnails
---

# Synopsis

This command checks to see if youtube thumbnails have been updated in @./youtube-videos.md . If there is a missing thumbnail, please update it!

# Steps

1. View each header indicating a youtube title
2. If there is a link to the video, but *not* a thumbnail, please append the thumbnail with the following format (top of the section):

```
| <Video Title> |
|-------------|
|![Thumbnail](https://i.ytimg.com/vi/dQw4w9WgXcQ/hqdefault.jpg)|
|https://youtu.be/dQw4w9WgXcQ|
```

(replace the video ID with the one mentioned in that markdown section)

3. If the video link is located on the bottom of the page, remove it, then put it in the table.
4. Repeat until all videos follow this format.

# Avoid:

- Please do not remove additional commentary from each section! This absolutely must stay, as it's cruicial for people to understand what the synopsis of each video is.