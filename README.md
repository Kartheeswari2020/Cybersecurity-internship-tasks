# Caesar Cipher

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

