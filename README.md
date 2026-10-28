# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** Indhu V
- **Register Number:** 212225040132

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
eagle_gray = cv2.imread("eagle.jpeg", cv2.IMREAD_GRAYSCALE)
assert eagle_gray is not None, "Eagle image not found"
print("Grayscale image loaded successfully")
```

#### 2. Print the image width, height & Channel.
```python
height, width = eagle_gray.shape
channels = 1

print("Width:", width)
print("Height:", height)
print("Channel:", channels)
```

#### 3. Display the image using matplotlib imshow().
```python
plt.imshow(eagle_gray, cmap="gray")
plt.title("Eagle Grayscale Image")
plt.axis("off")
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite("eagle_grayscale.png", eagle_gray)
print("Image saved successfully")
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
eagle_bgr = cv2.imread("eagle_grayscale.png", cv2.IMREAD_COLOR)
assert eagle_bgr is not None, "Saved image not found"

eagle_from_png_rgb = cv2.cvtColor(eagle_bgr, cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.imshow(eagle_from_png_rgb)
plt.title("Eagle Color Mode")
plt.axis("off")
plt.show()

height, width, channels = eagle_from_png_rgb.shape

print("Width:", width)
print("Height:", height)
print("Channels:", channels)
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
eagle_original_bgr = cv2.imread("eagle.jpeg", cv2.IMREAD_COLOR)
assert eagle_original_bgr is not None, "Eagle image not found"

eagle_rgb = cv2.cvtColor(eagle_original_bgr, cv2.COLOR_BGR2RGB)

# Crop the eagle using row and column coordinates
eagle_crop = eagle_rgb[20:445, 200:555]

plt.imshow(eagle_crop)
plt.title("Cropped Eagle")
plt.axis("off")
plt.show()
```

#### 8. Resize the image up by a factor of 2x.
```python
eagle_resized = cv2.resize(
    eagle_crop, None, fx=2, fy=2,
    interpolation=cv2.INTER_CUBIC
)

plt.imshow(eagle_resized)
plt.title("Eagle Resized 2x")
plt.axis("off")
plt.show()
```

#### 9. Flip the cropped/resized image horizontally.
```python
eagle_flipped = cv2.flip(eagle_resized, 1)

plt.imshow(eagle_flipped)
plt.title("Horizontally Flipped Eagle")
plt.axis("off")
plt.show()
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
apollo_bgr = cv2.imread("Apollo-11-launch.jpeg", cv2.IMREAD_COLOR)
assert apollo_bgr is not None, "Apollo image not found"

apollo_rgb = cv2.cvtColor(apollo_bgr, cv2.COLOR_BGR2RGB)

print("Apollo image shape:", apollo_rgb.shape)

plt.figure(figsize=(10, 6))
plt.imshow(apollo_rgb)
plt.axis("off")
plt.show()
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
text = "Apollo 11 Saturn V Launch, July 16, 1969"
font_face = cv2.FONT_HERSHEY_PLAIN

apollo_annotated = apollo_bgr.copy()

height, width = apollo_annotated.shape[:2]

font_scale = 1.5
thickness = 2

text_width = cv2.getTextSize(
    text, font_face, font_scale, thickness
)[0][0]

x = (width - text_width) // 2
y = height - 20

cv2.putText(
    apollo_annotated, text, (x, y),
    font_face, font_scale, (255, 255, 255),
    thickness, cv2.LINE_AA
)
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
rect_color = (255, 0, 255)  # Magenta in BGR

cv2.rectangle(
    apollo_annotated,
    (480, 55),
    (705, 630),
    rect_color,
    4
)
```

#### 13. Display the final annotated image.
```python
apollo_annotated_rgb = cv2.cvtColor(
    apollo_annotated, cv2.COLOR_BGR2RGB
)

plt.figure(figsize=(12, 7))
plt.imshow(apollo_annotated_rgb)
plt.title("Apollo 11 Annotated Image")
plt.axis("off")
plt.show()

cv2.imwrite("apollo_annotated.png", apollo_annotated)
```

#### 14. Read the image ('Boy.jpg').
```python
boy_bgr = cv2.imread("boy.jpeg", cv2.IMREAD_COLOR)
assert boy_bgr is not None, "Boy image not found"

boy_rgb = cv2.cvtColor(boy_bgr, cv2.COLOR_BGR2RGB)

print("Boy image shape:", boy_rgb.shape)

plt.imshow(boy_rgb)
plt.title("Original Boy Image")
plt.axis("off")
plt.show()
```

#### 15. Adjust the brightness of the image.
```python
# Create a matrix of ones with data type float64
matrix_ones = np.ones(boy_bgr.shape, dtype=np.float64)

# Brightness adjustment value
matrix = (matrix_ones * 50).astype(np.uint8)
```

#### 16. Create brighter and darker images.
```python
img_brighter = cv2.add(boy_bgr, matrix)
img_darker = cv2.subtract(boy_bgr, matrix)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
img_brighter_rgb = cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB)
img_darker_rgb = cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(14, 4))

