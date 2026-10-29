# Playbook: security and cryptography

**Covers:** security goals and threat modeling, classical ciphers, symmetric cryptography (block and stream ciphers, modes of operation), hash functions, MACs and authenticated encryption, public-key cryptography (RSA, Diffie–Hellman, elliptic curves), digital signatures, PKI and certificates, protocols (TLS, SSH, Kerberos, OAuth 2.0 and OpenID Connect), authentication and password storage, access control models, software vulnerabilities (memory corruption, injection, XSS, CSRF), defenses (ASLR, stack canaries, NX/DEP, sandboxing, CSP), network security (firewalls, IDS), side channels, post-quantum cryptography.

## What a complete answer contains

- **Threat model first:** what is being protected (the assets), from whom (the adversary's capabilities), and where the trust boundaries are. Then name the goal: confidentiality, integrity, availability, authenticity, non-repudiation. Most security mistakes come from protecting against the wrong adversary.
- **For a cryptographic primitive:**
  - the underlying math (modular arithmetic, groups, finite fields, the hardness assumption such as factoring or discrete log);
  - the algorithm step by step, with a complete worked example using tiny numbers. For example, RSA with p = 61 and q = 53: compute n, φ(n), choose e, find d with the extended Euclidean algorithm, then encrypt and decrypt a number;
  - the formal security definition it meets (IND-CPA, IND-CCA, EUF-CMA, collision resistance);
  - **how it breaks when misused:** ECB mode leaking patterns (the "ECB penguin"), nonce reuse in AES-GCM or stream ciphers, textbook RSA being malleable and deterministic, padding oracles, length-extension attacks on Merkle–Damgård hashes used as MACs.
- **For a protocol:** a message diagram showing what each party sends, what each message proves, and which attack each step prevents (replay, man-in-the-middle, downgrade). The canonical example is the TLS 1.3 handshake: ephemeral Diffie–Hellman key exchange, the certificate, CertificateVerify, Finished, and why it takes one round trip.
- **For a vulnerability:**
  - explain it from its root cause at the mechanism level. A stack buffer overflow needs a stack-frame diagram showing the buffer, the saved frame pointer and the return address. SQL injection needs the query string before and after concatenation, showing how the parser sees attacker data as code. XSS needs the same-origin policy and the browser's parsing context;
  - then give each defense and exactly why it works, and what it doesn't stop: parameterized queries, output encoding, ASLR, stack canaries, NX, CSP, memory-safe languages;
  - map it to the OWASP Top 10 and the CWE category, and use well-known real incidents as case studies (Heartbleed, CVE-2014-0160; Log4Shell, CVE-2021-44228).
- **Standards:** AES is NIST FIPS 197 (2001), SHA-2 is FIPS 180-4, and SHA-3 is FIPS 202 (2015). NIST's first post-quantum standards came out in August 2024: FIPS 203 (ML-KEM, from Kyber), FIPS 204 (ML-DSA, from Dilithium) and FIPS 205 (SLH-DSA, from SPHINCS+).
- **Ethics and practice:** teach attacks so the student understands defenses. Point practice toward legal environments: deliberately vulnerable apps (OWASP Juice Shop, DVWA), CTF competitions, and the student's own lab machines. Teach exploitation at the level of concepts and lab exercises. Don't help attack systems the student isn't authorized to test.

## Comparison dimensions

Symmetric versus asymmetric (speed, key distribution, key sizes at equivalent security, such as AES-128 ≈ RSA-3072 ≈ a 256-bit elliptic curve), hashing versus encryption versus encoding, MAC versus signature, authentication versus authorization, the security guarantee versus the performance cost.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| c. 1st century BC | Julius Caesar | The shift cipher |
| 9th century | al-Kindi | The first known description of frequency analysis, the start of cryptanalysis |
| 1553 | Giovan Battista Bellaso | The polyalphabetic cipher later misattributed to Vigenère |
| 1883 | Auguste Kerckhoffs | Kerckhoffs's principle: a system should be secure even if everything except the key is public |
| 1917 | Gilbert Vernam | The one-time pad |
| 1932 | Marian Rejewski (Polish Cipher Bureau) | Broke Enigma. The work continued at Bletchley Park with Alan Turing and others |
| 1949 | Claude Shannon | "Communication Theory of Secrecy Systems": perfect secrecy, and the proof that the one-time pad achieves it |
| 1975 | Jerome Saltzer and Michael Schroeder | "The Protection of Information in Computer Systems": least privilege, fail-safe defaults, economy of mechanism, and the other design principles |
| 1976 | Whitfield Diffie and Martin Hellman, building on Ralph Merkle's work | "New Directions in Cryptography": public-key key exchange (Turing Award 2015) |
| 1977 | Rivest, Shamir and Adleman | RSA (Turing Award 2002). Clifford Cocks at GCHQ found an equivalent scheme in 1973, kept classified until 1997 |
| 1977 | IBM, standardized by NBS | DES, based on Horst Feistel's Lucifer design |
| 1979 | Robert Morris and Ken Thompson | "Password Security: A Case History": salted password hashing in Unix |
| 1985 | Neal Koblitz; Victor Miller | Elliptic-curve cryptography, independently |
| 1988 | Robert Tappan Morris | The Morris worm, which exploited a buffer overflow in `fingerd` among other flaws |
| 1994 | Peter Shor | A quantum algorithm for factoring and discrete log. It is the reason for post-quantum cryptography |
| 1996 | Aleph One | "Smashing the Stack for Fun and Profit" in *Phrack* |
| 1998 | Jeff Forristal | Early public documentation of SQL injection, in *Phrack* |
| 1999 | Niels Provos and David Mazières | bcrypt |
| 2000–01 | Joan Daemen and Vincent Rijmen | Rijndael selected as AES |
| 2004; 2017 | Xiaoyun Wang et al.; Google and CWI ("SHAttered") | Practical collisions for MD5; a collision for SHA-1 |
| 2015 | Password Hashing Competition | Argon2 selected |
| 2018 | Several teams | Spectre and Meltdown, speculative-execution side channels |
| 2024 | NIST | The first post-quantum cryptography standards (FIPS 203, 204 and 205) |

## Canonical sources

- Katz and Lindell, *Introduction to Modern Cryptography* (rigorous, definitions and proofs)
- Boneh and Shoup, *A Graduate Course in Applied Cryptography* (free online)
- Ferguson, Schneier and Kohno, *Cryptography Engineering*
- Ross Anderson, *Security Engineering* (free online)
- William Stallings, *Cryptography and Network Security*
- The OWASP Top 10 and Cheat Sheet Series, MITRE CWE, and the NIST FIPS and SP 800 publications
- Dan Boneh's Cryptography I course (Coursera)

## Classic misconceptions

- "Hashing is encryption." Hashing is one-way with no key; encryption is reversible with the key.
- "Base64 is encryption." It is an encoding with no secret at all.
- "Encryption guarantees integrity." Unauthenticated encryption can be modified undetectably. Use authenticated encryption (AES-GCM, ChaCha20-Poly1305).
- "Store passwords with SHA-256." Fast hashes are made for speed, which helps attackers guessing passwords. Use a slow, salted password hash (Argon2, scrypt, bcrypt).
- "HTTPS means the site is trustworthy." It means the connection is to *that* domain and is encrypted; phishing sites have valid certificates too.
- "Longer keys are always stronger." Key length is only comparable within the same algorithm family; a 256-bit elliptic-curve key is far stronger than a 1024-bit RSA key.
- "Security through obscurity works." It violates Kerckhoffs's principle. Obscurity can add delay, but it can't be the foundation.
- "I'll write my own crypto." Correct primitives are routinely broken by implementation details: timing, nonce handling, padding.

## Question patterns

- Encrypt and decrypt with RSA, or perform a Diffie–Hellman exchange, with small numbers.
- Which security property does this scheme fail, and how would an attacker exploit it?
- Draw the stack frame and explain how this overflow overwrites the return address. Which defenses stop it?
- Fix this SQL injection, and explain why the fix works at the parser level.
- Threat-model this application: assets, adversaries, attack surface, mitigations.
- Why does TLS 1.3 use ephemeral key exchange? What is forward secrecy?

## Tools and artifacts to show

CyberChef, the `openssl` command line (generate keys, inspect certificates with `openssl x509 -text`), Wireshark for a TLS handshake, `gdb` with stack-frame inspection on a deliberately vulnerable lab binary, Burp Suite Community against OWASP Juice Shop, and Python's `cryptography` library.
