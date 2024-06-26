# UTS_PengolahanCitra
### TI.22.A5

> Membuat manipulasi gambar dengan menggunakan streamlit

Anggota Kelompok :

| Nama  |  Nim |
| ----------------- | ------------- |
| Vivie Zuliani Erikasari         | 312210475 |
| Zulaeha                         | 312210575 |
| Tyanshi Firli Maharani          | 312210581 |
| Wafha Zahra Mulqiya             | 312210577 |
| Alfaza Putra Adjie Ariefiansyah | 312210512 |

### Project
>  1. RGB to HSV
>  2. Histogram
>  3. Brightness and Contrast
>  4. Contours
>  5. Tampilan Setelah Dilakukan Running


### Information 
> Sebelum memulai untuk mengisi script dari RGB to HSV, di perlukan script `button` untuk button RGB to HSV, button Histogram, button Brightness and Contrast, dan button Contours. Scriptnya yaitu :
```
st.title('Image Manipulation App')

uploaded_file = st.file_uploader("Choose an image...", type=["jpg", "jpeg", "png"])
if uploaded_file is not None:
    file_bytes = np.asarray(bytearray(uploaded_file.read()), dtype=np.uint8)
    image = cv2.imdecode(file_bytes, cv2.IMREAD_COLOR)

    st.image(image, caption='Original Image', use_column_width=True)

    if st.button('Convert RGB to HSV'):
        hsv_image = convert_rgb_to_hsv(image)
        st.image(hsv_image, caption='HSV Image', use_column_width=True)

    if st.button('Show Histogram'):
        plt = plot_histogram(image)
        st.pyplot(plt)

    brightness = st.slider("Brightness", min_value=-100, max_value=100, value=0)
    contrast = st.slider("Contrast", min_value=-100, max_value=100, value=0)
    if st.button('Adjust Brightness and Contrast'):
        bc_image = adjust_brightness_contrast(image, brightness, contrast)
        st.image(bc_image, caption='Brightness and Contrast Adjusted Image', use_column_width=True)

    if st.button('Find Contours'):
        contours_image = find_contours(image)
        st.image(contours_image, caption='Image with Contours', use_column_width=True)
```

---
#####  1. RGB to HSV
```
import streamlit as st
import cv2
from matplotlib import pyplot as plt
import numpy as np

def convert_rgb_to_hsv(image):
    return cv2.cvtColor(image, cv2.COLOR_RGB2HSV)
```

#####  2. Histogram
```
def plot_histogram(image):
    color = ('b', 'g', 'r')
    for i, col in enumerate(color):
        hist = cv2.calcHist([image], [i], None, [256], [0, 256])
        plt.plot(hist, color=col)
        plt.xlim([0, 256])
    plt.title('Histogram')
    return plt

```

#####  3. Brightness and Contrast
```
def adjust_brightness_contrast(image, brightness=0, contrast=0):
    new_image = np.zeros(image.shape, image.dtype)
    alpha = contrast * 0.01
    beta = brightness

    # Adjustment made here
    for y in range(image.shape[0]):
        for x in range(image.shape[1]):
            for c in range(image.shape[2]):
                new_image[y,x,c] = np.clip(alpha*image[y,x,c] + beta, 0, 255)
    
    return new_image
```

#####  4. Contours
```
def find_contours(image):
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    blurred = cv2.GaussianBlur(gray, (5, 5), 0)
    edged = cv2.Canny(blurred, 50, 150)
    contours, _ = cv2.findContours(edged.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    image_with_contours = image.copy()
    cv2.drawContours(image_with_contours, contours, -1, (0, 255, 0), 3)
    return image_with_contours

```

---
#####  5. Tampilan Setelah Dilakukan Running
> Jalankan (run) code melalui command prompt dengan menggunakan script berikut :
```
python -m streamlit run uts.py
```
Sehingga muncul outputnya seperti berikut ini.

![Screenshot 2024-06-08 123656](https://github.com/VivieZuliani/UTS_PengolahanCitra/assets/130271255/8eb300ff-476c-4265-8b94-8df0cf7ea826)

![Screenshot 2024-06-08 123713](https://github.com/VivieZuliani/UTS_PengolahanCitra/assets/130271255/08df9cdf-8a01-4111-ae25-99392ae10f7d)

![Screenshot 2024-06-08 123735](https://github.com/VivieZuliani/UTS_PengolahanCitra/assets/130271255/4963689f-a6ed-43c0-b1fe-943ae22f6cf2)

![Screenshot 2024-06-08 123750](https://github.com/VivieZuliani/UTS_PengolahanCitra/assets/130271255/778765d2-bd01-4961-9047-3822a7377d47)

![Screenshot 2024-06-08 123830](https://github.com/VivieZuliani/UTS_PengolahanCitra/assets/130271255/042c61b6-6f43-453d-9cd5-052f67e3ff0e)

![Screenshot 2024-06-08 123856](https://github.com/VivieZuliani/UTS_PengolahanCitra/assets/130271255/7ccaf2af-30ba-4e6e-b111-120d7df831ad)


## END
### Terima Kasih










