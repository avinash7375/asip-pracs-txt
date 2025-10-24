## 📘 1. Digital Image Processing by Gonzalez & Woods — Core Reference

This is your *primary text* for almost all the topics in Unit 2.

---

### **1. Definition and Applications of Image Processing**

**Definition:**
Image processing is the field that involves operations on images to enhance them, extract information, or prepare them for analysis.
Formally, an image is represented as a 2D function ( f(x, y) ), where ( x, y ) denote spatial coordinates, and ( f ) denotes the intensity (brightness).

**Applications:**

* **Enhancement:** Improving contrast, brightness, or color (e.g., medical imaging, astronomy).
* **Restoration:** Removing noise or blur.
* **Compression:** JPEG, PNG, etc.
* **Segmentation and Feature Extraction:** Used in computer vision, OCR, autonomous vehicles.

---

### **2. Image Processing Pipeline (Fig. 1.2, Gonzalez)**

1. **Image Acquisition:** Capturing the image (camera, scanner).
2. **Preprocessing:** Noise reduction, resizing, correction.
3. **Segmentation:** Dividing an image into meaningful regions.
4. **Representation and Description:** Extracting features (edges, shapes).
5. **Recognition and Interpretation:** Assigning labels or meaning.
6. **Storage and Display:** Output of processed image.

---

### **3. Tools and Libraries**

From **Gonzalez**, you get the conceptual basis; implementation comes from **Python-based tools** (covered better in Think DSP and Python ecosystem):

* **OpenCV** – real-time image processing.
* **scikit-image** – high-level functions (filtering, thresholding).
* **Pillow (PIL)** – image I/O and manipulation.
* **NumPy** – matrix-based image representation.
* **matplotlib** – visualization and histogram plotting.

---

### **4. Image Types and File Formats**

**Image types:**

* **Binary images:** 1-bit pixels (0 or 1).
* **Grayscale images:** 8-bit pixels (0–255 intensity).
* **Color images:** 3-channel (RGB or CMY).
* **Indexed images:** Use color maps.

**Common formats:**

* **BMP:** Uncompressed, simple.
* **JPEG:** Lossy compression, used for photos.
* **PNG:** Lossless compression, transparency support.
* **TIFF:** High-quality scientific/medical imaging.

---

### **5. Intensity Transformations**

Intensity transformation functions modify pixel values to enhance image visibility or extract information.

**(a) Log Transform**
[
s = c \log(1 + r)
]

* Expands dark regions, compresses bright regions.
* Used in astronomical or X-ray images where intensity varies exponentially.

**(b) Power-law (Gamma) Transform**
[
s = c r^\gamma
]

* ( \gamma < 1 ): brightens image
* ( \gamma > 1 ): darkens image
* Used in **gamma correction** for display devices.

**(c) Contrast Stretching**
[
s =
\begin{cases}
0, & r < r_1 \
\frac{(r - r_1)}{(r_2 - r_1)} (s_2 - s_1) + s_1, & r_1 \le r \le r_2 \
L-1, & r > r_2
\end{cases}
]
Enhances contrast by stretching the range of intensity levels.

**(d) Thresholding**
[
s =
\begin{cases}
0, & r < T \
L-1, & r \ge T
\end{cases}
]
Separates objects from background — useful in segmentation.

---

### **6. Histogram Processing**

A histogram shows the frequency of each intensity value.

**(a) Histogram Equalization:**
Redistributes intensities to flatten the histogram and improve contrast.
[
s = (L-1) \int_0^r p_r(w),dw
]
where ( p_r(w) ) is the probability density function of intensity levels.

**(b) Histogram Matching (Specification):**
Maps one image’s histogram to another’s, useful for standardizing brightness across datasets.

---

### **7. Image Smoothing (Filtering)**

**Goal:** Reduce noise or blur unwanted details.

* **Linear smoothing (Averaging filter):**
  Convolution with a mean filter:
  [
  g(x, y) = \frac{1}{mn} \sum_{s,t} f(x+s, y+t)
  ]
  Simple average of neighboring pixels.

* **Non-linear smoothing:**

  * **Median filter:** replaces a pixel with the median of its neighborhood.
  * Preserves edges better than mean filtering.

---

### **8. Sharpening of Images**

Enhances edges or fine details by amplifying high-frequency components.

* **Laplacian-based sharpening:**
  [
  \nabla^2 f = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2}
  ]
  Sharpened image:
  [
  g(x, y) = f(x, y) - c \nabla^2 f(x, y)
  ]
  where ( c ) controls sharpening intensity.

* **Unsharp masking and High-boost filtering:**
  Subtract smoothed image from the original.

---

### **9. Image Derivatives and Gradients**

**Gradient magnitude:**
[
|\nabla f| = \sqrt{(G_x)^2 + (G_y)^2}
]
where ( G_x ) and ( G_y ) are first derivatives (Sobel or Prewitt operators).

**Direction:**
[
\theta = \tan^{-1}\left(\frac{G_y}{G_x}\right)
]

**Laplacian (Second derivative):**
Used for edge detection, but very sensitive to noise.

**Effect of noise:**
Derivatives amplify high-frequency components — hence noise is magnified.
Mitigation: Apply smoothing (Gaussian blur) before edge detection.

---

## 🧠 2. Think DSP (Allen Downey) — Supplementary View

Although primarily about *signal processing*, this book offers valuable analogies and Python tools that apply directly to **image processing** (which is 2D signal processing).

---

### Key Cross-links:

| Image Processing Concept | DSP Equivalent            | Insight from Think DSP            |
| ------------------------ | ------------------------- | --------------------------------- |
| Pixel intensity          | Amplitude (signal value)  | Both are discrete samples.        |
| Image filtering          | Signal filtering          | Convolution in time ↔ space.      |
| Smoothing                | Low-pass filtering        | Removes high-frequency noise.     |
| Sharpening               | High-pass filtering       | Enhances edges (details).         |
| Histogram equalization   | Dynamic range compression | Adjusting amplitude distribution. |

---

### Python Insight from Think DSP:

Downey demonstrates:

* **Fourier Transform** for frequency-domain analysis.
  → In image processing: 2D FFT used for filtering, denoising, and sharpening.
* **Windowing and Filtering** with NumPy convolution — identical logic applies to spatial kernels.

---

## 🧩 Summary Table (Book-wise Alignment)

| Topic                     | Gonzalez & Woods       | Think DSP                                |
| ------------------------- | ---------------------- | ---------------------------------------- |
| Definition & Applications | Chapter 1              | Ch. 1–2 (Signals & Systems analogies)    |
| Image Types & Formats     | Ch. 2                  | —                                        |
| Intensity Transformations | Ch. 3                  | Related to amplitude scaling             |
| Histogram Processing      | Ch. 3                  | Amplitude normalization                  |
| Smoothing/Sharpening      | Ch. 3                  | Low-/High-pass filters                   |
| Derivatives & Gradients   | Ch. 3                  | Differentiation in time/frequency domain |
| Effect of Noise           | Ch. 5                  | Spectral leakage and noise handling      |
| Tools (Python, NumPy)     | Implementation section | Core focus of Think DSP                  |
---
