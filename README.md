# Artify — Photo to Artwork

**DE4-DVS Module Project**  
*Project Suggestion 4: Turn photographs into painted-style artwork*

---

## 1. What We Have Achieved

We built **Artify**, a MATLAB application that converts photographs into artistic renditions. The application supports **seven artistic styles**, each with adjustable parameters:

| Style | Description | Key Techniques |
|-------|-------------|----------------|
| **Poster / Pop Art** | Flat colours, high contrast, bold outlines | Mean-Shift colour quantisation, contrast stretching, Sobel edges |
| **Cartoon** | Clean regions, comic-like edges | 5D Mean-Shift segmentation, morphological opening, LoG edges |
| **Sketch** | Pencil-style line drawing | Mean-Shift quantisation, Canny edge detection |
| **Watercolor** | Pigment-like wash, paper texture | Cartoon abstraction, morphological closing, edge darkening |
| **Bright Watercolor** | Lighter, more vibrant wash | Similar pipeline with different parameter tuning |
| **Oil Painting** | Painterly, colour-block effect | Watershed segmentation, median filtering |
| **Stained Glass** | Mosaic-style, jewel tones, lead lines | k-means segmentation, optional Gothic-arch frame |

The application is launched via **`artify_app`**, which provides a modern GUI with style dropdown, per-style parameter tuning, before/after slider comparison, SSIM evaluation, and save functionality.

Shared modules include `meanShiftColorQuant.m` and `meanShiftSegmentation.m`, used across multiple styles for coherent architecture.

---

## 2. How to Run the Application

### Requirements

- **MATLAB R2016a or later**
- **MATLAB Image Processing Toolbox** (for `edge`, `strel`, `watershed`, etc.)
- No additional hardware required

### How to Run

1. Open MATLAB and navigate to the `matlab` folder:
   ```matlab
   cd matlab
   ```
2. Run the application:
   ```matlab
   artify_app
   ```
3. Use the interface:
   - Click **Load Image** and select an image (JPG, PNG, BMP, TIFF supported)
   - Choose a style from the dropdown
   - Adjust parameters (hints show valid ranges)
   - Click **Process**
   - Drag the slider to compare result vs original
   - Click **Save Result** to export

---

## 3. Evidence That the Application Works

### Screenshots

*(Insert 2–4 screenshots here, for example:)*

1. **GUI with loaded image and processed result** — Show the main Artify window with an image loaded and one style (e.g. Poster) applied, with the before/after slider visible.
2. **Multiple styles comparison** — Same photo processed with Poster, Cartoon, and Sketch side by side.
3. **Parameter tuning** — Same style with different parameter values to show the effect of adjustments.
4. **Stained Glass with canvas** — Example of Stained Glass style with the optional mosaic frame enabled.

### Quick sanity check

To verify the application runs correctly:

1. Run `artify_app` in MATLAB.
2. Load any photograph (e.g. a portrait or landscape).
3. Select "Poster / Pop Art" and click Process.
4. You should see a flattened, high-contrast result with dark outlines.
5. Drag the slider to compare original and result.
6. Check that SSIM and processing time appear in the evaluation label.

---

## 4. Evaluation: What the Application Can and Cannot Do

### Strengths

- **Seven distinct artistic styles** with different visual outcomes (flat graphic, comic, pencil sketch, watercolor, oil, stained glass).
- **Instant feedback** via the slider comparison and parameter hints, so users can explore the effect of each setting.
- **Quantitative evaluation** (SSIM and processing time) for understanding style divergence and performance.
- **Flexible input** — Supports common image formats and handles grayscale by converting to RGB.
- **No external dependencies** — Uses only MATLAB and the Image Processing Toolbox.

### Limitations

- **Processing time**: Cartoon and other segmentation-heavy styles can take 10–30 seconds on large images (e.g. 1080p) due to Mean-Shift complexity. We apply downsampling for very large images to improve speed.
- **Sketch quality**: Canny edge detection can pick up texture (grass, fabric, skin) as well as structure, leading to noisy lines in some images. A DoG (Difference-of-Gaussians) approach could improve selectivity.
- **Parameter sensitivity**: Some styles (e.g. Poster, Cartoon) require parameter tuning for best results on different image types; default values are tuned for general-purpose use.
- **Stained Glass output size**: When "Add canvas" is enabled, the output may have different dimensions than the input due to the mosaic frame.

### Possible future improvements

- Additional edge-detection strategies (e.g. DoG) for cleaner Sketch lines.
- Batch processing of multiple images from a folder.
- Performance optimisation (e.g. parallel processing or GPU) for large images.
- Export of parameter presets for reproducible results.

---

## Project Structure

```
matlab/
├── artify_app.m          # Application entry point
├── main.m
├── getParameters.m
├── meanShiftColorQuant.m # Colour-only Mean-Shift quantisation
├── meanShiftSegmentation.m # 5D spatial-colour Mean-Shift
├── artify_poster.m       # Poster / Pop Art style
├── artify_cartoon.m      # Cartoon style
├── artify_sketch.m       # Sketch style
├── artify_watercolor.m   # Watercolor style
├── artify_bright_watercolor.m
├── artify_oilpainting.m
├── artify_stainedglass.m
├── lxy_cartoon.m         # Shared cartoon abstraction
├── colorspace.m          # Colour space utilities
└── bfilter2.m            # Bilateral filter
```

---

## References

- Project specification: [DE4-DVS-Labs/Project](https://github.com/DE4-DVS-Labs/Project)
- Project suggestion 4: "Artify" photographs — turn a photograph into something that looks more like painted artwork





