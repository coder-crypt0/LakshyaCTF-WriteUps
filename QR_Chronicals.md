# QR Chronicals Writeup

## Challenge Description
A simple CSV file? Think again! This file hides a crucial secret within its structured data, but it's not immediately visible to the naked eye. The key to unlocking it lies in understanding the encoded coordinates stored within. Can you decipher the hidden pattern and extract the concealed information?

Flag Format: LakshyaCTF{enter your flag as it is here}

## Initial Analysis

Upon opening the Excel file, I found a list of coordinates in the following format:

```
:::row,col:::
0,0
0,1
0,2
0,3
0,4
0,5
0,6
0,9
0,19
0,20
0,22
0,23
0,24
0,25
0,26
0,27
0,28
1,0
1,6
```
*(truncated for brevity)*

The first line `:::row,col:::` indicated that each subsequent line contained row and column coordinates. 

## The Approach

Looking at the data format with row/column coordinates, I realized it could represent pixel positions for an image. Given the challenge name "QR Chronicals," it seemed likely that these coordinates represented black pixels in a QR code.

I decided to write a Python script to:
1. Parse the Excel file to extract the coordinates
2. Create a binary matrix where the specified coordinates would be black (0) and all other positions would be white (1)
3. Generate a QR code image from this matrix
4. Save the image so I could scan it

## The Solution

I created the following Python script to generate the QR code:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from PIL import Image
import os

# User configuration - SET YOUR EXCEL FILE PATH HERE
EXCEL_FILE_PATH = r"secret_1_.xlsx"

def read_excel_data(file_path):
    """
    Read the Excel file containing row and column data.
    Format expected: ':::row,col:::'
    """
    try:
        df = pd.read_excel(file_path, header=None)
        data = []
        
        for _, row in df.iterrows():
            # Skip header row if it exists
            if str(row[0]).strip() == ':::row,col:::':
                continue
                
            # Parse row,col values
            try:
                r, c = map(int, str(row[0]).strip().split(','))
                data.append((r, c))
            except (ValueError, TypeError):
                print(f"Warning: Skipping invalid data: {row[0]}")
                
        return data
    except Exception as e:
        print(f"Error reading Excel file: {e}")
        return None

def generate_qr_code(data_points, size=50):
    """
    Generate a QR code image from a list of (row, col) coordinates.
    """
    if not data_points:
        print("No data points to generate QR code.")
        return None
        
    # Find dimensions needed for the QR code
    max_row = max([p[0] for p in data_points]) + 1
    max_col = max([p[1] for p in data_points]) + 1
    
    # Create an empty array filled with white (1s)
    qr_array = np.ones((max(max_row, size), max(max_col, size)))
    
    # Fill in black pixels (0s) based on data points
    for r, c in data_points:
        if 0 <= r < qr_array.shape[0] and 0 <= c < qr_array.shape[1]:
            qr_array[r, c] = 0
            
    return qr_array

def save_qr_code(qr_array, output_path, scale=10):
    """
    Save the QR code as an image.
    """
    if qr_array is None:
        return False
    
    # Create a higher resolution image with clean pixels
    height, width = qr_array.shape
    img = Image.new('RGB', (width * scale, height * scale), color='white')
    
    for r in range(height):
        for c in range(width):
            if qr_array[r, c] == 0:  # Black pixel
                for i in range(scale):
                    for j in range(scale):
                        img.putpixel((c * scale + i, r * scale + j), (0, 0, 0))
    
    img.save(output_path)
    print(f"QR code saved as: {output_path}")
    return True

def main():
    print("QR Code Generator from Excel Data")
    print("=================================")
    
    # Use the file path defined at the top
    file_path = EXCEL_FILE_PATH
    
    # Check if file exists
    if not os.path.exists(file_path):
        print(f"Error: File not found at {file_path}")
        print("Please update the EXCEL_FILE_PATH variable in the script with the correct path.")
        return
    
    print(f"Reading data from: {file_path}")
    
    # Read the data
    data_points = read_excel_data(file_path)
    if not data_points:
        return
        
    print(f"Found {len(data_points)} data points.")
    
    # Generate QR code
    qr_array = generate_qr_code(data_points)
    
    # Save the QR code
    output_folder = os.path.dirname(file_path)
    base_filename = os.path.splitext(os.path.basename(file_path))[0]
    output_path = os.path.join(output_folder, f"qr_{base_filename}.png")
    
    save_qr_code(qr_array, output_path)

if __name__ == "__main__":
    main()
```

## The Result

After running the script, I received a QR code image that looked something like:

```
![qr_secret_1_](https://github.com/user-attachments/assets/040d7c26-cea5-49d4-a90e-c733b113368f)

```

## The Flag

When I scanned the QR code with my phone, it revealed the following text:
```
n00bz{qr_c0d3_1n_4_t3xt_f1l3_w0w!!!!!!}
```

Following the challenge format requirements, the final flag was:
```
LakshyaCTF{n00bz{qr_c0d3_1n_4_t3xt_f1l3_w0w!!!!!!}}
```
