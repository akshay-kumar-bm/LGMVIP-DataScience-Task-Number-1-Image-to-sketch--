# Image to Pencil Sketch

**A Flask web app (and notebook) that converts an uploaded photo into a pencil sketch using OpenCV. LGMVIP Data Science internship, Task 1.**

## How it works

The sketch is produced with the classic "dodge" technique, implemented identically in `app.py` and the notebook:

1. Read the image and convert to grayscale
2. Invert the grayscale image
3. Gaussian blur the inverted image (21x21 kernel)
4. Invert the blurred image
5. Divide the grayscale image by the inverted blur (`cv2.divide`, scale 250 in the app, 240 in the notebook)

## Features

- Web upload form (`templates/index.html`) and a result preview page (`templates/preview.html`)
- Step-by-step Jupyter notebook (`image to sketch.ipynb`, also exported as PDF) visualising each stage with matplotlib
- Demo screen recording of the app (`Recording 2024-04-10 114233.mp4`)

## Tech stack

Python, Flask, OpenCV (`cv2`), NumPy, matplotlib, Werkzeug.

## Structure

```
app.py                      # Flask app: upload -> convert_to_sketch -> preview
templates/                  # index.html, preview.html
static/image_upload/        # uploaded images
static/saved_image/         # generated sketch.png
image to sketch.ipynb/.pdf  # notebook walkthrough
```

## Run

No requirements file is included; install dependencies manually.

```bash
pip install flask opencv-python numpy matplotlib
python app.py        # http://127.0.0.1:5000
```

## Limitations

- Paths use Windows backslashes (`static\image_upload`), so it only works as written on Windows; the `static/image_upload` folder must exist.
- Output always overwrites `sketch.png`; no input validation beyond `secure_filename`; debug mode is on.
- No `requirements.txt`; about 48 MB of repo size comes from a demo video and PDF.
