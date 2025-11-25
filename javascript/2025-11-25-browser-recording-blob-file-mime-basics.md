# TIL: Blob / File / MIME and Browser Recording Fundamentals

## 1. Basics of Blob / File / MIME

Three key concepts to understand before diving into browser recording:

### Blob = "A chunk of data in memory"

- Not a file
- Has no name
- Exists temporarily in memory
- MediaRecorder output (chunks) becomes a Blob when combined

### File = "Blob + filename + MIME type"

To generate a file in the browser:

```javascript
const file = new File([blob], "recording.webm", {
  type: "audio/webm",
});
```

- File encapsulates a Blob
- Use File for uploads (not Blob)

### MIME type = "A label indicating data format"

Examples:

- `audio/webm`
- `video/webm`
- `image/png`
- `application/json`

The server validates based on MIME type, so incorrect File type will cause upload failures.

---

## 2. Flow: MediaRecorder → Blob → File

Browser recording follows this flow:

```
MediaRecorder chunks
        ↓
    Blob (raw data)
        ↓ wrap with File()
File (completed WebM audio)
        ↓
  send via multipart/form-data
```

**Note:** Sending raw Blob often corrupts MIME type. Always convert to File before uploading.

---

## 3. Centralizing onstop for Stable Recording

Recording stop can originate from multiple sources:

- User clicks Stop button
- Browser UI "Stop Sharing"
- `MediaStreamTrack.onended` (screen share disconnected)

Scattered logic causes bugs. The correct design centralizes all logic in `MediaRecorder.onstop`.

Example:

```javascript
stream.getTracks().forEach(track => {
  track.onended = () => {
    const mr = mediaRecorderRef.current;
    if (mr && mr.state !== "inactive") mr.stop();
  };
});
```

---

## 4. Correct Way to Add to FormData and Upload

```javascript
const blob = new Blob(chunks, { type: "audio/webm" });

const file = new File([blob], `recording_${Date.now()}.webm`, {
  type: "audio/webm",
});

const fd = new FormData();
fd.append("file", file);

await fetch("/api/upload", { method: "POST", body: fd });
```

---

## 5. Today's Learnings (Summary)

- Blob is "a chunk of data in memory," not a file
- File is "the evolved form of Blob with name + MIME"
- Server uploads should use File, not raw Blob
- Incorrect MIME type will cause API rejection
- Recording stop has multiple entry points, so logic should be centralized in onstop
- Download raw file and test with curl for faster troubleshooting

---

## Additional Tips

### Identifying File vs Blob

```javascript
if (file instanceof File) // true
if (blob instanceof Blob) // true
```

### FormData Append with Optional Filename

```javascript
fd.append("file", file, file.name); // explicitly specify filename
```

### Debug with curl

1. Save File locally (using browser download)
2. Test API upload with curl
3. Compare behavior: browser vs curl → faster root cause analysis

---

## Common Pitfalls

- **Missing MIME type** → API rejects as "invalid format"
- **Chunk ordering or ondataavailable timing** → corrupted Blob
- **Upload failures** → check: type/filename, FormData structure, fetch headers
