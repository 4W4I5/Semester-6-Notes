| Title                                    | Status    |
| ---------------------------------------- | --------- |
| Lecture 11: Cryptographic Hash Functions | :warning: |
|                                          |           |

# Lecture 11: Cryptographic Hash Functions
## Introduction
- **Definition:** A hash function \( H \) accepts a variable-length block of data \( M \) and produces a fixed-size result \( h = H(M) \) called a hash value or hash code.
- **Primary Objective:** Ensure data integrity.
- **Property:** Any change in \( M \) results in a change in the hash value with high probability.

## Cryptographic Hash Function
- **One-way property:** Computationally infeasible to find a data object that maps to a pre-specified hash result.
- **Collision-free property:** Computationally infeasible to find two data objects that map to the same hash result.
- **Usage:** Verify if data has changed.

## Applications of Cryptographic Hash Functions
- **Message Authentication:** Ensures the data received is exactly as sent and verifies the sender's identity.
- **Digital Signatures:** Verifies the integrity and origin of a message using the sender's private key.
- **One-way Password Files:** Stores password hashes instead of plaintext passwords for security.
- **Virus Detection:** Identifies changes in software that might indicate a virus.
- **Pseudorandom Number Generator:** Generates numbers that are computationally indistinguishable from random sequences.

## Message Authentication
- **Mechanism:** Verifies the integrity of a message and ensures it has not been altered.
- **Message Digest:** A hash value used to authenticate a message.

## Man-in-the-Middle (MITM) Attack
- **Description:** An attacker intercepts and possibly alters the communication between two parties.
- **Prevention:** Use of secure hash functions and cryptographic protocols to detect alterations and verify authenticity.

## Digital Signatures
- **Mechanism:** The hash value of a message is encrypted with the sender's private key.
- **Verification:** Anyone with the sender's public key can verify the message's integrity.
- **Example:** Digital certificates in SSL/TLS protocols.

## Examples of Digital Signatures
- **SSL/TLS Certificates:** Ensure secure communication over the internet.
- **Code Signing:** Verifies the integrity and origin of software applications.

## Password Verification
- **Mechanism:** Passwords are hashed and stored. During login, the entered password is hashed and compared to the stored hash.
- **Security:** Protects against password theft by storing only the hash.

## Simple Hash Function
- **Process:** Input as a sequence of \( n \)-bit blocks processed iteratively.
- **XOR Hash Function:** Bit-by-bit XOR of every block.

## Problem with Simple Hash Function
- **Effectiveness:** Effective for random data, probability of unchanged hash value due to data error is \( 2^{-n} \).
- **Example:** For a 128-bit hash value, effective probability for normal text files with high-order bit zero is \( 2^{-112} \).

## Improvement of Simple Hash Function
- **Circular Shift:** Perform a one-bit circular shift on the hash value after each block.
- **Procedure:**
  1. Initialize \( n \)-bit hash value to zero.
  2. For each \( n \)-bit block:
     - Rotate hash value left by one bit.
     - XOR block into hash value.

## Requirements and Security
- **Pre-image Resistance:** Difficult to find any input \( x \) that maps to a specific hash \( h \).
- **Second Pre-image Resistance:** Difficult to find any second input \( x' \) such that \( H(x) = H(x') \).
- **Collision Resistance:** Difficult to find any two distinct inputs \( x \) and \( x' \) such that \( H(x) = H(x') \).

## Hash Properties for Hash Functions
- **Deterministic:** Same input always produces the same output.
- **Quick Computation:** Hash function should be efficient to compute.
- **Small Changes:** Any small change to the input should produce a significantly different hash.
- **Fixed Output Size:** The output hash should have a fixed size, regardless of the input size.

## Secure Hash Algorithm (SHA)
### SHA-512 Logic
- **Input:** Message with a maximum length of less than \( 2^{128} \) bits.
- **Output:** 512-bit message digest.
- **Processing:** In 1024-bit blocks.

### SHA-512 Steps
1. **Append Padding Bits:** Length congruent to 896 modulo 1024, padding consists of one 1 bit followed by necessary 0 bits.
2. **Append Length:** Append 128-bit block containing the length of the original message.
3. **Initialize Hash Buffer:** 512-bit buffer as eight 64-bit registers.
   - \( a = 6A09E667F3BCC908 \)
   - \( b = BB67AE8584CAA73B \)
   - \( c = 3C6EF372FE94F82B \)
   - \( d = A54FF53A5F1D36F1 \)
   - \( e = 510E527FADE682D1 \)
   - \( f = 9B05688C2B3E6C1F \)
   - \( g = 1F83D9ABFB41BD6B \)
   - \( h = 5BE0CD19137E2179 \)

