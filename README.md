# LIA (Latent Image Animator) - Modified for Easy Use

**Forked from:** [wyhsirius/LIA](https://github.com/wyhsirius/LIA)

This is a modified version of the LIA (Latent Image Animator) project that makes it easy to animate still images using Google Colab.

## What This Project Does

Animates a **still image** (like a portrait photo) using motion from a **driving video**. The result is a video where your still image moves, speaks, or acts according to the motion in the driving video.

**Example Use Case:**
- **Input:** Your portrait photo + a video of someone talking
- **Output:** Your photo animated to look like it's talking!

## My Modifications

### 1. **PyTorch Compatibility Fix**
Fixed a critical bug in `run_demo.py` for PyTorch 2.0+ compatibility:
```python
# Original (causes error):
weight = torch.load(model_path, map_location=lambda storage, loc: storage)['gen']

# Fixed version:
weight = torch.load(model_path, map_location=lambda storage, loc: storage, weights_only=False)['gen']
```

### 2. **Google Colab Integration**
Created `LIA_COLAB.ipynb` notebook for easy cloud-based execution with:
- Automated setup and dependency installation
- Automatic model download from Google Drive
- GPU acceleration (free via Google Colab)
- No local installation required

### 3. **Interactive Interface**
Added user-friendly file upload interface:
- Upload your own source image
- Upload your own driving video
- Process and download results with one click
- Real-time progress indicators

### 4. **CPU Support** 
Modified `run_demo.py` to automatically detect and use available hardware (GPU or CPU)

## How to Use

### Option 1: Google Colab (Recommended - No Setup Required!)

1. Open `LIA_COLAB.ipynb` in Google Colab
2. Click **Runtime → Run all** (or run cells sequentially)
3. Wait for setup to complete (~2 minutes)
4. See the demo animation with the provided sample
5. **For your own images:**
   - Scroll to the interactive section
   - Upload your source image when prompted
   - Upload your driving video when prompted
   - Wait 2-5 minutes for processing
   - Download your animated result automatically!

**Colab provides free GPU access, making processing much faster than local CPU execution.**

### Option 2: Local Installation

**Requirements:**
- Python 3.7+
- PyTorch 1.5+
- CUDA-capable GPU (recommended) or CPU

**Setup:**
```bash
# Clone the repository
git clone https://github.com/Vineela-10/CCN_LIA_Final.git
cd CCN_LIA_Final

# Install dependencies
pip install torch torchvision av tqdm lpips moviepy imageio-ffmpeg

# Download pre-trained models
# Download from: https://drive.google.com/drive/folders/1N4QcnqUQwKUZivFV-YeBuPyH4pGJHooc
# Place the .pt files in ./checkpoints/
```

**Run Demo:**
```bash
python run_demo.py --model vox --source_path ./data/vox/macron.png --driving_path ./data/vox/driving1.mp4
```

**Use Your Own Files:**
```bash
python run_demo.py --model vox --source_path YOUR_IMAGE.jpg --driving_path YOUR_VIDEO.mp4
```

Results will be saved in `./res/vox/`

## Project Structure

```
CCN_LIA_Final/
├── LIA_COLAB.ipynb          # Google Colab notebook (main interface)
├── run_demo.py              # Fixed demo script with CPU/GPU support
├── checkpoints/             # Pre-trained models (download separately)
├── data/                    # Sample images and videos
│   └── vox/                # VoxCeleb samples (talking faces)
├── networks/               # Neural network architecture
├── res/                    # Output results folder
└── README.md              # This file
```

## Technical Details

**Model Used:** VoxCeleb (VOX) - trained on talking face videos, optimized for facial animation and lip-sync

**Key Features:**
- Self-supervised learning - no keypoint annotations needed
- Linear latent space navigation for smooth motion
- Works with any face image and driving video
- Maintains source identity while transferring motion

## Limitations

- Works best when source image and driving video have similar viewpoints
- Requires clear, well-lit images for optimal results
- Processing time: 2-5 minutes per video (depends on video length and hardware)
- Large appearance variations between source and driving may reduce quality

## Credits

**Original Authors:** Yaohui Wang, Di Yang, François Brémond, Antitza Dantcheva

**Original Papers:**
- ICLR 2022: "Latent Image Animator: Learning to Animate Images via Latent Space Navigation"
- TPAMI 2024: "LIA: Latent Image Animator"

**Original Repository:** https://github.com/wyhsirius/LIA

**Modifications by:** Vineela-10

## License

This project follows the original LIA license. See LICENSE.md for details.

## Acknowledgments

Part of the original code adapted from [FOMM](https://github.com/AliaksandrSiarohin/first-order-model) and [MRAA](https://github.com/snap-research/articulated-animation).