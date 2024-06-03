
<!--
/InfoSec/Finals%20Prep/Images/
-->

| Title                                                     | Status             |
| --------------------------------------------------------- | ------------------ |
| Lecture 11: Cryptographic Hash Functions                  | :white_check_mark: | 
| Lecture 12: Message Authentication Codes                  | :white_check_mark: |
| Lecture 13: Digital Signatures                            | :white_check_mark: |
| Lecture 14: Cryptographic Key Management and Distribution | :white_check_mark: |

# Lecture 11: Cryptographic Hash Functions
## Introduction
- **Definition:** A hash function ( H ) accepts a variable-length block of data ( M ) and produces a fixed-size result ( h = H(M) ) called a hash value or hash code.
- **Primary Objective:** Ensure data integrity.
- **Property:** Any change in ( M ) results in a change in the hash value with high probability.
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
	- Seed hash + message without encryption
	- Seed Hash + Message before encryption

## Digital Signatures
- **Mechanism:** The hash value of a message is encrypted with the sender's private key.
- **Verification:** Anyone with the sender's public key can verify the message's integrity but to alter it would need to know the private key as well.
- **Example:**
	- Encrypt hash with private key, decrypt with public key
	- Same as above but encrypt with symmetric key

## Password Verification
- **Mechanism:** Passwords are hashed and stored. During login, the entered password is hashed and compared to the stored hash.
- **Security:** Protects against password theft by storing only the hash.

## Simple Hash Function
- **Process:** Input as a sequence of ( n )-bit blocks processed iteratively.
- **XOR Hash Function:** Bit-by-bit XOR of every block.
- **Problems: **
	- **Effectiveness:** Effective for random data, probability of unchanged hash value due to data error is ( 2<sup>-n</sup> ).
	- **Example:** For a 128-bit hash value, effective probability for normal text files with high-order bit zero is ( 2<sup>-112</sup> ).
- **Improvement:**
	- **Circular Shift:** Perform a one-bit circular shift on the hash value after each block.
	- **Procedure:**
	  1. Initialize ( n )-bit hash value to zero.
	  2. For each ( n )-bit block:
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
- **Input:** Message with a maximum length of less than ( 2^{128} ) bits. In 1024-bit blocks
- **Output:** 512-bit message digest.

### SHA-512 Steps
1. **Append Padding Bits:** Length congruent to 896 modulo 1024, padding consists of one 1 bit followed by necessary 0 bits.
2. **Append Length:** Append 128-bit block containing the length of the original message before padding.
3. **Initialize Hash Buffer:** 512-bit buffer as eight 64-bit registers.
	- **Values:**
		- a = 6A09E667F3BCC908
		- b = BB67AE8584CAA73B
		- c = 3C6EF372FE94F82B
		- d = A54FF53A5F1D36F1
		- e = 510E527FADE682D1
		- f = 9B05688C2B3E6C1F
		- g = 1F83D9ABFB41BD6B
		- h = 5BE0CD19137E2179
4. **Round Function:**
	- Each current block is hashed with the previous output (the buffer contents for the first block) for N number of blocks
	- Perform Round & Addition for each block
	- The round function processes each 1024-bit block using a series of logical functions and bitwise operations to update the hash value.

---

# Lecture 12: Message Authentication Codes
## Message Authentication Requirements
- **MAC Definition**
	- Verify integrity of the message and the authenticity of the sender
	- A signature counters repudiation
- **Attacks on Comms across a network**
	- Disclosure
	- Traffic analysis
	- Masquerade
	- Modifications
		- Sequence, Timing & Content
	- Source/Distance repudiation


## Message Authentication Functions
1. **Lower Level**: Produces an authenticator, a value used to authenticate a message.
	1. **Hash Function**: Maps a message of any length into a fixed-length hash value, serving as the authenticator.
	2. **Message Encryption**: The ciphertext of the entire message serves as its authenticator.
	3. **Message Authentication Code (MAC)**: A function of the message and a secret key that produces a fixed-length value serving as the authenticator.
2. **Higher Level**: Utilizes the authenticator in a protocol that enables a receiver to verify the authenticity of a message.


## Message Encryption
- **Can Encryption be used as authentication?**
	- Yes/No?
		- Yes if private key is used
	- Symmetric?
		- Already does
	- Asymmetric?
		- Need private key for auth, public key for sigs