4. **Round Function:**
   - The round function processes each 1024-bit block using a series of logical functions and bitwise operations to update the hash value.
   - **Example Rounds:**
     - **Message Schedule:** Prepare 80 words from the 1024-bit block.
     - **Compression Function:** Update the hash value with bitwise operations, modular additions, and logical functions.

---

# Lecture 12: Message Authentication Codes
### Message Authentication Requirements
In the context of communications across a network, the following attacks can be identified:
- Disclosure
- Traffic analysis
- Masquerade
- Content modification
- Sequence modification
- Timing modification
- Source repudiation
- Destination repudiation

Message authentication is a procedure to verify that received messages come from the alleged source and have not been altered. It may also verify sequencing and timeliness. A digital signature is an authentication technique that also includes measures to counter repudiation by the source.

### Message Authentication Functions
Any message authentication or digital signature mechanism has two levels of functionality:
1. **Lower Level**: Produces an authenticator, a value used to authenticate a message.
2. **Higher Level**: Utilizes the authenticator in a protocol that enables a receiver to verify the authenticity of a message.

### Authenticator Functions
1. **Hash Function**: Maps a message of any length into a fixed-length hash value, serving as the authenticator.
2. **Message Encryption**: The ciphertext of the entire message serves as its authenticator.
3. **Message Authentication Code (MAC)**: A function of the message and a secret key that produces a fixed-length value serving as the authenticator.

### Message Encryption
- **Can Encryption be used as authentication?**
  - Yes/No?
  - Symmetric?
  - Asymmetric?


### Message Authentication Code (MAC)
An alternative authentication technique involves using a secret key to generate a small fixed-size block of data known as a cryptographic checksum or MAC, appended to the message. This technique assumes that two communicating parties (say A and B) share a common secret key (K). When A sends a message to B, it calculates the MAC as follows:

\[ \text{MAC} = C(K, M) \]

If the received MAC matches the calculated MAC, then:
- The receiver is assured that the message has not been altered.
- The receiver is assured that the message is from the alleged sender.


### MACs Based on Block Ciphers
Two methods:
1. **DAA (Data Authentication Algorithm)**
   - **Description**: DAA is based on the Data Encryption Standard (DES). It uses DES in a cryptographic mode that ensures data integrity and authenticity.
   - **Details**: The DAA algorithm involves applying DES in cipher block chaining (CBC) mode to produce a fixed-length output (often 64 bits) from any input length. The algorithm ensures that any modification to the message will result in a different MAC, which the receiver can detect.
   - *[Added for clarity]*
2. **CMAC (Cipher-based Message Authentication Code)**
   - **Description**: CMAC is a block cipher-based MAC algorithm that is designed to provide message authentication. It can be used with any block cipher, including AES and DES.
   - **Details**: CMAC involves encrypting the message using a block cipher in a specific mode (typically CBC), then processing the final block with a special key. This key is derived from the original encryption key using a defined method, ensuring the integrity and authenticity of the message.
   - *[Added for clarity]*

### CBC MAC (CMAC)
**Description**:
- An adversary can exploit CBC MAC when given the CBC MAC of a one-block message \( X \):
  - If \( T = \text{MAC}(K, X) \)
  - The adversary knows the CBC MAC for the two-block message \( X \parallel (X \oplus T) \), which is also \( T \).

**Attack on CMAC:**
- It cannot be used for variable length messages:
  - \( T1 = \text{MAC}(M1) \)
  - \( T2 = \text{MAC}(M2 \oplus T1) = \text{MAC}(M1 \parallel M2) \)


### Frame Check Sequence /Checksum

Frame Check Sequence (FCS) or Checksum is an error-detecting code commonly used in data communications. It ensures that the data received is the same as the data sent by computing a value based on the data's binary content and sending this value along with the data. The receiver performs the same computation and compares the result. Any discrepancy indicates an error.

---

# Lecture 13: Digital Signatures
### Digital Signatures Overview
- **Purpose**: Message authentication protects two parties exchanging messages from any third party but does not protect the two parties from each other. Various disputes can arise, such as:
  - **Forgery**: One party (e.g., Mary) may forge a message and claim it came from the other (e.g., John). Mary would simply have to create a message and append an authentication code using the key that John and Mary share.
  - **Denial**: One party (e.g., John) can deny sending a message since it is possible for Mary to forge a message.

### Digital Signature Properties
- **Verification**: Must verify the author, date, and time of the signature.
- **Authentication**: Must authenticate the contents at the time of the signature.
- **Third-Party Verification**: Must be verifiable by third parties to resolve disputes.
- **Inclusion of Authentication Function**: Digital signature functions include the authentication function.

