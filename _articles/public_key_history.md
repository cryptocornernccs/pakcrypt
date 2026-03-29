---
layout: post
title: "History of Public Key Cryptography"
---

This article traces the history of public key cryptography from its classified origins in the 1960s through the post-quantum era of today. The narrative is deliberately person-centered, focusing on the individuals who made groundbreaking discoveries, their backgrounds, education, and the contexts that shaped their contributions. The field represents one of the most remarkable stories in modern science—a revolution that transformed how humanity secures digital communication.

---

## <span style="color: seagreen;"> **Part I: The Secret Origins (1969-1975)** </span>

### The GCHQ Trinity: Ellis, Cocks, and Williamson

The story of public key cryptography begins not in an American university, but in the classified corridors of Britain's Government Communications Headquarters (GCHQ), the UK's signals intelligence agency. For nearly three decades, this breakthrough remained one of the most closely guarded secrets in cryptography.

#### James H. Ellis (1924-1997)

**Background and Education:** James Henry Ellis was born in 1924 in Britain. He studied physics and electronics, developing a strong foundation in applied mathematics and engineering principles. Unlike many of his academic counterparts, Ellis spent his entire career in government service, working at the intersection of communications technology and security.

**The 1969 Breakthrough:** By the late 1960s, Ellis was working at GCHQ on the problem of key management. Military communications were becoming increasingly distributed, with more devices deployed at lower levels of command. The traditional method of physically distributing keys via couriers was becoming prohibitively expensive and operationally cumbersome.

In 1969, Ellis conceived the revolutionary idea that would become known as **non-secret encryption**—the conceptual foundation of public key cryptography. He realized that it might be possible for two parties to establish secure communication without having to exchange secret keys in advance. This insight came purely from theoretical reasoning about the nature of cryptography itself.

Ellis's breakthrough was conceptual rather than practical. He proved that such a system was theoretically possible, but he could not construct a working implementation. That would come later from his colleagues.

**Legacy:** Ellis's work remained classified until 1997, the year of his death. Only then did GCHQ reveal that British intelligence had invented public key cryptography years before the academic world. Ellis never received public recognition during his lifetime, though his contribution is now acknowledged as the conceptual birth of the field.

#### Clifford C. Cocks (born 1950)

**Background and Education:** Clifford Christopher Cocks was born in 1950 in Britain. He studied mathematics at Cambridge University, graduating with exceptional mathematical training in number theory—a field that would prove crucial to his later work.

**The 1973 Discovery:** In 1973, shortly after joining GCHQ, Cocks was shown Ellis's problem: the need for a mathematical implementation of non-secret encryption. Within a day, Cocks devised what we now know as the **RSA cryptosystem**—three years before Rivest, Shamir, and Adleman would independently discover it in the public domain.

Cocks's insight was elegant and profound: use the multiplication of large prime numbers as the mathematical foundation. The security would rest on the computational difficulty of factoring the product of two large primes—a problem that had stumped mathematicians for centuries.

**The Mathematics:** Cocks's scheme (identical to RSA) works as follows:
- Choose two large prime numbers, p and q
- Compute n = p × q (the public modulus)
- The public key consists of n and an encryption exponent
- The private key uses knowledge of p and q for decryption

**Career:** Cocks spent his entire career at GCHQ, eventually rising to senior positions. He continued working on cryptographic problems until his retirement. Unlike his academic counterparts, he could not publish his work or receive public academic recognition for decades.

**Recognition:** In 1997, when GCHQ declassified the work, Cocks finally received public acknowledgment. He has since been recognized by the cryptographic community, including receiving the IACR Fellow designation and the IEEE Millennium Medal. In 2008, he was made a Companion of the Order of the Bath for his services to cryptography.

#### Malcolm J. Williamson (1948-2015)

**Background and Education:** Malcolm John Williamson was born in 1948. Like Cocks, he studied mathematics at Cambridge, developing expertise in algebra and number theory. He joined GCHQ shortly after Cocks, becoming part of the same small research group.

**The 1974 Contribution:** In 1974, Williamson made his own crucial contribution. Working with Ellis's framework, he developed what we now call the **Diffie-Hellman key exchange**—a method for two parties to establish a shared secret key over an insecure channel, without having previously shared any secret information.

Williamson's method used modular exponentiation in a way that made it computationally infeasible for an eavesdropper to determine the shared secret, even if they intercepted all communications. This was mathematically equivalent to what Diffie and Hellman would publish in 1976.

**Career:** Williamson continued at GCHQ throughout his career, working as a consultant until 2015, the year of his death. His work, like that of Ellis and Cocks, remained classified until 1997.

**The GCHQ Legacy:** The GCHQ trio's work represents one of the most remarkable examples of parallel discovery in scientific history. They achieved what would later win the Turing Award for Diffie and Hellman, but did so in complete secrecy, motivated by national security rather than academic recognition.

---

## <span style="color: seagreen;"> **Part II: The Public Revolution (1976-1978)** </span>

### Whitfield Diffie (born 1944)

**Background and Education:** Whitfield Diffie was born on June 5, 1944, in New York City. He came from an intellectual family and developed an early interest in mathematics. He earned his B.S. in Mathematics from the Massachusetts Institute of Technology (MIT) in 1965.

After MIT, Diffie worked at MITRE Corporation and spent time as a resident guest at the MIT Artificial Intelligence Laboratory, where he was exposed to cutting-edge computer science research. He was particularly influenced by Marvin Minsky's work on artificial intelligence.

**The Journey (1973-1974):** By 1973, Diffie had become obsessed with cryptography. He took a leave of absence from Stanford (where he had enrolled as a graduate student) to travel across the United States, seeking out anyone with knowledge of cryptography. At the time, almost all cryptographic research was classified by the NSA, and what little existed in the open literature was scattered and incomplete.

Diffie was driven by two specific problems:
1. The key distribution problem: How could two parties communicate securely without having previously exchanged secret keys?
2. The digital signature problem: How could someone authenticate a digital message in a way that was legally binding?

