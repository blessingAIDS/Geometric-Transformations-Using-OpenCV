# Geometric Transformations Using OpenCV

---

## Aim

To write a Python program using OpenCV to perform various geometric transformations on an image.

The program performs the following operations:

- Image Translation  
- Image Scaling (Resizing)  
- Image Shearing  
- Image Reflection (Flipping)  
- Image Rotation  

---

##  Software Used

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (`cv2`)  
- NumPy  
- Matplotlib  

---

##  Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:
Read the input image in color mode.

### Step 3: Image Translation
- Create a translation matrix to shift the image  
- Move the image 50 pixels to the right and 80 pixels down  
- Apply transformation using `cv2.warpAffine()`  
- Display original and translated images  

### Step 4: Image Scaling
- Resize the image to 0.5× (downscale)  
- Resize the image to 2× (upscale)  
- Use `cv2.resize()`  
- Display original, downscaled, and upscaled images  

### Step 5: Image Shearing
- Create transformation matrices for:
  - Horizontal shearing  
  - Vertical shearing  
- Apply transformations using `cv2.warpAffine()`  
- Display original and sheared images  

### Step 6: Image Reflection
- Perform flipping using `cv2.flip()`:
  - Horizontal reflection  
  - Vertical reflection  
  - Both axes  
- Display all reflected images  

### Step 7: Image Rotation
- Create rotation matrices for:
  - 45° rotation  
  - 90° rotation  
- Use `cv2.getRotationMatrix2D()` and `cv2.warpAffine()`  
- Display original and rotated images  

---

##  Program
```
import cv2
import matplotlib.pyplot as plt
import numpy as np


img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)
rows, cols, channels = img_rgb.shape

def display_images(images, titles, grid_shape=(1, 2), figsize=(10, 5)):
    plt.figure(figsize=figsize)
    for i, (img, title) in enumerate(zip(images, titles)):
        plt.subplot(grid_shape[0], grid_shape[1], i + 1)
        plt.imshow(img)
        plt.title(title)
        plt.axis("off")
    plt.tight_layout()
    plt.show()


# ==========================================
# Step 3: Image Translation
# ==========================================
# Translation matrix M: [[1, 0, tx], [0, 1, ty]]
tx, ty = 50, 80  # 50 pixels right, 80 pixels down
M_translation = np.float32([[1, 0, tx], [0, 1, ty]])

translated_img = cv2.warpAffine(img_rgb, M_translation, (cols, rows))

display_images(
    [img_rgb, translated_img],
    ["Original Image", f"Translated (+{tx}px Right, +{ty}px Down)"],
    grid_shape=(1, 2),
)

# ==========================================
# Step 4: Image Scaling
# ==========================================
downscaled_img = cv2.resize(
    img_rgb, (0, 0), fx=0.5, fy=0.5, interpolation=cv2.INTER_AREA
)
upscaled_img = cv2.resize(
    img_rgb, (0, 0), fx=2.0, fy=2.0, interpolation=cv2.INTER_CUBIC
)

display_images(
    [img_rgb, downscaled_img, upscaled_img],
    ["Original Image", "Downscaled (0.5x)", "Upscaled (2.0x)"],
    grid_shape=(1, 3),
    figsize=(12, 4),
)

# ==========================================
# Step 5: Image Shearing
# ==========================================
sh_x = 0.3  # Horizontal shear factor
sh_y = 0.3  # Vertical shear factor

# Transformation matrices
M_shear_h = np.float32([[1, sh_x, 0], [0, 1, 0]])
M_shear_v = np.float32([[1, 0, 0], [sh_y, 1, 0]])

# Adjust output canvas dimensions to avoid severe clipping during shear
h_sheared_img = cv2.warpAffine(
    img_rgb, M_shear_h, (int(cols + rows * sh_x), rows)
)
v_sheared_img = cv2.warpAffine(
    img_rgb, M_shear_v, (cols, int(rows + cols * sh_y))
)

display_images(
    [img_rgb, h_sheared_img, v_sheared_img],
    ["Original Image", "Horizontal Shear (sh_x=0.3)", "Vertical Shear (sh_y=0.3)"],
    grid_shape=(1, 3),
    figsize=(12, 4),
)

# ==========================================
# Step 6: Image Reflection
# ==========================================
# cv2.flip parameters: 1 -> horizontal, 0 -> vertical, -1 -> both axes
flipped_h = cv2.flip(img_rgb, 1)
flipped_v = cv2.flip(img_rgb, 0)
flipped_both = cv2.flip(img_rgb, -1)

display_images(
    [img_rgb, flipped_h, flipped_v, flipped_both],
    [
        "Original Image",
        "Horizontal Reflection",
        "Vertical Reflection",
        "Both Axes Reflection",
    ],
    grid_shape=(2, 2),
    figsize=(8, 8),
)

# ==========================================
# Step 7: Image Rotation
# ==========================================
center = (cols // 2, rows // 2)

# Get 2D rotation matrices (center, angle in degrees, scale)
M_rot_45 = cv2.getRotationMatrix2D(center, 45, 1.0)
M_rot_90 = cv2.getRotationMatrix2D(center, 90, 1.0)

rotated_45 = cv2.warpAffine(img_rgb, M_rot_45, (cols, rows))
rotated_90 = cv2.warpAffine(img_rgb, M_rot_90, (cols, rows))

display_images(
    [img_rgb, rotated_45, rotated_90],
    ["Original Image", "Rotated 45° Counter-Clockwise", "Rotated 90° Counter-Clockwise"],
    grid_shape=(1, 3),
    figsize=(12, 4),
)
```
### Developed By:
**Name:** BLESSING S

### Register No:
212224230039  

---

##  Output
<img width="592" height="635" alt="image" src="https://github.com/user-attachments/assets/486ff5c8-3f37-4022-b28d-28b3896c527d" />

<img width="611" height="620" alt="image" src="https://github.com/user-attachments/assets/b3d1e533-7f1f-4599-b469-5c50502c0a5a" />
<img width="1252" height="430" alt="image" src="https://github.com/user-attachments/assets/3de53d98-9cf7-4fe0-acbf-748a93f170b0" />
<img width="1257" height="437" alt="image" src="https://github.com/user-attachments/assets/473c4a24-5c08-44be-b10f-02928a003eb1" />
<img width="1006" height="495" alt="image" src="https://github.com/user-attachments/assets/0d257ae6-ca48-4e2e-b269-92c295ff4047" />
<img width="937" height="487" alt="image" src="https://github.com/user-attachments/assets/d373e5fa-3948-476c-9ea8-1105a582d1b1" />

<img width="1235" height="432" alt="image" src="https://github.com/user-attachments/assets/69bca922-eccb-4632-a664-8c36c14f9d18" />





### Image Translation
- Original image is displayed  
- Translated image (shifted right and down) is displayed  

### Image Scaling
- Original image is displayed  
- Downscaled image (0.5×) is displayed  
- Upscaled image (2×) is displayed  

### Image Shearing
- Original image is displayed  
- Horizontally sheared image is displayed  
- Vertically sheared image is displayed  

### Image Reflection
- Original image is displayed  
- Horizontally flipped image is displayed  
- Vertically flipped image is displayed  
- Both-axis flipped image is displayed  

### Image Rotation
- Original image is displayed  
- 45° rotated image is displayed  
- 90° rotated image is displayed  

---

##  Result

Thus, various geometric transformations such as translation, scaling, shearing, reflection, and rotation are successfully performed using OpenCV. These transformations demonstrate how images can be spatially manipulated for different computer vision applications.
