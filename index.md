---
layout: default
title: Vevioz Downloader API
description: Official Vevioz MP3/MP4 downloader API integration examples for iframe, JavaScript SDK and REST API.
---

# Vevioz Downloader API

The current Vevioz API is available at **[api.vevioz.com](https://api.vevioz.com/)**.

## Try the live consumer service

**[Download Lagu MP3](https://download-lagu-mp3.com/)** is the ready-to-use Vevioz consumer downloader experience. Use it when you want the web interface without integrating the API yourself.

Vevioz provides three integration paths for developers:

1. **Responsive downloader iframe** for the fastest implementation.
2. **JavaScript Button SDK** for an inline MP3/MP4 download experience.
3. **REST API v1** for custom applications and front ends.

## REST API v1

```text
GET  https://api.vevioz.com/api/v1/info?url=YOUTUBE_URL
POST https://api.vevioz.com/api/v1/jobs
GET  https://api.vevioz.com/api/v1/jobs/{job_id}?token=ACCESS_TOKEN
GET  https://api.vevioz.com/api/v1/status
```

## Quick JavaScript integration

```html
<button id="download" type="button">Download MP3/MP4</button>
<script src="https://api.vevioz.com/static/vevioz-download-button.js?v=6"></script>
<script>
VeviozDownloadButton.bind(document.getElementById("download"), {
  url: "https://www.youtube.com/watch?v=YOUTUBE_VIDEO_ID"
});
</script>
```

### Official resources

- **[Open Vevioz Downloader API](https://api.vevioz.com/)**
- **[Check API status](https://api.vevioz.com/status)**
- **[Try Download Lagu MP3](https://download-lagu-mp3.com/)**
- **[Visit Vevioz](https://www.vevioz.com/)**

For the latest integration instructions, examples, formats, and API behavior, use the official API website above.
