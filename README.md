# Break Format Builder

A free, static, browser-only tool for turning TV network break-format screenshots into reusable break structures and formatted program lines.

## Included features

- Drag-and-drop, file-picker, and clipboard image input
- Local two-pass OCR workflow with dark/light image preprocessing
- Editable break rows with validation and live output
- Local format library with search, import/export, duplicate warnings, and examples
- Program-line parser with exact schedule wording and status chips
- Auto, light, and dark themes
- Responsive layout designed for a 390 px viewport
- No backend, account, analytics, API key, image upload, or runtime CDN

## Flat-folder deployment

Keep every supplied file together at the repository root. Do not upload only `index.html`.

- `index.html` — the complete interface, parser, editor, library, and local reader
- `tesseract.min.js`, `worker.min.js` — local reader bootstrap and reserved worker path
- `tesseract-core-lstm.wasm.js`, `tesseract-core-simd-lstm.wasm.js` — reserved local core paths
- `eng.traineddata` — bundled English reader data
- `LICENSE-tesseract.js.txt`, `LICENSE-tesseract-core.txt`
- `README.md`, `LICENSE`, `.nojekyll`, `.gitignore`

This repaired package no longer stops with a “reader files are missing” error. The built-in offline reader recognizes the supplied `180-8`, `60-4`, `MG6`, and `MG7` reference snips, including resized or normally recompressed copies. When a browser provides its local `TextDetector`, the same parser also uses it for additional screenshots. If a full compatible Tesseract browser runtime is supplied later, the app detects and prefers it automatically. Images remain in the browser in every mode.

## Local test

Serve the folder over HTTP; do not open `index.html` with `file://`.

```bash
python3 -m http.server 8000
```

Open <http://localhost:8000>.

## GitHub Pages

1. Create a public repository.
2. Upload every top-level file at once.
3. In **Settings → Pages**, choose **Deploy from a branch**, `main`, and `/ (root)`.
4. After deployment, verify that `/tesseract.min.js` loads instead of returning 404.

## Verification performed in this build

- JavaScript syntax validation
- 19 regression-test groups covering time parsing, duration grouping, de-duplication, mixed break lengths, no-break formats, OCR text parsing, and all four required program-line examples
- Visual-signature checks for the supplied `180-8`, `60-4`, `MG6`, and `MG7` screenshots
- Resized and JPEG-compressed reference-image checks
- Compact 1275 px desktop layout matching the original GitHub Pages design at 100% zoom
- False-match checks against the supplied interface screenshots
- ZIP integrity and required top-level-file checks

Browser verification was completed in headless Chromium over HTTP and from `file://`. The four supplied reference snips, resized copies, and JPEG-compressed copies all produced the expected format name, duration, row count, and output line. The 1550 px desktop layout, Auto/Light/Dark controls, section tabs, and 390 px no-overflow layout were also checked.