### Digital Signature Requirements
- The signature must be a bit pattern that depends on the message.
- It must use information only known to the sender to prevent forgery and denial.
- Production and verification of the digital signature must be relatively easy.
- It must be computationally infeasible to forge the signature.
- It must be practical to store a copy of the digital signature.

### Direct Digital Signatures
- **Definition**: Involves only the communicating parties (source and destination) with the destination knowing the public key of the source.
- **Security**: Depends on the security of the sender’s private key.
- **Threats**:
  - **Denial**: A sender may claim that the private key was lost or stolen to deny sending a message.
  - **Actual Theft**: If a private key is stolen, an opponent can send a message signed with the sender's signature and backdate it.

### ElGamal Digital Signature Scheme

#### Key Generation
- **Global Elements**: A prime number \( q \) and a primitive root \( \alpha \) of \( q \).
- **User A's Key Pair**: Generated as follows:
  1. Select a private key \( x \) such that \( 1 < x < q-1 \).
  2. Compute the public key \( y \) as \( y = \alpha^x \mod q \).

#### Signature Generation
1. Choose a random integer \( k \) such that \( 1 < k < q-1 \) and \( \gcd(k, q-1) = 1 \).
2. Compute \( r = (\alpha^k \mod q) \).
3. Compute \( k^{-1} \mod (q-1) \).
4. Compute \( s = (k^{-1} (H(m) - xr)) \mod (q-1) \).
5. The signature is the pair \( (r, s) \).

#### Signature Verification
1. Verify that \( 0 < r < q \) and \( 0 < s < q-1 \).
2. Compute \( v1 = \alpha^{H(m)} \mod q \).
3. Compute \( v2 = (y^r r^s) \mod q \).
4. The signature is valid if \( v1 = v2 \).

#### Example
- For example, let \( q = 23 \), \( \alpha = 5 \), \( x = 6 \), \( y = 8 \), \( k = 15 \), and message \( m = "Hello" \).
- Follow the steps to generate and verify the signature (details would involve specific calculations based on the steps above).

### NIST Digital Signature Algorithm (DSA)
- **Overview**: DSA is a Federal Information Processing Standard for digital signatures.
- **Key Generation**: Involves generating a private key \( x \) and a corresponding public key \( y \).
- **Signature Generation**:
  1. Generate a random number \( k \).
  2. Compute \( r = (g^k \mod p) \mod q \).
  3. Compute \( s = (k^{-1}(H(m) + xr)) \mod q \).
- **Signature Verification**:
  1. Compute \( w = s^{-1} \mod q \).
  2. Compute \( u1 = (H(m)w) \mod q \) and \( u2 = (rw) \mod q \).
  3. Compute \( v = ((g^{u1} y^{u2}) \mod p) \mod q \).
  4. The signature is valid if \( v = r \).

### Elliptic Curve Digital Signature Algorithm (ECDSA)

#### Process Overview
- **Elements Involved**:
  - **Global Domain Parameters**: Defines an elliptic curve \( E \) and a base point \( G \) on \( E \).
  - **Key Generation**:
    - Select a random integer \( d \) as the private key.
    - Compute the public key \( Q = dG \).
  - **Signature Generation**:
    1. Compute the hash \( e = H(m) \).
    2. Select a random integer \( k \).
    3. Compute \( R = kG \) and \( r = R_x \mod n \) (where \( R_x \) is the x-coordinate of \( R \)).
    4. Compute \( s = k^{-1}(e + dr) \mod n \).
    5. The signature is the pair \( (r, s) \).
  - **Signature Verification**:
    1. Verify \( r \) and \( s \) are in the correct range.
    2. Compute \( e = H(m) \).
    3. Compute \( w = s^{-1} \mod n \).
    4. Compute \( u1 = ew \mod n \) and \( u2 = rw \mod n \).
    5. Compute \( R = u1G + u2Q \) and \( v = R_x \mod n \).
    6. The signature is valid if \( v = r \).

#### Global Domain Parameters
- **Parameters**:
  - The elliptic curve \( E \) over a finite field \( \mathbb{F}_p \) or \( \mathbb{F}_{2^m} \).
  - A base point \( G \) with large order \( n \).
  - The field size \( p \) or \( 2^m \), and the coefficients defining the curve.

#### Key Generation, Digital Signature Generation, and Verification
- **Key Generation**: Select private key \( d \), compute public key \( Q = dG \).
- **Digital Signature Generation**: Generate \( r \) and \( s \) as detailed above.
- **Digital Signature Verification**: Verify \( r \) and \( s \) using the steps detailed above.

---

# Lecture 14: C