# clahe
import cv2
import os

def apply_clahe(input_path, output_path, clip_limit=2.0, tile_grid_size=(8, 8)):
    # Load the image
    image = cv2.imread(input_path)
    
    # Split the image into color channels
    b, g, r = cv2.split(image)
    
    # Create a CLAHE object for each channel
    clahe = cv2.createCLAHE(clipLimit=clip_limit, tileGridSize=tile_grid_size)
    
    # Apply CLAHE to each color channel
    clahe_b = clahe.apply(b)
    clahe_g = clahe.apply(g)
    clahe_r = clahe.apply(r)
    
    # Merge the color channels back into an image
    clahe_image = cv2.merge((clahe_b, clahe_g, clahe_r))
    
    # Save the processed image
    cv2.imwrite(output_path, clahe_image)

# Input directory containing images
input_directory = 'input_images/'

# Output directory for processed images
output_directory = 'processed_images/'

# Create the output directory if it doesn't exist
os.makedirs(output_directory, exist_ok=True)

# Loop through each image in the input directory
for input_image in os.listdir(input_directory):
    input_path = os.path.join(input_directory, input_image)
    output_image = os.path.join(output_directory, 'clahe_' + input_image)
    apply_clahe(input_path, output_image)

print("CLAHE preprocessing complete.")


#bil
import cv2
import os

def apply_bilateral_filter(input_path, output_path, diameter=9, sigma_color=75, sigma_space=75):
    # Load the image
    image = cv2.imread(input_path)
    
    # Apply bilateral filter
    filtered_image = cv2.bilateralFilter(image, diameter, sigma_color, sigma_space)
    
    # Save the processed image
    cv2.imwrite(output_path, filtered_image)

# Input directory containing images
input_directory = 'input_images/'

# Output directory for processed images
output_directory = 'processed_images_bilateral/'

# Create the output directory if it doesn't exist
os.makedirs(output_directory, exist_ok=True)

# Loop through each image in the input directory
for input_image in os.listdir(input_directory):
    input_path = os.path.join(input_directory, input_image)
    output_image = os.path.join(output_directory, 'bilateral_' + input_image)
    apply_bilateral_filter(input_path, output_image)

print("Bilateral filter preprocessing complete.")