plt.subplot(1, 3, 1)
plt.imshow(boy_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(img_darker_rgb)
plt.title("Darker Image")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(img_brighter_rgb)
plt.title("Brighter Image")
plt.axis("off")

plt.tight_layout()
plt.show()
```

#### 18. Modify the image contrast.
```python
# Create two higher contrast images
matrix1 = 1.1
matrix2 = 1.2

img_higher1 = cv2.convertScaleAbs(
    boy_bgr, alpha=matrix1, beta=0
)

img_higher2 = cv2.convertScaleAbs(
    boy_bgr, alpha=matrix2, beta=0
)
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
img_lower = cv2.convertScaleAbs(
    boy_bgr, alpha=0.8, beta=0
)

img_lower_rgb = cv2.cvtColor(img_lower, cv2.COLOR_BGR2RGB)
img_higher2_rgb = cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(14, 4))

plt.subplot(1, 3, 1)
plt.imshow(boy_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(img_lower_rgb)
plt.title("Lower Contrast")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(img_higher2_rgb)
plt.title("Higher Contrast")
plt.axis("off")

plt.tight_layout()
plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(boy_bgr)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(b, cmap="gray")
plt.title("Blue Channel")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(g, cmap="gray")
plt.title("Green Channel")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(r, cmap="gray")
plt.title("Red Channel")
plt.axis("off")

plt.tight_layout()
plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged_bgr = cv2.merge([b, g, r])
merged_rgb = cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.imshow(boy_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(merged_rgb)
plt.title("Merged RGB Image")
plt.axis("off")

plt.tight_layout()
plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv_img = cv2.cvtColor(boy_bgr, cv2.COLOR_BGR2HSV)

h, s, v = cv2.split(hsv_img)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(h, cmap="gray")
plt.title("Hue Channel")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(s, cmap="gray")
plt.title("Saturation Channel")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(v, cmap="gray")
plt.title("Value Channel")
plt.axis("off")

plt.tight_layout()
plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.merge([h, s, v])

restored_bgr = cv2.cvtColor(
    merged_hsv, cv2.COLOR_HSV2BGR
)

restored_rgb = cv2.cvtColor(
    restored_bgr, cv2.COLOR_BGR2RGB
)

plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.imshow(boy_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(restored_rgb)
plt.title("Merged HSV Image")
plt.axis("off")

plt.tight_layout()
plt.show()
```

## Output:
- **i)** Read and Display an Image.
<img width="790" height="594" alt="image" src="https://github.com/user-attachments/assets/044a8905-ba25-4efe-9bd7-0a6759b45c8b" />

- **ii)** Adjust Image Brightness.
- <img width="1035" height="288" alt="image" src="https://github.com/user-attachments/assets/88a6af09-0611-4fe9-9b06-0de8d3620e01" />

- **iii)** Modify Image Contrast.
- <img width="1054" height="287" alt="image" src="https://github.com/user-attachments/assets/566d8850-d57d-4322-9855-ccaca6c1dbd6" />

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.
