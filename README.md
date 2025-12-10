def encrypt_char(char, shift):
    # --- Logic for UPPERCASE Letters ---
    if 'A' <= char <= 'Z':
        # Subtract ord('A') to map 'A' to 0, 'B' to 1, etc.
        original_pos = ord(char) - ord('A')
        
        # Add shift, apply modulo 26 for wrapping
        new_pos = (original_pos + shift) % 26
        
        # Add ord('A') back to get the new ASCII value
        new_ascii = new_pos + ord('A')
        
        # Convert ASCII back to character
        return chr(new_ascii)
        
    # --- Logic for LOWERCASE Letters ---
    elif 'a' <= char <= 'z':
        # Subtract ord('a') to map 'a' to 0, 'b' to 1, etc.
        original_pos = ord(char) - ord('a')
        
        # Add shift, apply modulo 26 for wrapping
        new_pos = (original_pos + shift) % 26
        
        # Add ord('a') back to get the new ASCII value
        new_ascii = new_pos + ord('a')
        
        # Convert ASCII back to character
        return chr(new_ascii)
        
    else:
        # If it's not a letter (space, number, punctuation), return it unchanged
        return char


def caesar_encrypt(message, shift):
    # This empty string will store our result
    result_message = ""
    
    # Loop through every character and apply encryption/decryption logic
    for char in message:
        # Use our existing function to process the current character
        processed_char = encrypt_char(char, shift)
        
        # Add the processed character to our result string
        result_message += processed_char
        
    return result_message


# --- User Interaction Code (Main Program) ---
def main():
    print("\n--- Prodigy InfoTech Task 01: Caesar Cipher Tool ---")
    
    # 1. Get the operation choice
    choice = input("Do you want to (E)ncrypt or (D)ecrypt? Enter E or D: ").upper()
    
    if choice in ['E', 'D']:
        # 2. Get the message from the user
        message = input("Enter the message: ")
        
        # 3. Get the shift value
        try:
            # We use try/except to catch errors if the user enters non-numbers
            shift = int(input("Enter the shift value (a number, e.g., 3): "))
        except ValueError:
            print("Invalid shift value. Please enter a whole number.")
            return

        # 4. Adjust the shift for decryption
        if choice == 'D':
            # Decryption is simply encryption with the negative shift
            final_shift = -shift
            action = "Decryption"
        else: # choice == 'E'
            final_shift = shift
            action = "Encryption"
            
        print(f"\nPerforming {action} with shift: {shift}")
            
        # 5. Run the core function
        result = caesar_encrypt(message, final_shift)
        
        # 6. Display the result
        print("---------------------------------")
        print(f"RESULT: {result}")
        print("---------------------------------")
        
    else:
        print("Invalid choice. Please enter E for Encrypt or D for Decrypt.")

# This line is standard practice to start the 'main' function
if __name__ == "__main__":
    main()
