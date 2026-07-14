# Task 1-Caesar Cipher

# Encryption Function
def encrypt(text, shift):
    encrypted_text = ""

    for char in text:
        if char.isalpha():
            if char.isupper():
                encrypted_text += chr((ord(char) - ord('A') + shift) % 26 + ord('A'))
            else:
                encrypted_text += chr((ord(char) - ord('a') + shift) % 26 + ord('a'))
        else:
            encrypted_text += char

    return encrypted_text


# Decryption Function
def decrypt(text, shift):
    decrypted_text = ""

    for char in text:
        if char.isalpha():
            if char.isupper():
                decrypted_text += chr((ord(char) - ord('A') - shift) % 26 + ord('A'))
            else:
                decrypted_text += chr((ord(char) - ord('a') - shift) % 26 + ord('a'))
        else:
            decrypted_text += char

    return decrypted_text


# User Input
message = input("Enter the message: ")
shift = int(input("Enter the shift value: "))

# Encryption
encrypted = encrypt(message, shift)
print("Encrypted Message:", encrypted)

# Decryption
decrypted = decrypt(encrypted, shift)
print("Decrypted Message:", decrypted)





# Task 2-Password Strength Checker

import string

# Take password input
password = input("Enter your password: ")

# Initialize score
score = 0

# Check minimum length
if len(password) >= 8:
    score += 1

# Check for uppercase letters
if any(char.isupper() for char in password):
    score += 1

# Check for lowercase letters
if any(char.islower() for char in password):
    score += 1

# Check for numbers
if any(char.isdigit() for char in password):
    score += 1

# Check for special characters
special_chars = string.punctuation
if any(char in special_chars for char in password):
    score += 1

# Display password strength
print("\nPassword Analysis:")
print("Length:", "✓" if len(password) >= 8 else "✗")
print("Uppercase:", "✓" if any(char.isupper() for char in password) else "✗")
print("Lowercase:", "✓" if any(char.islower() for char in password) else "✗")
print("Numbers:", "✓" if any(char.isdigit() for char in password) else "✗")
print("Special Characters:", "✓" if any(char in special_chars for char in password) else "✗")

# Determine strength
if score <= 2:
    print("\nPassword Strength: Weak")
elif score == 3 or score == 4:
    print("\nPassword Strength: Medium")
else:
    print("\nPassword Strength: Strong")


# Task 3-Password Generator

#Password Generator

import random
import string

# Characters to use in the password
letters = string.ascii_letters
numbers = string.digits
symbols = string.punctuation
all_characters = letters + numbers + symbols

# Get password length from the user
length = int(input("Enter the password length: "))

# Get the number of passwords to generate
count = int(input("How many passwords do you want to generate? "))

print("\nGenerated Password(s):")
for i in range(count):
    # Ensure the password contains at least one letter, one number, and one symbol
    password = [
        random.choice(letters),
        random.choice(numbers),
        random.choice(symbols)
    ]

    # Fill the remaining length with random characters
    password += random.choices(all_characters, k=length - 3)

    # Shuffle the password to make it random
    random.shuffle(password)

    # Convert list to string
    password = ''.join(password)

    print(f"Password {i + 1}: {password}")




# Task 4-simple_login_system
import os

FILE_NAME = "users.txt"

# Create file if it doesn't exist
if not os.path.exists(FILE_NAME):
    open(FILE_NAME, "w").close()

# Register function
def register():
    username = input("Enter a username: ")
    password = input("Enter a password: ")

    # Check if username already exists
    with open(FILE_NAME, "r") as file:
        for line in file:
            user, pwd = line.strip().split(",")
            if user == username:
                print("Username already exists!")
                return

    # Save new user
    with open(FILE_NAME, "a") as file:
        file.write(f"{username},{password}\n")

    print("Registration successful!")

# Login function
def login():
    username = input("Enter your username: ")
    password = input("Enter your password: ")

    with open(FILE_NAME, "r") as file:
        for line in file:
            user, pwd = line.strip().split(",")
            if user == username and pwd == password:
                print("Login successful! Welcome,", username)
                return

    print("Login failed! Invalid username or password.")

# Main menu
while True:
    print("\n===== LOGIN SYSTEM =====")
    print("1. Register")
    print("2. Login")
    print("3. Exit")

    choice = input("Enter your choice (1-3): ")

    if choice == "1":
        register()
    elif choice == "2":
        login()
    elif choice == "3":
        print("Thank you!")
        break
    else:
        print("Invalid choice. Please try again.")




# Task 3-Basic Text File Encryption and Decryption using XOR

# XOR function
def xor_encrypt_decrypt(data, key):
    result = bytearray()

    for byte in data:
        result.append(byte ^ key)

    return result

# Main Program
print("===== Basic Text File Encryption =====")

input_file = input("Enter the text file name (e.g., sample.txt): ")
key = int(input("Enter an encryption key (0-255): "))

try:
    # Read original file
    with open(input_file, "rb") as file:
        data = file.read()

    # Encrypt data
    encrypted_data = xor_encrypt_decrypt(data, key)

    # Save encrypted file
    encrypted_file = "encrypted_file.bin"
    with open(encrypted_file, "wb") as file:
        file.write(encrypted_data)

    print("File encrypted successfully!")
    print("Encrypted file saved as:", encrypted_file)

    # Read encrypted file
    with open(encrypted_file, "rb") as file:
        encrypted_data = file.read()

    # Decrypt data
    decrypted_data = xor_encrypt_decrypt(encrypted_data, key)

    # Save decrypted file
    decrypted_file = "decrypted_file.txt"
    with open(decrypted_file, "wb") as file:
        file.write(decrypted_data)

    print("File decrypted successfully!")
    print("Decrypted file saved as:", decrypted_file)

except FileNotFoundError:
    print("Error: File not found!")
except ValueError:
    print("Please enter a valid key between 0 and 255.")

