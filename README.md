# Gradient Panel (Python)

This simple Python script generates a **smooth diagonal gradient** between two colors using **NumPy** and **Matplotlib**.  
It’s minimal, easy to tweak, and great for quick visual experiments.

---

## 🧩 Requirements

Install dependencies first:

```bash
pip install numpy matplotlib
```

**Libraries used:**
- **NumPy** → for array math and interpolation  
- **Matplotlib** → to display the gradient as an image  

---

## 🚀 Run

Save the code below as **`gradient_panel.py`**, then run:

```bash
python gradient_panel.py
```

A window will pop up showing the generated gradient.

---

## 🧠 Full Code (with comments)

```python
import numpy as np
import matplotlib.pyplot as plt

def gradient_panel(n, c1, c2):
    """
    Create a diagonal gradient image from color c1 to color c2.

    Parameters:
        n  (int)      – Image resolution (n x n)
        c1 (tuple)    – RGB color 1 (0–255)
        c2 (tuple)    – RGB color 2 (0–255)
    Returns:
        np.ndarray    – n x n x 3 RGB array
    """

    # Convert 8-bit RGB (0–255) to normalized 0–1 range for math
    c1, c2 = np.array(c1)/255, np.array(c2)/255

    # Create a 1D array from 0 to 1 (n equally spaced values)
    x = np.linspace(0, 1, n)

    # Blend factor for each pixel (averaging x and y gives diagonal gradient)
    t = (x[:, None] + x[None, :]) / 2

    # Linearly interpolate between c1 and c2 using t
    img = (1 - t)[..., None]*c1 + t[..., None]*c2
    return img


# === Run the gradient generator ===

n = 100  # resolution (higher = smoother)
cyan = (0, 255, 255)
pink = (255, 105, 180)

# Generate the gradient
img = gradient_panel(n, cyan, pink)

# Display the result
plt.imshow(img, origin='lower')
plt.axis('off')
plt.show()
```

---

## ⚙️ Customize

- Change the **colors**:
  ```python
  gradient_panel(200, (255, 0, 0), (0, 0, 255))  # red to blue
  ```

- Change the **size** (resolution):
  ```python
  n = 300  # smoother gradient
  ```

---

## 📸 Example Output

A smooth diagonal blend from **cyan → pink**:

```
╔══════════════════╗
║ cyan ░░░░ pink   ║
╚══════════════════╝
```

---

*Made with NumPy & Matplotlib — no extra dependencies.*
