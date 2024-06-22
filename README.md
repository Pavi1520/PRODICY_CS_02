from PIL import Image
import numpy as np

def encrypt_image(input_image_path, output_image_path, key):
    # Open the image
    image = Image.open(input_image_path)
    
    # Convert image to numpy array for faster pixel manipulation
    img_array = np.array(image)
    
    # Encrypt each pixel with XOR operation
    encrypted_img_array = np.bitwise_xor(img_array, key)
    
    # Convert encrypted array back to image
    encrypted_image = Image.fromarray(encrypted_img_array)
    
    # Save the encrypted image
    encrypted_image.save(output_image_path)
    print(f"Encrypted image saved as {output_image_path}")

def decrypt_image(input_image_path, output_image_path, key):
    # Open the encrypted image
    encrypted_image = Image.open(input_image_path)
    
    # Convert image to numpy array
    encrypted_img_array = np.array(encrypted_image)
    
    # Decrypt each pixel with XOR operation
    decrypted_img_array = np.bitwise_xor(encrypted_img_array, key)
    
    # Convert decrypted array back to image
    decrypted_image = Image.fromarray(decrypted_img_array)
    
    # Save the decrypted image
    decrypted_image.save(output_image_path)
    print(f"Decrypted image saved as {output_image_path}")

# Example usage:
input_image = "input_image.jpg"
encrypted_image_path = "encrypted_image.jpg"
decrypted_image_path = "decrypted_image.jpg"
encryption_key = np.random.randint(0, 256, size=(300, 400, 3), dtype=np.uint8)  # Generate a random encryption key

# Encrypt the image
encrypt_image(input_image, encrypted_image_path, encryption_key)

# Decrypt the image (using the same key)
decrypt_image(encrypted_image_path, decrypted_image_path, encryption_key)
