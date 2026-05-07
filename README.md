# CAPTCHA Recognizer 🔥

UGH! Big project here. Much work. Me explain.

## What This Fire Do?

This tool recognize CAPTCHA text from image. Use computer sight (vision) to find letter shapes. Then brain (neural network) read what letter be.

## How Rock Stack Work (Tech Stack)

```
Image come in
    ↓
Preprocessing (make clean picture)
    ↓
Segmentation (find each letter)
    ↓
Neural network (guess what letter be)
    ↓
Text come out
```

## Fire You Build (Features)

### 🎯 Image Preprocessing

Many way to clean picture. Code find what work best:

- **Grayscale conversion** - Remove color noise, make simpler
- **Histogram equalization** - Make dark part bright, bright part brighter
- **Adaptive thresholding** - Find letter edge (black/white split)
- **Median blur** - Remove small noise spot
- **Morphological operations** - Close gap in letter, connect broken part

### 🔤 Character Segmentation

UGH. Hard part. Found letter in picture. Multiple approach tried:

- **Contour detection** - Find shape outline
- **Bounding box extraction** - Get rectangle around letter
- **Morphology with different kernel** - Try (1,1) and (2,2) kernel size
- **Color-based detection** - Use HSV color space for better letter find
- **Hue histogram analysis** - Look at color peak to detect letter boundary
- **Watershed algorithm** - Advanced technique for touch letter
- **Tesseract OCR** - Alternative method for text read

### 🧠 Neural Network Models

Build many brain type to recognize letter:

- **model.py** - Base CNN with 2 convolutional layer, batch norm, dense layer
- **model2.py** - Another try (small variation)
- **model3.py** - VGG16 approach (try famous architecture)
- **model4.py** - Another experiment

### 📊 Data Augmentation

Make more training rock (data):

```python
- Rotation (5°) - Tilt letter little
- Zoom (10%) - Make letter bigger/smaller
- Width shift (10%) - Move letter sideways
- Height shift (10%) - Move letter up/down
- Shear (10%) - Bend letter angle
```

### 🎓 Training Pipeline

```
extracted_letter_images/          (folder with letter training data)
├── a/
│   ├── 1.png
│   ├── 2.png
│   └── ...
├── b/
│   └── ...
└── 0-9/
    └── ...
        ↓
    Load and preprocess
        ↓
    Resize to 40x40 pixel
        ↓
    Normalize (divide by 255)
        ↓
    Train/test split (75/25)
        ↓
    Train CNN model
        ↓
    Save model (.hdf5 file)
```

## Many Experiment Notebook (Jupyter)

UGH. Much work with notebook:

- **code.ipynb** - Main testing space
- **gut.ipynb** - Test individual file
- **color.ipynb** - Deep color space experiment (HSV, RGB)
- **color-1.ipynb** - Another color try
- **hsv.ipynb** - HSV channel deep dive
- **segmentation.ipynb** - Segmentation technique test
- **watershed.ipynb** - Advanced segmentation method try
- **trump_wall.ipynb** - ... wall technique? Mystery notebook

## Rock You Made (Files)

### Model File
- `captcha_recognition_model.hdf5` (10.7 MB) - Trained model brain
- `captcha_recognition_model.h5` (1.4 MB) - Another model version
- `model_labels.dat` - Letter label map (a-z, 0-9)

### Code File
- `captcha_segmentation.py` - Main segmentation approach
- `captcha_segmentation_2.py` - Alternative segmentation
- `captcha_segmenter.py` - Another segmentation (with color analysis)
- `model.py` - Main model training script
- `model2.py`, `model3.py`, `model4.py` - Other model approach try
- `segment_for_cleaning.py` - Data cleaning for segmentation
- `guzman.py` - Special technique (mystery name)
- `tesseract.py` - OCR alternative test
- `new.py` - New approach test

## What Need To Work

```
numpy==1.21.6
opencv-python==4.10.0.84
keras
tensorflow
scikit-learn
matplotlib
```

## How Use (Usage)

### 1. Segment CAPTCHA Image First

```python
from captcha_segmentation import CaptchaSegmenter

segmenter = CaptchaSegmenter("path/to/captcha.png")
segmenter.run_segmentation()
# Output: extracted_letter_images/ folder with letter separated
```

### 2. Train Model

```bash
python model.py
# Load letter, train brain, save model
```

### 3. Use Model For Prediction

```python
import cv2
import pickle
from keras.models import load_model

# Load model and label map
model = load_model("captcha_recognition_model.hdf5")
with open("model_labels.dat", "rb") as f:
    lb = pickle.load(f)

# Predict on single image
image = cv2.imread("letter.png", 0)
image = cv2.resize(image, (40, 40))
image = image.astype("float") / 255.0
prediction = model.predict(image)
predicted_letter = lb.inverse_transform(prediction)
```

## Git Journey (Effort Timeline)

38 commit made. Journey like:

1. **Start** - First segmenter try
2. **Evolve** - Many segmentation approach try (kernel size, color, watershed)
3. **Model iterate** - Try VGG16, different architecture
4. **Data clean** - Tesseract, remove black line, fix color peak
5. **Refine** - Test individual file, optimize parameter
6. **Update** - Final polish

```
Total commit: 38
Branch merge: Multiple try with main
Approach test: Segmentation, color, OCR, neural network
```

## Architecture Decision

### Why Two Kernel Size For Segmentation?

Try (1,1) kernel first - get more letter (split connected letter).
If fail, try (2,2) kernel - get less letter (merge close letter).

### Why Data Augmentation?

Only have limited real CAPTCHA image. Augmentation make 1 image become 8 different image. Brain learn better this way.

### Why Early Stopping?

Brain train too long = learn noise not pattern. Stop when validation loss not improve = save best brain.

### Why Learning Rate Reduce?

First big jump in learning. Then smaller jump. Better convergence.

## Challenge Solve

✅ **Overlapping letter** - Use watershed, use color analysis

✅ **Distorted letter** - Augmentation, morphology operation

✅ **Noise in image** - Median blur, threshold, morphology

✅ **Different letter size** - Adaptive kernel, segmentation by character width

UGH. Big journey. Much try. Much fail. But fire work now.

---

**Make by**: Pawan (caveman programmer)
**Status**: Still growing, still experiment
**Latest effort**: 2026-05-07
