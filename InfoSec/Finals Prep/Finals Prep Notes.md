> [!WARNING]
> Used GPT to convert pptx files into md files, only those marked with :white_check_mark: have been processed

| Title                                                     | Status             |
| --------------------------------------------------------- | ------------------ |
| Lecture 11: Cryptographic Hash Functions                  | :white_check_mark: |
| Lecture 12: Message Authentication Codes                  | :warning:          |
| Lecture 13: Digital Signatures                            | :warning:          |
| Lecture 14: Cryptographic Key Management and Distribution | :warning:          |

# Lecture 11: Cryptographic Hash Functions
## Introduction
- **Definition:** A hash function \( H \) accepts a variable-length block of data \( M \) and produces a fixed-size result \( h = H(M) \) called a hash value or hash code.
- **Primary Objective:** Ensure data integrity.
- **Property:** Any change in \( M \) results in a change in the hash value with high probability.
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
- **Flaw:** Susceptible to a MITM attack
	- Attacker modifies contents of the message without the hash and recomputes the hash to match
- **Flows:** Methods of Authentication
	- Encrypt message+hash before sending
	- Encrypt hash before sending
	- #### WARN: 2 more but diagram ki smjh nhi aarhi


## Digital Signatures
- **Mechanism:** The hash value of a message is encrypted with the sender's private key.
- **Verification:** Anyone with the sender's public key can verify the message's integrity but to alter it would need to know the private key as well.
- **Example:**
	- #### WARN: Cant understand diagrams

## Password Verification
- **Mechanism:** Passwords are hashed and stored. During login, the entered password is hashed and compared to the stored hash.
- **Security:** Protects against password theft by storing only the hash.

## Simple Hash Function
- **Process:** Input as a sequence of \( n \)-bit blocks processed iteratively.
- **XOR Hash Function:** Bit-by-bit XOR of every block.
- **Problems: **
	- **Effectiveness:** Effective for random data, probability of unchanged hash value due to data error is \( 2<sup>-n</sup> \).
	- **Example:** For a 128-bit hash value, effective probability for normal text files with high-order bit zero is \( 2<sup>-112</sup> \).
- **Improvement:**
	- **Circular Shift:** Perform a one-bit circular shift on the hash value after each block.
	- **Procedure:**
	  1. Initialize \( n \)-bit hash value to zero.
	  2. For each \( n \)-bit block:
	     - Rotate hash value left by one bit.
	     - XOR block into hash value.

## Requirements and Security
| **Requirement**                                      | **Description**                                                                                                  |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Variable input size                                  | H can be applied to a block of data of any size.                                                                 |
| Fixed output size                                    | H produces a fixed-length output.                                                                                |
| Efficiency                                           | H(x) is relatively easy to compute for any given x, making both hardware and software implementations practical. |
| Preimage resistant (one-way property)                | For any given hash value h, it is computationally infeasible to find y such that H(y) = h.                       |
| Second preimage resistant (weak collision resistant) | For any given block x, it is computationally infeasible to find y ≠ x with H(y) = H(x).                          |
| Collision resistant (strong collision resistant)     | It is computationally infeasible to find any pair (x, y) with x ≠ y, such that H(x) = H(y).                      |
| Pseudorandomness                                     | Output of H meets standard tests for pseudorandomness.                                                           |

## Hash Properties for Hash Functions
|                                         | Preimage Resistant | Second Preimage Resistant | Collision Resistant |
| --------------------------------------- | ------------------ | ------------------------- | ------------------- |
| Hash + digital signature                | yes                | yes                       | yes*                |
| Intrusion detection and virus detection |                    | yes                       |                     |
| Hash + symmetric encryption             |                    |                           |                     |
| One-way password file                   | yes                |                           |                     |
| MAC                                     | yes                | yes                       | yes*                |
- **Property Definitions**
	- **Pre-image Resistance:** Difficult to find any input xxx that maps to a specific hash hhh.
	- **Second Pre-image Resistance:** Difficult to find any second input x′x'x′ such that H(x)=H(x′)H(x) = H(x')H(x)=H(x′).
	- **Collision Resistance:** Difficult to find any two distinct inputs xxx and x′x'x′ such that H(x)=H(x′)H(x) = H(x')H(x)=H(x′).


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

# Lecture 14: Cryptographic Key Management and Distribution
## Key Distribution Options
For two parties A and B, key distribution can be achieved in several ways:

1. **Physical Delivery by A**: A can select a key and physically deliver it to B.
2. **Third-Party Selection**: A third party can select the key and physically deliver it to A and B.
3. **Using Previous Keys**: If A and B have previously and recently used a key, one party can transmit the new key to the other, encrypted using the old key.
4. **Encrypted Connection to a Third Party**: If A and B each have an encrypted connection to a third party C, C can deliver a key on the encrypted links to A and B.

## Key Distribution Between Two Communicating Entities

### Key Hierarchy
- **Description**: The key hierarchy establishes different levels of keys with specific roles. For instance, master keys, session keys, and encryption keys. Each level of keys serves a different purpose and provides different levels of security.

