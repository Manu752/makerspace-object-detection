# makerspace-object-detection

> **Project Year: 2024**  
> YOLO-based object detection application for workshop tools, electronic components, PCBs and other makerspace objects.

A client-side, zero-server computer vision application for detecting, classifying, and cataloging makerspace items (hand tools, electronic modules, passive components, PCBs, hardware fasteners, materials). Runs real-time inference directly in the browser via WebAssembly (ONNX Runtime Web with SIMD acceleration).

---

## Key Features

- **Client-Side Edge Inference**: Executes a trained `YOLO11n` ONNX model (`yolo11n_makerspace.onnx`) client-side inside a Web Worker with multi-threaded WASM SIMD acceleration (`ort-wasm-simd-threaded.wasm`). No server or GPU required.
- **Multiple Video Input Modes**: Live webcam feed, pre-recorded conveyor-belt demo (`demo_belt.mp4`), or custom video file upload.
- **Live Inventory & Item Detail**: Automatic item deduplication, confidence filtering, bounding box rendering, and inventory logging.
- **Cited Retrieval (Lexical Corpus Search)**: Verbatim German and English reference database (`corpus/`) for recycling and reuse instructions, material separation, and disposal regulations.
- **Complete Full-Stack Architecture**: Contains both the browser-mode frontend GUI and backend training / FastAPI pipeline modules.

---

## Quick Start & Execution

### 1. Run the Browser Detector
Serve the web application locally:
```bash
# Using Node / npm
npm install
npm start
# Opens at http://localhost:3000

# Or using Python 3
python3 -m http.server 3000
```
Open `http://localhost:3000` in any modern browser with WebAssembly support (Chrome, Firefox, Safari, Edge).

### 2. Python Backend & Model Training
To train or re-export YOLO11 models:
```bash
pip install -r requirements.txt

# Start local FastAPI backend (optional)
uvicorn api.main:app --host 0.0.0.0 --port 8000

# Export YOLO11 model to ONNX format
python3 scripts/export_onnx.py --weights models/yolo11n.pt --output yolo11n_makerspace.onnx
```

---

## Repository Structure

```
.
├── index.html            # Browser application entry point
├── yolo11n_makerspace.onnx # Trained YOLO11n ONNX model weights
├── ort-wasm-simd-threaded.wasm # ONNX Runtime WebAssembly binary
├── assets/               # Built web application bundle, styles, and worker
├── corpus/               # Multilingual reuse and recycling reference guides
├── examples/             # Sample conveyor-belt frame images
├── screenshots/          # Application preview screenshots
├── demo_belt.mp4         # Sample conveyor-belt evaluation video
├── demo_slideshow.mp4    # Sample detection slideshow
├── api/                  # FastAPI backend server implementation
├── training/             # Ultralytics YOLO training and fine-tuning pipelines
├── web/                  # React frontend source code
├── package.json          # Node server dependencies
├── requirements.txt      # Python dependencies
└── Makefile              # Automation tasks
```

---

## Model Weights & Licensing

- **Code**: Licensed under the [MIT License](LICENSE).
- **YOLO Model Weights**: The trained YOLO11n weights (`yolo11n_makerspace.onnx`) are licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