**Meeting Hellman (1974):** In the fall of 1974, Diffie visited Stanford University to meet Martin Hellman, a professor of electrical engineering. What was planned as a half-hour meeting stretched into an entire afternoon, followed by dinner and discussion late into the evening. Hellman later described it as finding an "intellectual soul mate."

**The Collaboration:** Diffie and Hellman began working together immediately. Diffie secured a position at Stanford to support his cryptography research. In 1975, Hellman encouraged Diffie to formally enroll as a doctoral student under his supervision, which Diffie did for the fall semester.

**Ralph Merkle's Contribution:** Around this time, they became aware of similar independent work by Ralph Merkle, then a Master's student at UC Berkeley. Merkle had developed "Merkle's Puzzles"—an early key exchange protocol. Hellman encouraged Merkle to enroll at Stanford, which he did in 1976.

**The 1976 Breakthrough:** In November 1976, Diffie and Hellman published "New Directions in Cryptography" in *IEEE Transactions on Information Theory*. The paper opened with a bold statement: "We stand today on the brink of a revolution in cryptography."

The paper introduced:
1. **The Diffie-Hellman Key Exchange**: A practical method for two parties to establish a shared secret over an insecure channel
2. **The concept of public-key cryptosystems**: A framework for encryption using pairs of mathematically related keys
3. **Digital signatures**: A method for authenticating digital messages

**Later Career:** Diffie never completed his Ph.D. at Stanford—he admitted he "was not very good at being a student." However, in 1992, the Swiss Federal Institute of Technology (ETH) awarded him an honorary doctorate.

Diffie became manager of secure systems research at Northern Telecom through the 1980s. In 1992, he co-authored *Privacy on the Line* with Susan Landau. In 2010, he joined ICANN as Vice President for Information Security and Cryptography.

**Awards and Recognition:**
- IEEE Donald G. Fink Prize Paper Award (1981)
- NIST/NSA National Computer Systems Security Award (1996, with Hellman)
- ACM Kanellakis Award (1997, with Hellman)
- IEEE Kobayashi Award (1999, with Hellman and Merkle)
- IEEE Richard W. Hamming Medal (2010, with Hellman and Merkle)
- **ACM A.M. Turing Award (2015, with Hellman)**
- National Inventors Hall of Fame (2011)
- Fellow of the Royal Society (2017)

### Martin E. Hellman (born 1945)

**Background and Education:** Martin Edward Hellman was born in 1945 in New York City. He earned his B.E. in Electrical Engineering from New York University in 1966, followed by an M.S. (1967) and Ph.D. (1969) from Stanford University, all in electrical engineering.

**Academic Career:** Hellman joined the faculty at MIT in 1969, then moved to Stanford University in 1971, where he would spend the rest of his academic career. He became a full professor and established himself as a leading researcher in information theory.

**The 1974 Meeting:** Hellman's meeting with Diffie in 1974 transformed his research direction. He recognized the revolutionary potential of Diffie's ideas and committed himself fully to the collaboration.

**The 1976 Paper:** Hellman co-authored "New Directions in Cryptography" with Diffie. The paper's impact cannot be overstated—it fundamentally redefined what cryptography could achieve and opened entirely new research directions.

**Key Contributions:**
1. **Diffie-Hellman Key Exchange**: The practical implementation of public-key distribution
2. **The concept of trapdoor functions**: Mathematical functions that are easy to compute in one direction but difficult to reverse without special knowledge
3. **Digital signatures**: The authentication mechanism that would enable electronic commerce

**Later Career:** Hellman became Professor Emeritus at Stanford in 1996. In the 1980s, he worked with Soviet scientists to foster dialogue on nuclear weapons reduction. He has been a vocal advocate for international peace and cooperation.

**Awards:** Hellman shares all the major awards with Diffie, including the 2015 Turing Award.

### Ralph C. Merkle (born 1952)

**Background and Education:** Ralph Charles Merkle was born on February 2, 1952, in Berkeley, California. He came from a scientific family—his father directed Project Pluto, a U.S. Air Force nuclear ramjet program, and his sister Judith became a historical novelist.

Merkle earned his B.A. in Computer Science from UC Berkeley in 1974, followed by an M.S. in 1977. He then pursued his Ph.D. at Stanford under Martin Hellman's supervision, completing it in 1979.

**The 1974 Undergraduate Discovery:** As an undergraduate at Berkeley in 1974, Merkle conceived "Merkle's Puzzles"—a method for secure key exchange over an insecure channel. This was one of the earliest examples of public-key cryptography, predating even Diffie and Hellman's published work.

Merkle submitted his idea as a class project, but his professors showed little interest. The idea languished until Merkle learned about Diffie and Hellman's work at Stanford.

**Joining the Diffie-Hellman Team:** In 1976, Merkle joined Diffie and Hellman at Stanford for the summer, then formally enrolled as Hellman's doctoral student that fall. His Ph.D. thesis, titled "Secrecy, Authentication, and Public Key Systems," laid important theoretical foundations.

**Additional Contributions:**
1. **Merkle Trees** (1979): A data structure for efficient verification of large datasets, now fundamental to blockchain technology
2. **Merkle-Damgård Construction**: A method for building cryptographic hash functions
3. **Merkle-Hellman Knapsack Cryptosystem** (1978): One of the first public-key cryptosystems (later broken)

**Later Career:** After Stanford, Merkle worked at Elxsi (1980-1988) and Xerox PARC (1988-1999). At PARC, he designed the Khufu and Khafre block ciphers and the Snefru hash function.

Since the late 1990s, Merkle has focused on nanotechnology and cryonics. He became a Distinguished Professor at Georgia Tech (2003-2006) and has been a senior research fellow at the Institute for Molecular Manufacturing.

**Awards:**
- ACM Paris Kanellakis Theory and Practice Award (1996, with Diffie and Hellman)
- IEEE Kobayashi Award (1999, with Diffie and Hellman)
- RSA Award in Mathematics (2000)
- IEEE Richard W. Hamming Medal (2010, with Diffie and Hellman)
- National Inventors Hall of Fame (2011)
- Levchin Prize for Real-World Cryptography (2020)