### Symmetric Key Distribution Using Asymmetric Encryption

#### Simple Secret Key Distribution
- **Diagram**: Two parties exchange a secret key using a simple protocol where one party sends the key encrypted with the other's public key.
- **Explanation**:
    1. **Initiator A**: Encrypts the secret key with the public key of responder B and sends it.
    2. **Responder B**: Decrypts the received message with its private key to obtain the secret key.

#### Man-in-the-Middle (MITM) Attack
- **Diagram**: An attacker intercepts the communication between A and B.
- **Explanation**:
    1. The attacker intercepts the public key sent from A to B.
    2. The attacker sends its own public key to B, pretending to be A.
    3. B encrypts the secret key with the attacker's public key.
    4. The attacker decrypts the message, reads the secret key, re-encrypts it with the real public key of B, and forwards it.

### Secret Key Distribution with Confidentiality and Authentication
- **Diagram**: An improved protocol that ensures both confidentiality and authentication.
- **Explanation**:
    1. **Initiator A**: Encrypts the secret key with B's public key and signs the message with its private key.
    2. **Responder B**: Verifies the signature using A's public key and decrypts the message with its private key to obtain the secret key.

## Distribution of Public Keys

### Public Announcement of Public Keys
Anyone can forge a public announcement. That is, some user could pretend to be user A and send a public key to another participant or broadcast such a public key. Until user A discovers the forgery and alerts other participants, the forger can read all encrypted messages intended for A and use the forged keys for authentication.

### Publicly Available Directory
1. The authority maintains a directory with a {name, public key} entry for each participant.
2. Each participant registers a public key with the directory authority. Registration would have to be in person or by some form of secure, authenticated communication.
3. A participant may replace the existing key with a new one at any time, either because of the desire to replace a public key that has already been used for a large amount of data or because the corresponding private key has been compromised.
4. Participants could access the directory electronically. Secure, authenticated communication from the authority to the participant is mandatory.

This scheme is more secure than individual public announcements but still has vulnerabilities. If an adversary obtains or computes the private key of the directory authority, the adversary could authoritatively pass out counterfeit public keys and impersonate any participant and eavesdrop on messages sent to any participant. Another way to achieve the same end is for the adversary to tamper with the records kept by the authority.

### Public-Key Authority
The public-key authority could be a bottleneck in the system, as a user must appeal to the authority for a public key for every other user it wishes to contact. As before, the directory of names and public keys maintained by the authority is vulnerable to tampering.

### Public-Key Certificates

#### X.509 Certificates
ITU-T recommendation X.509 is part of the X.500 series of recommendations that define a directory service. X.509 defines a framework for the provision of authentication services by the X.500 directory to its users. X.509 is an important standard because the certificate structure and authentication protocols defined in X.509 are used in a variety of contexts.

#### X.509 Public-Key Certificate Use
- **Diagram**: Illustrates how public key certificates are used in authentication.
- **Explanation**:
    1. **Unsigned Certificate**: Contains user ID and user’s public key.
    2. **Generate Hash**: Create a hash code of the unsigned certificate.
    3. **Sign Certificate**: Use the CA’s private key to form a signature on the hash code.
    4. **Verify Algorithm**: The recipient uses the CA’s public key to verify the signature.

#### X.509 Certificate Format
- **Diagram**: Shows the structure of an X.509 certificate.
- **Components**:
    - Version
    - Certificate Serial Number
    - Signature Algorithm Identifier
    - Issuer Name
    - Validity Period (Not Before, Not After)
    - Subject’s Public Key Information
    - Issuer Unique Identifier (Optional)
    - Subject Unique Identifier (Optional)
    - Extensions (Optional)
    - Signature

### How to Verify the Certificate
Suppose A has obtained a certificate from certification authority X1 and B has obtained a certificate from CA X2. If A does not securely know the public key of X2, then B’s certificate issued by X2 is useless to A. A can read B’s certificate but cannot verify the signature.

However, if the two CAs have securely exchanged their own public keys, the following procedure will enable A to obtain B’s public key:

1. Obtain from the directory the certificate of X2 signed by X1. Because A securely knows X1’s public key, A can obtain X2’s public key from its certificate and verify it using X1’s signature on the certificate.
2. A then goes back to the directory and obtains the certificate of B signed by X2. Because A now has a trusted copy of X2’s public key, A can verify the signature and securely obtain B’s public key.

### Example PKI Scenario
- **Diagram**: Illustrates a Public Key Infrastructure (PKI) scenario.
- **Explanation**:
    - **Entities**:
        - **Certification Authority (CA)**: Issues and manages certificates.
        - **Registration Authority (RA)**: Handles the registration process for users.
        - **End User**: Utilizes the certificates for secure communication.
    - **Process**:
        1. **Request for Certificate**: The end user requests a certificate from the RA.
        2. **Issuing Certificate**: The CA issues the certificate and the user can now use it for secure communication.
        3. **Using Certificates**: The end user can now use their private key to sign messages and others can use the corresponding public key to verify the signatures.