# Visual Inspection of Motorcycle Connecting Rods

A computer-vision system for the automated visual inspection of motorcycle
connecting rods ("bielle"). Given a grayscale image of rods scattered on an
inspection plane, the system detects each rod and measures its key dimensional
features. Developed as the final project for the **Computer Vision and Image
Processing** course (Master's in Automation Engineering).

## Objective

Analyse the dimensions of two different types of connecting rods:

- **Type A** – rods with **one** hole
- **Type B** – rods with **two** holes

For every rod found in an image, the system reports:

- Type (A / B) and number of holes
- Position (barycentre coordinates) and orientation of the major axis
- Length, width, and width at the barycentre
- For each hole: centre position and diameter

## Pipeline

1. **Image loading & histogram analysis** – load the grayscale images and inspect intensity distributions.
2. **Denoising** – reduce sensor/scan noise for cleaner segmentation.
3. **Segmentation** – threshold the rods (foreground) from the background.
4. **Connected components** – label each separate blob (rod).
5. **Feature extraction** per blob:
   - Haralick circularity measure
   - Barycentre coordinates
   - Hole detection (centre + diameter)
   - Major-axis orientation
   - Width along the minor axis
6. **Inspection report** – summarise measurements per rod.

## Tasks

- **Task 1 — Basic inspection:** Rods appear clearly separated and non-touching.
- **Task 2 — Robustness to distractors:** The system is extended to cope with a
  more realistic setup:
  - Distractor objects (e.g. screws/washers) present in the scene
  - The inspection area may be dirty due to scattered iron powder
  - Handled via **Gaussian + Bilateral filtering** and **connected-components
    analysis with threshold/area filtering**.

## Repository contents

| File | Description |
|------|-------------|
| `Final_Project_Computer_Vision.ipynb` | Main notebook with the full implementation and results |
| `ispezione-bielle-immagini/` | Input test images (`TESI*.BMP`) |
| `Visual Inspection of Motorcycle.pdf` | Project report |

## Tech stack

- Python 3
- [OpenCV](https://opencv.org/) (`cv2`)
- NumPy
- SciPy
- Matplotlib

## Running

The notebook was developed in **Google Colab** (it mounts Google Drive to load
the images). To run it:

- **Colab:** upload the `ispezione-bielle-immagini/` folder to your Drive and
  adjust the image-folder path, or
- **Locally (Jupyter):** replace the `google.colab.drive` mount with a local
  path to the `ispezione-bielle-immagini/` folder, then run all cells.

```bash
pip install opencv-python numpy scipy matplotlib
jupyter notebook Final_Project_Computer_Vision.ipynb
```