### Ronald L. Rivest (born 1947)

**Background and Education:** Ronald Linn Rivest was born on May 6, 1947, in Schenectady, New York. He grew up in Niskayuna, a suburb of Schenectady. He attended public schools and graduated from Niskayuna High School in 1965.

Rivest earned his B.A. in Mathematics from Yale University in 1969. He then pursued graduate studies at Stanford University, where he had the extraordinary privilege of studying under two Turing Award winners: his Ph.D. supervisor Robert Floyd, and close collaborator Don Knuth. Rivest received his Ph.D. in Computer Science from Stanford in 1973.

**Postdoctoral Work:** After Stanford, Rivest spent a year at INRIA in Rocquencourt, France, before joining the faculty at MIT in 1974, where he has remained ever since.

**The RSA Discovery (1977):** In 1976, Rivest read Diffie and Hellman's "New Directions in Cryptography" and became fascinated by the challenge of finding a practical implementation of public-key cryptography. Working with Adi Shamir and Leonard Adleman—both also at MIT—Rivest spent months trying various approaches.

The breakthrough came in 1977. Rivest realized that the difficulty of factoring large numbers could provide the necessary one-way function. The RSA algorithm was born.

**The Algorithm:** RSA works as follows:
- Choose two large prime numbers p and q
- Compute n = p × q
- Choose public exponent e such that 1 < e < φ(n) and gcd(e, φ(n)) = 1
- Compute private exponent d where d × e ≡ 1 (mod φ(n))
- Public key: (n, e); Private key: d

**RSA Data Security:** In 1983, Rivest, Shamir, and Adleman founded RSA Data Security to commercialize their invention. The company played a crucial role in making strong cryptography widely available. In 1995, VeriSign was spun off from RSA's certification services business, becoming the dominant certificate authority for the early internet.

**Later Contributions:** Rivest has made numerous other contributions to cryptography and computer science:
- **RC4 Stream Cipher** (1987): One of the most widely used stream ciphers
- **MD5 Hash Function** (1991): A widely used (though now broken) hash function
- **Introduction to Algorithms** (1990): Co-authored the definitive textbook on algorithms with Cormen, Leiserson, and Stein—over 1 million copies sold

**Current Position:** Rivest is the Andrew and Erna Viterbi Professor of Computer Science at MIT, a member of CSAIL, and a leader of MIT's Cryptography and Information Security Group.

**Awards:**
- ACM Paris Kanellakis Theory and Practice Award (1997, with Shamir and Adleman)
- IEEE Koji Kobayashi Computers and Communications Award (2000, with Shamir and Adleman)
- **ACM A.M. Turing Award (2002, with Shamir and Adleman)**
- Marconi Prize (2007)
- National Inventors Hall of Fame (2018)

### Adi Shamir (born 1952)

**Background and Education:** Adi Shamir was born on July 6, 1952, in Tel Aviv, Israel. He earned his B.Sc. in Mathematics from Tel Aviv University in 1973. He then pursued graduate studies at the Weizmann Institute of Science, receiving his M.Sc. in 1975 and Ph.D. in Computer Science in 1977.

**Coming to MIT:** After completing his Ph.D., Shamir came to MIT as a postdoctoral researcher in 1977-1980. It was during this period that he collaborated with Rivest and Adleman on what would become RSA.

**The RSA Collaboration:** Shamir brought strong mathematical expertise to the team. His contributions to RSA included the security analysis and the mathematical proofs underlying the system.

**Later Career:** Shamir returned to Israel in 1980, joining the faculty of the Weizmann Institute of Science, where he has remained. He is the Paul and Marlene Borman Professor of Applied Mathematics.

**Major Contributions Beyond RSA:**
1. **Shamir's Secret Sharing** (1979): A method for distributing a secret among multiple parties
2. **Breaking the Merkle-Hellman Knapsack Cryptosystem** (1982): With Richard Schroeppel
3. **Differential Cryptanalysis** (1990): With Eli Biham, a powerful method for attacking block ciphers
4. **Twofish Block Cipher** (1998): One of the AES finalists

**Awards:** Shamir shares the Turing Award and other major honors with Rivest and Adleman.

### Leonard M. Adleman (born 1945)

**Background and Education:** Leonard Max Adleman was born on December 31, 1945, in California. He earned his B.A. in Mathematics from the University of California, Berkeley in 1968, followed by a Ph.D. in Computer Science from Berkeley in 1976.

**The RSA Story:** Adleman joined MIT as a faculty member in 1976. When Rivest and Shamir were working on public-key cryptography, they would frequently discuss their ideas with Adleman, who provided mathematical rigor and skepticism. Adleman's role was crucial in verifying the security of the proposed system.

Adleman has humorously noted that his initials appear last in "RSA" because he spent his time trying to break the system rather than inventing it—only when he failed to break it did they know they had something secure.

**Later Career:** Adleman returned to USC in 1980, where he is the Henry Salvatori Professor of Computer Science and Professor of Molecular Biology.

**DNA Computing:** In 1994, Adleman made a groundbreaking contribution to molecular computing by solving an instance of the Hamiltonian path problem using DNA molecules—effectively creating the field of DNA computing.

**Awards:** Adleman shares all major RSA-related awards with Rivest and Shamir.

---

## <span style="color: seagreen;"> **Part III: The Expansion Era (1980-1989)** </span>

### Taher Elgamal (born 1955)

**Background and Education:** Taher Elgamal was born in 1955 in Cairo, Egypt. His first love was mathematics, which he pursued with passion from an early age. He earned his Bachelor of Science degree from Cairo University in 1977.

Elgamal came to the United States to pursue graduate studies at Stanford University, where he earned his M.S. in 1981 and Ph.D. in Electrical Engineering in 1984. At Stanford, he met Professor Martin Hellman, who sparked his interest in cryptography. Elgamal would later describe cryptography as "the most beautiful use of math I'd ever seen."

**The 1985 Breakthrough:** In 1985, Elgamal published "A Public Key Cryptosystem and a Signature Scheme Based on Discrete Logarithms." This paper introduced:

