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

## Phase 2: Video Compression ✅ COMPLETE

### Results
- **7 intro videos** compressed to 720p H.264
- **Total size reduced:** ~95MB → ~18MB (**80% savings**)
- **Quality:** High (CRF 28), compatible with all browsers
- **Audio:** Preserved (no re-encoding)

### Details
| File | Before | After |
|------|--------|-------|
| Banaras | 21M | 3.0M |
| Coorg | 23M | 4.0M |
| GOA | 13M | 4.3M |
| Mahabaleshwar | 12M | 2.0M |
| Mathura | 13M | 2.0M |
| Dapoli | 6.0M | 956K |
| Matheran | 7.4M | 2.0M |

---

## Phase 3: Code Optimization ✅ COMPLETE

### 1. Preloading Next 3 Images
- Added loop in `playMedia()` to preload the next 3 images in the background.
- Eliminates transition delays between slides.

### 2. Lazy Loading
- Added `loading="lazy"` to floating thumbnails on the profile screen.
- Reduces initial page load time and data usage.

### 3. Performance Tweaks
- Smoother playback experience with pre-cached images.
- Reduced memory footprint by not loading all thumbnails at once.

---

## Final Folder Structure
```
netflix/
├── main_bg.webp          # Background image
├── profiles/             # Profile photos
├── thumnails/            # Main card thumbnails (WebP)
├── thumbnails/           # Generated thumbnails (WebP)
├── series/
│   ├── GOA/
│   │   ├── intro.mp4     # Compressed 720p
│   │   ├── audio1.mp3
│   │   └── IMG_*.webp    # Converted images
```

## Execution Checklist
- [x] Install conversion tools (Pillow via pip).
- [x] Run batch conversion for Images (JPEG -> WebP with EXIF orientation fix).
- [x] Run batch conversion for Thumbnails (Resize + WebP).
- [x] Compress all `intro.mp4` files to 720p (FFmpeg).
- [x] Update `script.js` DATA object with new paths/extensions.
- [x] Add Preloading logic to `playMedia` (Next 3 images).
- [x] Add Lazy Loading to floating thumbnails.
- [x] Test playback speed and data usage.