- **Diagrams Explained**
	- A
		- ![](/InfoSec/Finals%20Prep/Images/Pasted%20image%2020240603230643.png)
			- Symmetric grants confidentiality & authentication
				- Required -> Key and message for encryption
	- B
		- ![](/InfoSec/Finals%20Prep/Images/Pasted%20image%2020240603230747.png)
			- Public-Key grants confidentiality
				- Required -> Public Key for encryption
	- C
		- ![](/InfoSec/Finals%20Prep/Images/Pasted%20image%2020240603230754.png)
			- Public-Key grants Authentication & Signature
				- Required -> Private Key for encryption
	- D
		- ![](/InfoSec/Finals%20Prep/Images/Pasted%20image%2020240603230810.png)
			- Public-Key grants Confidentiality, Authentication & Signature
				- Required -> Private Key for encryption, Public key for signature

## Frame Check Sequence (FCS Checksum)
- Provides error control in case message integrity is tampered/corrupted
- **Diagrams**
	- Internal Error Control
		- Calc checksum, append to end of message and encrypt
		- Compare at the receiver side after decryption
	- External Error Control
		- Encrypt message, calc checksum and append to encrypted message
		- Extract checksum and compare at sender side

## Message Authentication Code (MAC)
- Similar to FCS
- A and B share a common secret Key K
- MAC calculated via C(K,M) and appended to message
- B Calculates MAC and compares the received MAC
	- If match
		- Assured that the message has not been altered and that the message is from the alleged sender.

## MACs Based on Block Ciphers
1. **DAA (Data Authentication Algorithm)**
	- **Description**: DAA is based on the Data Encryption Standard (DES). It uses DES in a cryptographic mode that ensures data integrity and authenticity.
	- **Details**: The DAA algorithm involves applying DES in cipher block chaining (CBC) mode to produce a fixed-length output (often 64 bits) from any input length. The algorithm ensures that any modification to the message will result in a different MAC, which the receiver can detect.
1. **CMAC (Cipher-based Message Authentication Code)**
	- **Description**: CMAC is a block cipher-based MAC algorithm that is designed to provide message authentication. It can be used with any block cipher, including AES and DES.
	- **Details**: CMAC involves encrypting the message using a block cipher in a specific mode (typically CBC), then processing the final block with a special key.
		- This key is derived from the original encryption key using a defined method, ensuring the integrity and authenticity of the message.
		- The final encryption MSB yields the Length of Message T
	- **Flaw:** An adversary can exploit CBC MAC when given the CBC MAC of a one-block message ( X ):
		- If ( T = MAC(K, X) )
			- The adversary knows the CBC MAC for the two-block message ( X \|\| (X  +  T) ), which is also ( T ).
				- It cannot be used for variable length messages:
					- T1 = MAC(M1)
					- T2 = MAC(M2 + T1) = MAC(M1 \|\| M2)

---

# Lecture 13: Digital Signatures
## Digital Signatures Overview
- **Purpose**: Message authentication protects two parties exchanging messages from any third party but does not protect the two parties from each other.
- **Flaws**
	- **Forgery**: One party (e.g., Mary) may forge a message and claim it came from the other (e.g., John). Mary would simply have to create a message and append an authentication code using the key that John and Mary share.
	- **Denial**: One party (e.g., John) can deny sending a message since it is possible for Mary to forge a message.
- **Properties**
	- **Verification**: Must verify the author, date, and time of the signature.
	- **Authentication**: Must authenticate the contents at the time of the signature.
	- **Third-Party Verification**: Must be verifiable by third parties to resolve disputes.
	- **Inclusion of Authentication Function**: Digital signature functions include the authentication function.
- **Requirements**
	- The signature must be a bit pattern that depends on the message.
	- It must use information only known to the sender to prevent forgery and denial.
	- Production and verification of the digital signature must be relatively easy.
	- It must be computationally infeasible to forge the signature.
	- It must be practical to store a copy of the digital signature.

## Direct Digital Signatures
- **Definition**: Involves only the communicating parties (source and destination) with the destination knowing the public key of the source.
- **Security**: Depends on the security of the sender’s private key.
- **Threats**:
	- **Denial**: A sender may claim that the private key was lost or stolen to deny sending a message.
	- **Actual Theft**: If a private key is stolen, an opponent can send a message signed with the sender's signature and backdate it.

