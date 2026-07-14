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

