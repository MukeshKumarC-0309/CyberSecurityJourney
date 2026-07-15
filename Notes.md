# Base 64
Base64 is a binary-to-text encoding that uses 64 printable characters to represent each 6-bit segment of a sequence of byte values. As for all binary-to-text encodings, Base64 encoding enables transmitting binary data on a communication channel that only supports text.When comparing the original data to the resulting encoded data, Base64 encoding increases the size by 33% plus about 4% additional if inserting line breaks for typical line length.        

# Caeser Cipher
In cryptography, a Caesar cipher, also known as Caesar's cipher, the shift cipher, Caesar's code, or Caesar shift, is one of the simplest and most widely known encryption techniques. It is a type of substitution cipher in which each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet. For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.The method is named after Julius Caesar, who used it in his private correspondence.
The encryption step performed by a Caesar cipher is often incorporated as part of more complex schemes, such as the Vigenère cipher, and still has modern application in the ROT13 system. As with all single-alphabet substitution ciphers, the Caesar cipher is easily broken and in modern practice offers essentially no communications security.              

# Vigenère cipher
The Vigenère cipher is a method of encrypting alphabetic text where each letter of the plaintext is encoded with a different Caesar cipher, whose increment is determined by the corresponding letter of another text, the key.For example, if the plaintext is attacking tonight and the key is oculorhinolaryngology, then        
* the first letter of the plaintext, a, is shifted by 14 positions in the alphabet (because the first letter of the key, o, is the 14th letter of the alphabet, counting from zero), yielding o;        
* the second letter, t, is shifted by 2 (because the second letter of the key, c, is the 2nd letter of the alphabet, counting from zero) yielding v;        
* the third letter, t, is shifted by 20 (u), yielding n, with wrap-around;        
and so on.      
The Vigenère cipher is therefore a special case of a polyalphabetic substitution.            