## ElGamal Digital Signature Scheme

### Key Generation
- **Global Elements**: A prime number (q) and a primitive root (α) of (q).
- **User A's Key Pair**: Generated as follows:
	1. Select a private key (x) such that (1 < x < q-1).
	2. Compute the public key (y) as (y = α^x mod q).

### Signature Generation
1. Choose a random integer (k) such that (1 < k < q-1) and gcd(k, q-1) = 1.
2. Compute S<sub>1</sub> = (α<sup>k</sup> mod q) .
	1. This is basically the same as Elgammal C1
3. Compute k<sup>-1</sup> mod (q-1) .
4. Compute S<sub>2</sub> = k<sup>-1</sup>e(m - X<sub>A</sub>S<sub>1</sub>) mod (q-1) .
5. The signature is the pair (S<sub>1</sub>, S<sub>2</sub>).

### Signature Verification
1. Verify that ( 0 < r < q ) and ( 0 < s < q-1 ).
2. Compute v<sub>1</sub> = α<sup>m</sup> mod q.
3. Compute v<sub>2</sub> = Y<sub>A</sub><sup>S<sub>1</sub></sup> S<sub>1</sub><sup>S<sub>2</sub></sup> mod q.
4. The signature is valid if ( v1 = v2 ).

### NIST Digital Signature Algorithm (DSA)
- **Overview**: DSA is a Federal Information Processing Standard for digital signatures.
- **Key Generation**: Involves generating a private key ( x ) and a corresponding public key ( y ).
- **Signature Generation**:
	1. Generate a random number ( k ).
	2. Compute r = (g<sup>k</sup> mod p) mod q .
	3. Compute s = (k<sup>H(m)</sup> + xr)) mod q .
