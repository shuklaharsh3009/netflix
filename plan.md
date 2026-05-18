# SiyaFlix Optimization Plan

## Goal
Reduce load times, minimize data consumption, and improve playback smoothness.

---

## Phase 1: Asset Compression ✅ COMPLETE

### Results
- **528 images** converted from JPEG/PNG to WebP (~30% smaller)
- **528 thumbnails** generated (400px width, WebP)
- **EXIF orientation preserved** - images display correctly
- **All code updated** - script.js and style.css reference .webp files

### Tools Used
- Python Pillow (`ImageOps.exif_transpose()` for rotation fix)
- WebP format (Quality 85% for main, 75% for thumbnails)

---

## Phase 2: Video Compression (Pending)

### Action Required
Compress `intro.mp4` files to 720p H.264.

**Install FFmpeg:**
```bash
brew install ffmpeg
```

**Compress videos:**
```bash
find netflix -name "intro.mp4" -exec sh -c 'ffmpeg -i "$1" -vcodec libx264 -crf 28 -vf scale=1280:720 -acodec copy "${1%.mp4}_720p.mp4" && mv "${1%.mp4}_720p.mp4" "$1"' _ {} \;
```

---

## Phase 3: Code Optimization (Pending)

### 1. Preloading
Add to `playMedia()` in `script.js`:
```javascript
if (index + 1 < mediaList.length && !isVideo(mediaList[index + 1])) {
    const preloadImg = new Image();
    preloadImg.src = mediaList[index + 1];
}
```

### 2. Lazy Loading
Add to floating thumbnails in `initFloatingThumbnails()`:
```javascript
thumb.setAttribute('loading', 'lazy');
```

---

## Folder Structure
```
netflix/
├── main_bg.webp          # Background image
├── profiles/             # Profile photos
├── thumnails/            # Main card thumbnails (WebP)
├── thumbnails/           # Generated thumbnails (WebP)
├── series/
│   ├── GOA/
│   │   ├── intro.mp4     # Needs compression
│   │   ├── audio1.mp3
│   │   └── IMG_*.webp    # Converted images
```