1. **The ElGamal Encryption Scheme**: A public-key cryptosystem based on the difficulty of computing discrete logarithms in finite fields
2. **The ElGamal Signature Scheme**: A digital signature algorithm that would later influence the Digital Signature Standard (DSS)

The ElGamal encryption system works by using the difficulty of the discrete logarithm problem: given g, p, and g^x mod p, finding x is computationally infeasible for large values.

**SSL and the Internet:** From 1995-1998, Elgamal served as Chief Scientist at Netscape Communications. There, he led the development of **Secure Sockets Layer (SSL)**, the protocol that secured the early commercial internet. SSL 3.0 became the basis for TLS (Transport Layer Security), which remains the standard for web security today.

Elgamal's crucial contribution at Netscape was making SSL a free and transparent industry standard, gaining support from competitors including Microsoft. This prevented fragmentation of web security and established a single standard.

**Later Career:** After Netscape, Elgamal founded Securify (acquired by Kroll-O'Gara), served as Director of Engineering at RSA Security, and since 2013 has been CTO of Security at Salesforce.

**Awards:**
- RSA Conference Lifetime Achievement Award (2009)
- Marconi Prize (2019, with Paul Kocher)
- National Academy of Engineering (2022)

### Neal Koblitz (born 1948)

**Background and Education:** Neal I. Koblitz was born in 1948 in Washington, D.C. His father was a noted Slavic languages scholar. Koblitz showed exceptional mathematical talent early, entering Harvard University at age 16 and completing his bachelor's degree in 1969.

He earned his Ph.D. from Princeton University in 1974 under the supervision of renowned number theorist Nicholas Katz. His doctoral work focused on number theory and algebraic geometry, particularly elliptic curves.

**The 1985 Breakthrough:** In 1985, Koblitz had a breakthrough insight: the group structure of elliptic curves could be used to implement public-key cryptography. The resulting system, **Elliptic Curve Cryptography (ECC)**, offered equivalent security to RSA with dramatically smaller key sizes.

Koblitz published his findings in "Elliptic Curve Cryptosystems" in *Mathematics of Computation* in 1987.

**The Mathematics:** ECC uses the algebraic structure of elliptic curves over finite fields. The security rests on the Elliptic Curve Discrete Logarithm Problem (ECDLP): given points P and Q on an elliptic curve where Q = nP, finding n is computationally infeasible.

A 256-bit ECC key provides security comparable to a 3072-bit RSA key, making ECC ideal for resource-constrained environments.

**Later Career:** Koblitz joined the University of Washington in 1979, where he remains a Professor of Mathematics. He has been an outspoken critic of NSA influence on cryptographic standards, advocating for transparency in elliptic curve parameter selection.

**Awards:**
- Levchin Prize for Real-World Cryptography (2021)
- IACR Fellow

### Victor S. Miller (born 1947)

**Background and Education:** Victor Saul Miller was born on March 3, 1947, in Brooklyn, New York. He earned his A.B. in Mathematics from Columbia University in 1968 and his Ph.D. from Harvard University in 1975, with a dissertation on "Diophantine and p-Adic Analysis of Elliptic Curves and Modular Forms."

**Career at IBM:** Miller joined IBM's Thomas J. Watson Research Center in 1978, initially working on the IBM 801 RISC project. In 1984, he moved to the Mathematics Department, where he focused on computational number theory.

**The 1985 Discovery:** Independently of Koblitz, Miller conceived of using elliptic curves for cryptography. He published "Use of Elliptic Curves in Cryptography" at CRYPTO '85, the same year as Koblitz's paper. This simultaneous discovery demonstrated that the time was ripe for ECC.

Miller also developed the **double-and-add algorithm** for efficient computation on elliptic curves, making ECC practical for implementation.

**Other Contributions:**
- **LZW Data Compression** (1985): With Mark Wegman, the compression algorithm used in GIF and TIFF
- **Miller's Algorithm**: For efficient Weil pairing computation, fundamental to pairing-based cryptography
- **Lagarias-Miller-Odlyzko Prime Counting Algorithm**

**Later Career:** Miller left IBM in 1993 to join the Institute for Defense Analyses' Center for Communications Research in Princeton. In 2022, he joined Meta as a research scientist, and in 2023 moved to SRI International.

**Awards:**
- IEEE Millennium Medal
- RSA Award for Excellence in Mathematics (2009)
- Levchin Prize (2021, with Koblitz)
- IACR Fellow (2013)
- IEEE Fellow (2010)
- ACM Fellow (2016)

### David Chaum (born 1955)

**Background and Education:** David Chaum was born in 1955 in Los Angeles, California. He earned his Ph.D. in Computer Science from the University of California, Berkeley in 1982. His dissertation, "Computer Systems Established, Maintained, and Trusted by Mutually Suspicious Groups," laid the groundwork for much of his future work.

**The 1982-1983 Breakthroughs:** Chaum invented several foundational concepts:

1. **Blind Signatures** (1982): A form of digital signature where the content is hidden before signing, enabling anonymous digital cash
2. **Digital Cash/eCash** (1983): The first system for anonymous electronic payments
3. **Mix Networks** (1981): A system for anonymous communication that "shreds" metadata

Chaum's work established the field of **anonymous digital credentials** and influenced the development of cryptocurrencies decades later.

**The Cypherpunk Movement:** Chaum founded the International Association for Cryptologic Research (IACR) in the early 1980s when the NSA was attempting to suppress academic cryptography research. His motto was "Set cryptography free."

**DigiCash:** In 1990, Chaum founded DigiCash to commercialize his eCash technology. The company issued "CyberBucks" and licensed the technology to banks worldwide. Though DigiCash eventually failed, it proved the concept of digital currency.

**Current Work:** Chaum currently leads xx network, a quantum-secure decentralized messaging and payment platform.

**Legacy:** Chaum is widely recognized as the "father of digital cash" and a foundational figure in the cypherpunk movement that would later produce Bitcoin.

### Shafi Goldwasser (born 1959)

**Background and Education:** Shafi Goldwasser was born in 1959, growing up between Tel Aviv and the United States. She earned her undergraduate degree from Carnegie Mellon University, intending to study mathematics. She pursued graduate studies at UC Berkeley, where she studied under Turing Award winner Manuel Blum.

At Berkeley, she attended the first CRYPTO conference in Santa Barbara, where she met the future creators of RSA. She also met her future long-time collaborator, Silvio Micali.

**The 1982-1985 Breakthroughs:** Goldwasser and Micali co-authored landmark papers:

1. **"Probabilistic Encryption" (1982)**: Defined semantic security and established rigorous foundations for encryption
2. **Zero-Knowledge Proofs (1985)**: Introduced the revolutionary concept that one could prove a statement's validity without revealing any information beyond that validity

**Zero-Knowledge Proofs:** The concept seems paradoxical: how can you prove you know something without revealing what you know? Goldwasser and Micali showed it was possible through interactive protocols.

**Later Career:** Goldwasser joined MIT as a postdoc in 1983 and the faculty in 1983. In 1997, she became the first RSA Professor of Electrical Engineering and Computer Science. She leads the Cryptography and Information Security Group at CSAIL.

**Awards:**
- **ACM A.M. Turing Award (2012, with Silvio Micali)**
- IACR Fellow (2004)

### Silvio Micali (born 1954)

**Background and Education:** Silvio Micali was born in 1954 in Palermo, Sicily, Italy. He received his undergraduate degree in Mathematics from Sapienza University of Rome in 1978, graduating as one of the brightest students of Professor Corrado Böhm.

He earned his Ph.D. from UC Berkeley in 1982 under Manuel Blum. After a postdoc in Toronto, he joined MIT in 1983, where he has remained.

**Contributions:** Micali's work with Goldwasser established the rigorous mathematical foundations of modern cryptography. Their work on zero-knowledge proofs, probabilistic encryption, and interactive proofs transformed cryptography from an art to a science.

**Later Work:** Micali has continued to make fundamental contributions:
- **Verifiable Random Functions** (1999)
- **Algorand Blockchain** (2017): A proof-of-stake cryptocurrency

**Awards:** Micali shares the 2012 Turing Award with Goldwasser.

---

## <span style="color: seagreen;"> **Part IV: The Maturation Era (1990-1999)** </span>

### Robert J. McEliece (1942-2019)

**Background and Education:** Robert J. McEliece was born on May 21, 1942, in Washington, D.C. He earned his B.S. in Mathematics from Caltech in 1964 and his Ph.D. from Caltech in 1967 after graduate study at Cambridge University.

**Career:** McEliece joined NASA's Jet Propulsion Laboratory (JPL) in 1963, where he worked on error-correcting codes for deep space communications. He returned to Caltech as a faculty member in 1982, serving as executive officer of the Electrical Engineering department from 1990-1999.

**The 1978 Cryptosystem:** In 1978, McEliece published a public-key cryptosystem based on error-correcting codes. The **McEliece cryptosystem** uses Goppa codes and remains unbroken to this day. Its security rests on the difficulty of decoding a general linear code.

**Post-Quantum Relevance:** The McEliece cryptosystem has gained renewed interest as a post-quantum candidate because it is resistant to Shor's algorithm. "Classic McEliece" was a finalist in NIST's post-quantum competition.

**Legacy:** McEliece's work on error-correcting codes was crucial for NASA missions including Voyager, Galileo, Cassini, and Mars Exploration Rovers. He received the IEEE Claude E. Shannon Award in 2004.

### Charles H. Bennett (born 1943)

**Background and Education:** Charles Henry Bennett was born in 1943 in New York City to music teachers. He earned his B.A. in Chemistry from Brandeis University in 1964 and his Ph.D. from Harvard University in 1970, working on computer simulations of molecular motion.

**IBM Career:** Bennett joined IBM Research in Yorktown Heights in 1972, where he has spent his entire career. He was recruited by Rolf Landauer, a pioneer in the physics of information.

**The 1984 Breakthrough:** In 1984, Bennett and Gilles Brassard introduced **BB84**, the first practical quantum cryptography protocol. Named after their initials and the year, BB84 allows two parties to establish a secret key with security guaranteed by the laws of physics.

**The Story:** Bennett conceived of BB84 after learning about Stephen Wiesner's concept of "quantum money" from the early 1970s. At a 1979 conference in Puerto Rico, Bennett literally swam out to Brassard in the ocean to tell him about the idea.

**Quantum Teleportation:** In 1993, Bennett co-authored the landmark paper introducing **quantum teleportation**—the transfer of quantum states using entanglement and classical communication.

**Awards:**
- Wolf Prize in Physics (2018, with Brassard)
- Breakthrough Prize in Fundamental Physics (2023, with Brassard, Deutsch, and Shor)
- **ACM A.M. Turing Award (2025, with Brassard)**

### Gilles Brassard (born 1955)

**Background and Education:** Gilles Brassard was born on April 20, 1955, in Montreal, Quebec, Canada. He earned his B.S. (1972) and M.S. (1975) in Computer Science from the University of Montreal, followed by a Ph.D. in Theoretical Computer Science from Cornell University in 1979.

**Academic Career:** Brassard returned to the University of Montreal in 1979, becoming a full professor in 1988. He has held a Canada Research Chair in Quantum Information Science since 2001.

**Contributions:** Brassard's collaboration with Bennett produced:
1. **BB84 Quantum Key Distribution** (1984)
2. **Quantum Teleportation** (1993)
3. **Privacy Amplification**
4. **Entanglement Distillation**

**Awards:** Brassard shares the Wolf Prize, Breakthrough Prize, and Turing Award with Bennett.

### Peter W. Shor (born 1959)

**Background and Education:** Peter Williston Shor was born on August 14, 1959. He earned his B.S. in Mathematics from Caltech in 1981 and his Ph.D. in Applied Mathematics from MIT in 1985 under Tom Leighton.

**Career:** Shor joined Bell Labs in Murray Hill, New Jersey, after his Ph.D.

**The 1994 Breakthrough:** In 1994, Shor published "Algorithms for Quantum Computation," introducing **Shor's algorithm**—a quantum algorithm for integer factorization and discrete logarithms.

**Impact:** Shor's algorithm demonstrated that a sufficiently powerful quantum computer could break RSA and Diffie-Hellman cryptography in polynomial time. This was a watershed moment that:
1. Stimulated massive investment in quantum computing research
2. Created the field of post-quantum cryptography
3. Transformed quantum computing from theoretical curiosity to urgent practical concern

**Later Career:** Shor joined MIT in 2003, where he is the Morss Professor of Applied Mathematics.

**Awards:**
- Nevanlinna Prize (1998)
- Gödel Prize (1999)
- King Faisal International Prize (2002)
- IEEE Information Theory Society Paper Award
- Breakthrough Prize in Fundamental Physics (2023)

### Daniel J. Bernstein (born 1971)

**Background and Education:** Daniel Julius Bernstein ("djb") was born on October 29, 1971. He graduated from Bellport High School at age 15 in 1987, ranking 5th in the Westinghouse Science Talent Search. He earned his B.S. in Mathematics from NYU in 1991 and his Ph.D. from UC Berkeley in 1995 under Hendrik Lenstra.

**Bernstein v. United States (1995):** At age 24, Bernstein, with the EFF, sued the U.S. government over restrictions on cryptography exports. The ruling established that software source code is protected speech under the First Amendment, fundamentally changing cryptography regulation.

**Major Contributions:**
1. **Salsa20** (2005): A fast stream cipher
2. **ChaCha20** (2008): An improved stream cipher, now widely used in TLS
3. **Curve25519** (2005): A high-security elliptic curve for key exchange
4. **Ed25519** (2011): A high-security digital signature scheme
5. **SPHINCS+**: A hash-based post-quantum signature scheme (NIST selected)

**Current Position:** Bernstein is a Personal Professor at Eindhoven University of Technology and Research Professor at the University of Illinois at Chicago.

---

## <span style="color: seagreen;"> **Part V: The Modern Era (2000-Present)** </span>

### Dan Boneh (born 1969)

**Background and Education:** Dan Boneh was born in Israel in 1969. He earned his B.A. in Computer Science from the Technion—Israel Institute of Technology, followed by his M.A. and Ph.D. in Computer Science from Princeton University in 1996 under Richard J. Lipton.

**Academic Career:** Boneh joined the Stanford faculty in 1997, where he heads the Applied Cryptography Group and co-directs the Computer Security Lab.

**The 2001 Breakthrough:** In 2001, Boneh and Matt Franklin introduced the first practical **Identity-Based Encryption (IBE)** scheme using bilinear pairings on elliptic curves. This was a revolutionary concept: a public key could be any string (like an email address), eliminating the need for certificates.

**Pairing-Based Cryptography:** Boneh's work established pairing-based cryptography as a major field. Applications include:
- Short signatures (BLS signatures)
- Attribute-based encryption
- Functional encryption

**Voltage Security:** In 2002, Boneh co-founded Voltage Security with his students. The company commercialized IBE and was acquired by HP in 2015.

**Awards:**
- Gödel Prize (2013, with Matt Franklin and Antoine Joux)
- ACM Prize in Computing (2014)
- National Academy of Engineering (2016)
- National Academy of Sciences (2023)

### Matt Franklin (born 1965)

**Background and Education:** Matt Franklin earned his Ph.D. in Computer Science from Columbia University. He is a professor at UC Davis.

**Contributions:** Franklin's collaboration with Boneh on identity-based encryption won the Gödel Prize. He has made significant contributions to secure multi-party computation and cryptographic protocols.

### Oded Regev (born 1972)

**Background and Education:** Oded Regev was born in 1972 in Israel. He earned his B.Sc. (1995), M.Sc. (1997), and Ph.D. (2001) from Tel Aviv University under Yossi Azar, completing his Ph.D. at age 21.

**Career:** Regev held positions at Tel Aviv University and CNRS/École Normale Supérieure in Paris before joining NYU's Courant Institute in 2012. He was appointed Silver Professor in 2022.

**The 2005 Breakthrough:** In 2005, Regev published "On Lattices, Learning with Errors, Random Linear Codes, and Cryptography," introducing the **Learning With Errors (LWE)** problem.

**LWE:** LWE establishes a connection between worst-case lattice problems and average-case cryptographic hardness. The problem: given samples of the form (aᵢ, bᵢ = ⟨aᵢ, s⟩ + eᵢ), where eᵢ is small noise, recover the secret s.

**Impact:** LWE has become the foundation of post-quantum cryptography. It enables:
- Public-key encryption
- Fully homomorphic encryption
- Attribute-based encryption
- All major NIST post-quantum candidates

**Awards:**
- Gödel Prize (2018)
- Simons Investigator Award (2019)
- RSA Conference Award for Excellence in Mathematics (2024, with Gentry)

### Craig Gentry (born 1973)

**Background and Education:** Craig Gentry was born in 1973. He showed exceptional mathematical talent from an early age—his mother recounts that before age three, he taught himself multiplication using Cheerios arranged in grids on his high chair tray.

Gentry earned his B.S. in Mathematics from Duke University in 1995, becoming a Putnam Fellow in 1993. In an unusual move, he then earned a J.D. from Harvard Law School in 1998 and practiced intellectual property law from 1998-2000.

Returning to mathematics, he worked at DoCoMo USA Labs (2000-2005) before pursuing his Ph.D. in Computer Science at Stanford under Dan Boneh, completing it in 2009.

**The 2009 Breakthrough:** Gentry's Ph.D. thesis introduced the first **Fully Homomorphic Encryption (FHE)** scheme. FHE allows arbitrary computations on encrypted data without decryption—a "holy grail" of cryptography that had been sought since the 1970s.

**Bootstrapping:** Gentry's key innovation was "bootstrapping"—homomorphically evaluating the decryption circuit to refresh ciphertext noise, enabling unlimited computation depth.

**Later Career:** Gentry joined IBM Research (2009-2019), then the Algorand Foundation (2019-2022), TripleBlind as CTO (2022-2024), and since 2024 has been Chief Scientist at Cornami.

**Awards:**
- ACM Doctoral Dissertation Award (2009)
- ACM Grace Murray Hopper Award (2010)
- MacArthur Fellowship ("Genius Grant") (2014)
- Gödel Prize (2022, with Brakerski and Vaikuntanathan)
- RSA Conference Award for Excellence in Mathematics (2024, with Regev)

### Mihir Bellare (born 1962)

**Background and Education:** Mihir Bellare earned his B.S. in Mathematics from Caltech in 1986 and his Ph.D. from MIT in 1991 under Silvio Micali.

**Career:** Bellare worked at IBM Research (1991-1995) before joining UC San Diego in 1995, where he runs the Cryptography Group.

**Contributions:** Bellare and Phillip Rogaway pioneered **practice-oriented provable security**—a methodology for creating practical cryptographic schemes with rigorous security proofs.

**Major Designs:**
- **HMAC** (1996): The standard for message authentication
- **OAEP** (1994): Optimal Asymmetric Encryption Padding for RSA
- **RSA-PSS** (1996): Probabilistic Signature Scheme

**Awards:**
- ACM Paris Kanellakis Theory and Practice Award (2009, with Rogaway)
- RSA Conference Award in Mathematics (2003)
- Levchin Prize for Real-World Cryptography (2019)

### Phillip Rogaway (born 1960)

**Background and Education:** Phillip Rogaway earned his undergraduate degree from UC Berkeley and his Ph.D. from MIT in 1991 under Silvio Micali.

**Career:** Rogaway worked at IBM as a Security Architect (1991-1994) before joining UC Davis, where he remained until retiring in 2024.

**Contributions:** Rogaway, with Bellare, established practice-oriented provable security. He designed:
- **OCB Mode** (2001): Efficient authenticated encryption
- **UMAC** (1999): Fast message authentication
- **EAX Mode**: Authenticated encryption

**Awards:**
- ACM Paris Kanellakis Theory and Practice Award (2009, with Bellare)
- Levchin Prize for Real-World Cryptography (2016)
- IACR Fellow (2012)

### Jean-Philippe Aumasson (born 1979)

**Background and Education:** Jean-Philippe Aumasson was born in 1979 in Paris, France. He earned his Ph.D. in Cryptography from EPFL (Switzerland) in 2009.

**Contributions:** Aumasson is a leading designer of cryptographic hash functions:
- **BLAKE** (2008): SHA-3 finalist
- **BLAKE2** (2012): Faster successor, used in WinRAR, Pcompress
- **BLAKE3** (2020): Parallelizable hash function
- **SipHash** (2012): Fast hash for hash tables, used in Perl, Ruby, OpenDNS

**Current Position:** Aumasson is co-founder and Chief Security Officer at Taurus, a Swiss crypto asset management technology company.

---

## <span style="color: seagreen;"> **Part VI: Post-Quantum Cryptography Standardization (2016-2024)** </span>

### The NIST Competition

In 2016, NIST launched the Post-Quantum Cryptography Standardization Process to select quantum-resistant algorithms. The competition ran for eight years, with 82 initial submissions from 25 countries.

### CRYSTALS-Kyber (ML-KEM) Team

**Principal Authors:**
- Peter Schwabe (Max Planck Institute, Radboud University)
- Roberto Avanzi
- Joppe Bos
- Léo Ducas
- Eike Kiltz
- Tancrède Lepoint
- Vadim Lyubashevsky
- John M. Schanck
- Gregor Seiler
- Damien Stehlé

**Background:** Peter Schwabe is a leading researcher in implementation of post-quantum cryptography. The CRYSTALS-Kyber team brought together experts from academia and industry across multiple countries.

**The Algorithm:** Kyber is a lattice-based Key Encapsulation Mechanism (KEM) based on the hardness of the Module-LWE problem. It offers excellent performance and relatively small key sizes.

**Standardization:** Kyber was selected as the primary encryption standard (FIPS 203) in 2024.

### CRYSTALS-Dilithium (ML-DSA) Team

**Principal Authors:** Same core team as Kyber

**The Algorithm:** Dilithium is a lattice-based digital signature scheme based on the hardness of the Module-LWE and Module-SIS problems.

**Standardization:** Dilithium was selected as the primary signature standard (FIPS 204) in 2024.

### FALCON (FN-DSA) Team

**Designers:**
- Thomas Prest
- Pierre-Alain Fouque
- Jeffrey Hoffstein
- Paul Kirchner
- Vadim Lyubashevsky
- Thomas Pornin
- Thomas Ricosset
- Gregor Seiler
- William Whyte
- Zhenfei Zhang

**The Algorithm:** FALCON is a lattice-based signature scheme using NTRU lattices with fast Fourier sampling. It offers the smallest signature sizes among NIST selections.

**Standardization:** FALCON is expected to be standardized as FIPS 206 in late 2024.

### SPHINCS+ (SLH-DSA) Team

**Team Leader:** Andreas Hülsing (Eindhoven University of Technology)

**The Algorithm:** SPHINCS+ is a stateless hash-based signature scheme. It provides a conservative security guarantee based purely on hash function properties, with no number-theoretic assumptions.

**Standardization:** SPHINCS+ was selected as a backup signature standard (FIPS 205) in 2024.

---

## <span style="color: seagreen;"> **Summary: The People and Their Legacies** </span>

### The Pioneers (1969-1978)

| Person | Contribution | Background | Key Insight |
|--------|--------------|------------|-------------|
| James Ellis | Concept of non-secret encryption | GCHQ physicist | Two parties can communicate securely without prior key exchange |
| Clifford Cocks | RSA cryptosystem (1973) | Cambridge mathematician | Prime factorization provides one-way function |
| Malcolm Williamson | Diffie-Hellman key exchange (1974) | Cambridge mathematician | Modular exponentiation enables secure key agreement |
| Whitfield Diffie | Public-key cryptography concept (1976) | MIT mathematician | Digital signatures and key exchange are possible |
| Martin Hellman | Diffie-Hellman key exchange (1976) | Stanford engineer | Practical implementation of public-key distribution |
| Ralph Merkle | Merkle's Puzzles, Merkle Trees | UC Berkeley computer scientist | Public-key distribution is possible; hash trees enable verification |
| Ron Rivest | RSA cryptosystem (1977) | MIT computer scientist | Factorization enables practical public-key encryption |
| Adi Shamir | RSA cryptosystem (1977) | Weizmann mathematician | Mathematical rigor for RSA security |
| Leonard Adleman | RSA cryptosystem (1977) | Berkeley mathematician | Verification of RSA security |

### The Expanders (1980-1989)

| Person | Contribution | Background | Key Insight |
|--------|--------------|------------|-------------|
| Taher Elgamal | ElGamal encryption/signatures | Stanford EE, Egyptian immigrant | Discrete logarithms enable encryption and signatures |
| Neal Koblitz | Elliptic Curve Cryptography | Princeton mathematician | Elliptic curves offer efficiency advantages |
| Victor Miller | Elliptic Curve Cryptography | Harvard mathematician, IBM | ECC is practical with efficient algorithms |
| David Chaum | Digital cash, blind signatures | Berkeley computer scientist | Cryptography enables anonymous digital payments |
| Shafi Goldwasser | Zero-knowledge proofs, semantic security | Berkeley PhD, MIT professor | Proofs can reveal nothing but validity |
| Silvio Micali | Zero-knowledge proofs | Berkeley PhD, MIT professor | Cryptography can have rigorous foundations |

### The Modern Era (1990-Present)

| Person | Contribution | Background | Key Insight |
|--------|--------------|------------|-------------|
| Robert McEliece | Code-based cryptography | Caltech mathematician, NASA JPL | Error-correcting codes enable post-quantum security |
| Charles Bennett | Quantum cryptography | Harvard physicist, IBM | Physics guarantees security, not just math |
| Gilles Brassard | Quantum cryptography | Cornell CS, Montreal professor | BB84 enables quantum key distribution |
| Peter Shor | Quantum algorithms | MIT applied mathematician | Quantum computers break current cryptography |
| Dan Boneh | Pairing-based cryptography, IBE | Princeton PhD, Stanford professor | Bilinear pairings enable new cryptographic capabilities |
| Oded Regev | Learning With Errors | Tel Aviv PhD, NYU professor | LWE connects worst-case and average-case hardness |
| Craig Gentry | Fully homomorphic encryption | Stanford PhD, IBM/Algorand | Arbitrary computation on encrypted data is possible |
| Mihir Bellare | Practice-oriented provable security | MIT PhD, UCSD professor | Practical cryptography can have rigorous proofs |
| Phillip Rogaway | Practice-oriented provable security | MIT PhD, UC Davis professor | Efficient authenticated encryption is achievable |
| Daniel Bernstein | Curve25519, ChaCha20, SPHINCS+ | Berkeley PhD, UIC professor | Cryptography can be both fast and secure |

---

## Final Words

The history of public key cryptography is a testament to human ingenuity and the power of mathematical thinking. From James Ellis's classified conceptual breakthrough at GCHQ to the post-quantum standards being deployed today, this field has been shaped by remarkable individuals from diverse backgrounds.

What unites these pioneers is not just mathematical talent, but a willingness to question fundamental assumptions about what is possible. Ellis asked whether secure communication required prior key exchange. Diffie and Hellman asked whether digital signatures were possible. Gentry asked whether arbitrary computation on encrypted data could be done.

The field continues to evolve. Quantum computing threatens current systems, but lattice-based cryptography offers a path forward. Fully homomorphic encryption promises to transform cloud computing. Zero-knowledge proofs are enabling new privacy-preserving applications.

The people profiled in this survey have fundamentally changed how humanity secures its digital communications. Their work protects billions of online transactions, secures government communications, and enables the digital economy. It is a legacy that will endure for generations.

---

## References and Further Reading

1. Diffie, W., & Hellman, M. (1976). New directions in cryptography. *IEEE Transactions on Information Theory*, 22(6), 644-654.

2. Rivest, R. L., Shamir, A., & Adleman, L. (1978). A method for obtaining digital signatures and public-key cryptosystems. *Communications of the ACM*, 21(2), 120-126.

3. Koblitz, N. (1987). Elliptic curve cryptosystems. *Mathematics of Computation*, 48(177), 203-209.

4. Miller, V. S. (1986). Use of elliptic curves in cryptography. In *Advances in Cryptology—CRYPTO '85 Proceedings* (pp. 417-426).

5. Elgamal, T. (1985). A public key cryptosystem and a signature scheme based on discrete logarithms. *IEEE Transactions on Information Theory*, 31(4), 469-472.

6. Goldwasser, S., & Micali, S. (1982). Probabilistic encryption & how to play mental poker keeping secret all partial information. In *Proceedings of the 14th Annual ACM Symposium on Theory of Computing* (pp. 365-377).

7. Goldwasser, S., Micali, S., & Rackoff, C. (1989). The knowledge complexity of interactive proof systems. *SIAM Journal on Computing*, 18(1), 186-208.

8. Shor, P. W. (1994). Algorithms for quantum computation: discrete logarithms and factoring. In *Proceedings 35th Annual Symposium on Foundations of Computer Science* (pp. 124-134).

9. Boneh, D., & Franklin, M. (2001). Identity-based encryption from the Weil pairing. In *Advances in Cryptology—CRYPTO 2001* (pp. 213-229).

10. Regev, O. (2005). On lattices, learning with errors, random linear codes, and cryptography. In *Proceedings of the 37th Annual ACM Symposium on Theory of Computing* (pp. 84-93).

11. Gentry, C. (2009). A fully homomorphic encryption scheme. *Stanford University Ph.D. Dissertation*.

12. Bennett, C. H., & Brassard, G. (1984). Quantum cryptography: Public key distribution and coin tossing. In *Proceedings of IEEE International Conference on Computers, Systems and Signal Processing* (pp. 175-179).

---

*This article was compiled to provide a comprehensive, person-centered history of public key cryptography. The field continues to evolve, with new discoveries and new researchers building on these foundational contributions.*