- **Signature Verification**:
	1. Compute w = s'<sup>-1</sup> mod q .
	2. Compute u1 = (H(m)w) mod q
	3. Compute u2 = (r'w) mod q .
	4. Compute v = ((g<sup>u1</sup> y<sup>u2</sup>) mod p) mod q .
	5. The signature is valid if ( v = r').

### Elliptic Curve Digital Signature Algorithm (ECDSA)

#### Process Overview
- **Elements Involved**:
	- **Global Domain Parameters**: Defines an elliptic curve ( E ) and a base point ( G ) on ( E ).
	- **Key Generation**:
		- Select a random integer ( d ) as the private key.
		- Compute the public key ( Q = dG ).
	- **Signature Generation**:
		1. Compute the hash ( e = H(m) ).
		2. Select a random integer ( k ).
		3. Compute ( R = kG ) and ( r = R_x mod n ) (where ( R_x ) is the x-coordinate of ( R )).
		4. Compute ( s = k<sup>-1</sup>(e + dr) mod n ).
		5. The signature is the pair ( (r, s) ).
	- **Signature Verification**:
		1. Verify ( r ) and ( s ) are in the correct range.
		2. Compute ( e = H(m) ).
		3. Compute ( w = s^{-1} mod n ).
		4. Compute ( u1 = ew mod n ) and ( u2 = rw mod n ).
		5. Compute ( R = u1G + u2Q ) and ( v = R_x mod n ).
		6. The signature is valid if ( v = r ).

---

# Lecture 14: Cryptographic Key Management and Distribution
## Methods of Key Distribution
1. **Physical Delivery by A**: A can select a key and physically deliver it to B.
2. **Third-Party Selection**: A third party can select the key and physically deliver it to A and B.
3. **Using Previous Keys**: If A and B have previously and recently used a key, one party can transmit the new key to the other, encrypted using the old key.
4. **Encrypted Connection to a Third Party**: If A and B each have an encrypted connection to a third party C, C can deliver a key on the encrypted links to A and B.

## Key Distribution using a 3rd party
### Key Translation
- **Sender (A) sends a request**: A generates a session key (Ks), encrypts it using its master key (Kma), and sends this to the KTC.
- **KTC creates a session**: The KTC decrypts the session key (Ks) using Kma, then re-encrypts it using the receiver's (B's) master key (Kmb).
- **Receiver (B) can now create a session**: B decrypts the session key (Ks) using Kmb and establishes a secure session with A using Ks.

### Key Translation with Key Forwarding
- **Sender (A) sends a request**: A generates a session key (Ks), encrypts it using its master key (Kma), and sends this to the KTC.
- **KTC re-encrypts the session key**: The KTC decrypts Ks using Kma, then re-encrypts it using B's master key (Kmb).
- **KTC sends the re-encrypted session key to A**: A receives the session key encrypted with Kmb.
- **A forwards the session key to B**: A sends the encrypted session key (Ks encrypted with Kmb) to B.
- **Receiver (B) decrypts the session key**: B decrypts Ks using Kmb and establishes a secure session with A using Ks.

### Key Distribution
- **Sender (A) requests a session key**: A sends a request to the KDC for a session key (Ks) to use with B.
- **KDC generates the session key**: The KDC generates Ks.
- **KDC encrypts the session key for A and B**: The KDC encrypts Ks with A's master key (Kma) and B's master key (Kmb).
- **KDC sends the encrypted session keys to A and B**: A receives Ks encrypted with Kma, and B receives Ks encrypted with Kmb.
- **Both A and B establish a secure session**: A and B decrypt Ks using their respective master keys and use Ks for secure communication.

### Key Distribution with Key Forwarding
- **Sender (A) requests a session key**: A sends a request to the KDC for a session key (Ks) to use with B.
- **KDC generates the session key**: The KDC generates Ks.
- **KDC encrypts the session key for A and B**: The KDC encrypts Ks with A's master key (Kma) and B's master key (Kmb).
- **KDC sends both encrypted keys to A**: A receives Ks encrypted with Kma and Ks encrypted with Kmb.
- **A forwards the session key to B**: A sends the session key encrypted with Kmb to B.
- **Both A and B establish a secure session**: A and B decrypt Ks using their respective master keys and use Ks for secure communication.


### Symmetric Key Distribution Using Asymmetric Encryption
#### Simple Secret Key Distribution
- **A generates a key pair**:
    - A creates a public key (PUa) and a private key (PRa).
    - A sends PUa and an identifier (IDA) to B.
- **B generates a secret key**:
    - B creates a secret session key (Ks).
    - B encrypts Ks using A's public key (PUa) and sends the encrypted key to A.
- **A recovers the secret key**:
    - A decrypts the received message using its private key (PRa) to get Ks.
    - Only A can decrypt this message, so only A and B know Ks.
- **Keys are discarded**:
    - A discards both its public key (PUa) and private key (PRa).
    - B discards A's public key (PUa).

#### Man-in-the-Middle (MITM) Attack
- **A generates a key pair**:
    - A creates a public key (PUa) and a private key (PRa).
    - A sends PUa and an identifier (IDA) to B.
- **D (the attacker) intercepts the message**:
    - D intercepts A's message to B.
    - D generates its own public key (PUd) and private key (PRd).
    - D sends PUd and IDA to B, pretending to be A.
- **B generates a secret key**:
    - B creates a secret session key (Ks).
    - B encrypts Ks using D's public key (PUd) (believing it to be A's public key) and sends the encrypted key to A (which actually goes to D).
- **D intercepts the message**:
    - D intercepts B's message containing E(PUd, Ks).
    - D decrypts the message using its private key (PRd) to obtain Ks.
- **D transmits the key to A**:
    - D encrypts Ks using A's public key (PUa).
    - D sends E(PUa, Ks) to A.

### Secret Key Distribution with Confidentiality and Authentication
- **A initiates communication**:
    - A encrypts a message with B's public key (PUb).
    - The message contains A's identifier (IDA) and a nonce (N1), which uniquely identifies the transaction.
    - A sends the encrypted message to B.
