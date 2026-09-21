# Vevioz Downloader API — MP3/MP4 Video Downloader API

**Official API:** https://api.vevioz.com/  
**Service status:** https://api.vevioz.com/status

Vevioz Downloader API provides a public integration layer for websites and applications that need video metadata, available formats, MP3 audio, MP4 video, download jobs, or a ready-made downloader interface.

**Version 1 is live.**

## Integration options

- **Responsive iframe** — fastest way to add the complete downloader UI.
- **JavaScript Button SDK** — renders formats, verification, progress, and the final file link directly on your page.
- **REST API** — structured JSON endpoints for custom websites, apps, and workflows.

## JavaScript Button SDK

```html
<button id="download" type="button">Download MP3/MP4</button>

<script src="https://api.vevioz.com/static/vevioz-download-button.js?v=6"></script>
<script>
  VeviozDownloadButton.bind(document.getElementById("download"), {
    url: "https://www.youtube.com/watch?v=YOUTUBE_VIDEO_ID"
  });
</script>
```

## Responsive iframe

```html
<iframe
  id="vevioz-api"
  src="https://api.vevioz.com/YOUTUBE_VIDEO_ID"
  title="Vevioz Downloader"
  loading="lazy"
  referrerpolicy="strict-origin-when-cross-origin"
  allow="clipboard-write"
  sandbox="allow-scripts allow-forms allow-downloads allow-same-origin allow-popups allow-popups-to-escape-sandbox"
  style="width:100%;height:720px;border:0">
</iframe>

<script>
window.addEventListener("message", function (event) {
  var frame = document.getElementById("vevioz-api");
  if (event.origin !== "https://api.vevioz.com" || event.source !== frame.contentWindow) return;

  if (event.data.type === "vevioz-api-resize") {
    frame.style.height = Math.min(1800, Math.max(320, event.data.height)) + "px";
  }

  if (event.data.type === "vevioz-api-capabilities-request") {
    event.source.postMessage({
      type: "vevioz-api-capabilities",
      sandbox: frame.hasAttribute("sandbox") ? Array.from(frame.sandbox) : null
    }, event.origin);
  }

  if (event.data.type === "vevioz-api-download" && typeof event.data.url === "string") {
    var download = new URL(event.data.url, "https://api.vevioz.com");
    if (
      download.origin === "https://api.vevioz.com" &&
      download.pathname.indexOf("/api/v1/files/") === 0
    ) {
      window.location.assign(download.href);
    }
  }
});
</script>
```

## REST API v1

Current public endpoints:

```text
GET  /api/v1/info?url=YOUTUBE_URL
POST /api/v1/jobs
GET  /api/v1/jobs/{job_id}?token=ACCESS_TOKEN
GET  /api/v1/status
```

Typical workflow:

1. Read video metadata and available formats with `/api/v1/info`.
2. Create a download job with `/api/v1/jobs`.
3. Poll the job endpoint until the secure file URL is ready.

The API returns the formats available for the selected video; applications should display only the formats returned by the metadata response.

## Why use Vevioz API?

- First-party infrastructure operated by Vevioz.
- MP3 audio and MP4 video support.
- Responsive embed for fast integrations.
- REST endpoints for custom front ends.
- Metadata caching, bounded workers, automatic cleanup, and explicit error handling.
- Public service-status page.

## Links

- **Official Vevioz Downloader API:** https://api.vevioz.com/
- **API status:** https://api.vevioz.com/status
- **Vevioz:** https://www.vevioz.com/

Use the service only for media you are authorized to access or download and comply with applicable platform terms and laws.