- **B responds with authentication**:
    - B decrypts A's message using its private key (PRb).
    - B sends a message back to A, encrypted with A's public key (PUa).
    - This message contains the nonce N1 (proving B received A's message) and a new nonce (N2) generated by B.
    - Because only B could decrypt A's initial message and include N1 in its response, A is assured that the message is from B.
- **A confirms its identity**:
    - A encrypts the nonce N2 using B's public key (PUb) and sends it to B.
    - This step confirms to B that the correspondent is indeed A.
- **A sends the secret key (Ks)**:
    - A selects a secret key (Ks) for secure communication.
    - A encrypts Ks first with A's private key (PRa) and then with B's public key (PUb), creating message M = E(PUb, E(PRa, Ks)).
    - A sends M to B. Encryption with B's public key ensures only B can read it, and encryption with A's private key ensures the message is authentically from A.
- **B retrieves the secret key**:
    - B decrypts the received message M using its private key (PRb) to obtain E(PRa, Ks).
    - B then decrypts this using A's public key (PUa) to retrieve the secret key Ks.
    - This ensures that the key Ks was indeed sent by A and can now be used for secure communication.

## Distribution of Public Keys

### Public Announcement of Public Keys
- Anyone can forge a public announcement.
- That is, some user could pretend to be user A and send a public key to another participant or broadcast such a public key.
- Until user A discovers the forgery and alerts other participants, the forger can read all encrypted messages intended for A and use the forged keys for authentication.

### Publicly Available Directory
1. The authority maintains a directory with a {name, public key} entry for each participant.
2. Each participant registers a public key with the directory authority. Registration would have to be in person or by some form of secure, authenticated communication.
3. A participant may replace the existing key with a new one at any time, either because of the desire to replace a public key that has already been used for a large amount of data or because the corresponding private key has been compromised.
4. Participants could access the directory electronically. Secure, authenticated communication from the authority to the participant is mandatory.

### Public-Key Authority
- **A requests B’s public key**:
    - A sends a timestamped message to the public-key authority requesting B’s current public key.
- **Authority responds with B’s public key**:
    - The authority responds with a message encrypted with its private key (PRauth). This message includes:
        - B’s public key (PUb).
        - The original request, allowing A to match the response with its request and verify it wasn't altered.
        - The original timestamp, ensuring the response is timely and not outdated.
- **A verifies and uses B’s public key**:
    - A decrypts the authority's message using the authority’s public key (PUauth) to obtain B’s public key (PUb).
    - A encrypts a message to B containing its identifier (IDA) and a nonce (N1) using PUb to ensure only B can read it.
- **B requests A’s public key**:
    - B sends a similar request to the public-key authority for A’s current public key.
- **Authority responds with A’s public key**:
    - The authority responds with a message encrypted with its private key (PRauth), containing A’s public key (PUa), the original request, and the timestamp.
- **B verifies and uses A’s public key**:
    - B decrypts the authority's message using the authority’s public key (PUauth) to obtain A’s public key (PUa).
    - B encrypts a message to A with PUa, containing A’s nonce (N1) and a new nonce (N2), ensuring only A can read it. The presence of N1 assures A that the message is from B.
- **A confirms its identity to B**:
    - A encrypts N2 using B’s public key (PUb) and sends it to B.
    - This step assures B that the correspondent is indeed A.

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
- Suppose A has obtained a certificate from certification authority X1 and B has obtained a certificate from CA X2.
- If A does not securely know the public key of X2, then B’s certificate issued by X2 is useless to A.
	- A can read B’s certificate but cannot verify the signature.

However, if the two CAs have securely exchanged their own public keys, the following procedure will enable A to obtain B’s public key:

1. Obtain from the directory the certificate of X2 signed by X1.
2. Because A securely knows X1’s public key, A can obtain X2’s public key from its certificate and verify it using X1’s signature on the certificate.
3. A then goes back to the directory and obtains the certificate of B signed by X2.
4. A now has a trusted copy of X2’s public key, A can verify the signature and securely obtain B’s public key.

### PKI Scenario

![](/InfoSec/Finals%20Prep/Images/Pasted%20image%2020240604013816.png)

- **Key Generation by Bob**:
    - Bob generates a pair of keys: a public key and a private key.
- **Application for Certificate**:
    - Bob sends a request to the Registration Authority (RA) for a public key certificate. This includes Bob's public key and identity information.
- **Verification by Registration Authority (RA)**:
    - The RA verifies Bob's identity and details. Once verified, the RA forwards Bob's certificate request to the Certification Authority (CA).
- **Certificate Issuance by Certification Authority (CA)**:
    - The CA creates Bob's public key certificate, which binds Bob's identity to his public key.
    - The CA signs the certificate with its own private key to ensure its authenticity.
- **Certificate Storage**:
    - Bob's public key certificate is stored in a repository, which may also contain certificate revocation lists (CRLs).
- **Certificate Retrieval by Alice**:
    - When Alice needs to verify Bob's signature on a document, she retrieves Bob's public key certificate from the repository.
- **Verification Process by Alice**:
    - Alice uses the CA's public key to verify the signature on Bob's public key certificate.
    - Once verified, Alice uses Bob's public key to verify the signature on the document signed by Bob.