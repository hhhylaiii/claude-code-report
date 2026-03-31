# Thesis directions in unclonable encryption: five research frontiers

Unclonable encryption—leveraging quantum no-cloning to produce ciphertexts that cannot be duplicated for two independent decryptors—has evolved from a niche theoretical curiosity into one of quantum cryptography's most active subfields. **All five directions the professor identified contain genuine open problems suitable for thesis research**, though they vary in maturity. The fake-key property from Ananth-Kaleoglu (TCC 2021) connects deeply to classical notions of deniable and non-committing encryption, and these connections remain largely unformalized. Below is a detailed analysis of each direction with specific open questions, key references, and feasibility assessments.

---

## Direction 1: No public-key fake-key property has been formally defined

The fake-key property (Definition 16 in Ananth-Kaleoglu) states that given a ciphertext ct = Enc(k, m₀), an efficient algorithm FakeGen can produce a key k′ such that Dec(k′, ct) = m₁ for any chosen m₁, with (ct, k′) computationally indistinguishable from a real encryption pair. **No paper from 2021–2026 defines a standalone public-key analog of this property.** The concept exists only implicitly.

Ananth-Kaleoglu themselves achieve public-key unclonable encryption by embedding fake-key functionality into functional encryption: a "fake decryption key" is realized as a functional key sk_{f_{m′}} for the constant function f_{m′}(·) = m′. They explicitly note this is "a special case of a primitive called somewhere equivocal encryption [Hemenway-Jafargholi-Ostrovsky-Sahai-Wichs, 2015]." This FE-based approach remains the only technique in the unclonable encryption literature for achieving public-key equivocability.

The closest existing public-key concepts and why they fall short:

- **Receiver-deniable PKE** is conceptually identical—the receiver produces a fake secret key making a real ciphertext decrypt to a chosen message. However, Bendlin et al. (ASIACRYPT 2011) proved that non-interactive receiver-deniable PKE with negligible detection probability **cannot have polynomial-size keys**, making it effectively impossible in the standard non-interactive model.
- **Non-committing encryption** (Canetti-Feige-Goldreich-Naor, STOC 1996) allows a simulator to produce fake (pk, sk, randomness) explaining a ciphertext as any message—but requires the ciphertext itself to be simulated, not honestly generated. This is a critical distinction from fake-key, which operates on real ciphertexts.
- **Lossy encryption** (Peikert-Waters, STOC 2008) and **dual-mode encryption** (Peikert-Vaikuntanathan-Waters) only destroy message information in lossy mode; neither produces keys that decrypt to a *chosen* message. They are insufficient substitutes.

**Thesis opportunity**: Formally define a public-key fake-key property, prove whether it can be achieved (likely requiring interaction or quantum techniques to circumvent the Bendlin et al. impossibility), and study its relationship to receiver deniability and NCE. The quantum setting may offer an escape from the classical impossibility.

---

## Direction 2: The unclonable encryption landscape from 2020 to 2026

The field has progressed through four distinct phases, each expanding what is achievable:

**Phase 1 — Foundations (2020–2021).** Broadbent and Lord (TQC 2020) formally defined unclonable encryption using BB84 states in the quantum random oracle model, achieving search (weak) security. Ananth and Kaleoglu (TCC 2021) extended this to reusable private-key and public-key constructions, introduced the fake-key property, and proved unclonable-indistinguishability implies copy-protection for point functions. Coladangelo, Liu, Liu, and Zhandry (CRYPTO 2021) introduced hidden coset states and constructed single-decryptor encryption from iO in the plain model. Majenz, Schaffner, and Tahmasbi (2021) proved information-theoretic limitations, showing explicit cloning attacks with success probability approaching **0.71^n** for conjugate encryption.

**Phase 2 — Strong security in QROM (2022–2023).** Ananth, Kaleoglu, Li, Liu, and Zhandry (CRYPTO 2022) achieved the first unclonable encryption with **indistinguishability security** (the strong notion) unconditionally in the QROM using coset states. Ananth, Kaleoglu, and Liu (CRYPTO 2023) unified the field through the "cloning games" framework, simplifying constructions to use BB84 states instead of coset states. Kitagawa and Nishimaki (TCC 2023) introduced "one-out-of-many" unclonable security, achieving the first single-decryptor encryption from LWE without iO or oracles.

**Phase 3 — Plain model and unconditional results (2024–2025).** Ananth, Kaleoglu, and Yuen (ITCS 2025) achieved the **first plain-model unclonable encryption with indistinguishability security**, using Haar random quantum states as decryption keys and proving "simultaneous Haar indistinguishability." Ananth and Behera (CRYPTO 2024) introduced unclonable puncturable obfuscation as a modular framework. Bhattacharyya and Culf (Nature Physics, 2025) proved the existence of UE with **zero computational assumptions**—a landmark unconditional result using decoupling arguments.

**Phase 4 — Multi-copy security and extensions (2025–2026).** Çakan, Goyal, Kitagawa, Nishimaki, and Yamakawa (2025) constructed the first multi-copy secure unclonable encryption via a generic compiler from collusion-resistant primitives. Kitagawa and Yamakawa (TCC 2025) systematized single-decryptor encryption foundations. Champion, Kitagawa, Nishimaki, and Yamakawa (TCC 2025) introduced untelegraphable encryption as a relaxation based on the no-telegraphing principle.

**Key open problems remaining**: achieving standard-model UE with *classical* decryption keys and indistinguishability security (without QROM); optimal multi-copy security bounds; practical implementations; and formal connections to simulation-based security frameworks.

---

## Direction 3: The unexplored triangle of fake-key, NCE, and quantum deniability

This direction contains what may be the richest thesis opportunity. Three concepts—the fake-key property, non-committing encryption, and deniable encryption—all capture the same fundamental idea of *equivocability* (retroactively explaining a ciphertext as encrypting a different message), yet **no paper explicitly draws the connection among all three in the unclonable encryption context**.

**Quantum deniable encryption exists but follows a different path.** Coladangelo, Goldwasser, and Vazirani (STOC 2022) constructed sender-deniable encryption where the encryption algorithm is quantum but ciphertexts are classical. Their key contribution is **"perfect unexplainability"**—a property strictly stronger than classical deniability where even an honest sender cannot prove what they encrypted. This is impossible classically and relies on quantum computation's irreversibility. The construction uses quantum-hard LWE in the random oracle model. Notably, the paper's original claim of "ℓ-deniability" was found insecure and retracted in a later version; the unexplainability results stand.

**NCE has not been studied in the quantum or unclonable setting.** No paper defines or constructs "quantum NCE" or applies NCE techniques to unclonable primitives. The closest quantum analog is the **extractable and equivocal quantum bit commitments** from Bartusek, Coladangelo, Khurana, and Ma (CRYPTO 2021), which enable simulation-secure quantum oblivious transfer from one-way functions. These equivocal commitments play the same structural role in quantum secure computation that NCE plays in classical adaptive MPC.

**The conceptual map connecting these notions** is clear but unformalised:

The fake-key property equivocates *the decryption key* on a *real* ciphertext. NCE equivocates *both key and randomness* on a *simulated* ciphertext. Receiver-deniable encryption equivocates *the secret key* on a *real* ciphertext. All three serve the same purpose in security proofs: enabling a simulator or reduction to "explain away" ciphertext contents. The fake-key property is essentially a restricted form of receiver deniability, and both are special cases of the equivocability that NCE provides.

**Classical NCE references the student should study**: Canetti-Feige-Goldreich-Naor (STOC 1996) for the original definition; Damgård-Nielsen (CRYPTO 2000) for simulatable PKE as a building block; Nielsen (CRYPTO 2002) for impossibility of non-interactive NCE in the non-programmable random oracle model; and Canetti-Poburinnaya-Raykova (ASIACRYPT 2017) for optimal-rate NCE.

**Thesis opportunities**: (1) Define "quantum NCE" and determine whether quantum resources circumvent Nielsen's impossibility for non-interactive NCE. (2) Formalize the fake-key ↔ NCE ↔ deniable encryption triangle and prove implications or separations. (3) Determine whether quantum deniable encryption techniques (CGV22) can strengthen unclonable encryption constructions. (4) Study UC security for unclonable encryption using quantum equivocal techniques.

---

## Direction 4: Unclonable functional encryption emerged in 2024

The primary paper is **"Unclonable Functional Encryption"** by Arthur Mehta and Anne Müller (arXiv:2410.06029, ePrint 2024/1683, October 2024). This preprint has not yet appeared at a major conference as of March 2026.

Mehta and Müller define **quantum functional encryption (QFE)**—a scheme allowing evaluation of polynomial-sized circuits on quantum messages—and prove that any QFE universally achieves **unclonable functional encryption (UFE)**. Their construction uses quantum garbled circuits (from Barrington-Yuen 2022) for the base QFE scheme, then combines it with unclonable encryption with quantum decryption keys from Ananth-Kaleoglu-Yuen (ITCS 2025). The UFE guarantee ensures two parties cannot simultaneously recover correct function outputs using independently sampled function secret keys. As an application, they give the **first public-key UE with variable decryption keys**.

Critically, Mehta-Müller **does not use the fake-key property**. Their technical path runs through quantum garbled circuits and simultaneous Haar indistinguishability rather than equivocal/simulation techniques. They also prove that multi-input indistinguishability-secure QFE unconditionally implies quantum indistinguishability obfuscation (qiO).

Several related lines of work address unclonable keys for functional encryption from different angles. Kitagawa and Nishimaki (ASIACRYPT 2022) defined **functional encryption with secure key leasing**—a weaker property where returned keys lose functionality—and achieved it from standard SKFE without additional assumptions. Çakan and Goyal (TCC 2024) constructed the first **unbounded collusion-resistant copy-protection for public-key FE** from sub-exponential iO and LWE. Champion, Kitagawa, Nishimaki, and Yamakawa (TCC 2025) defined **untelegraphable functional encryption**, achieving both secret-key and public-key variants as a relaxation of full unclonability. Kitagawa and Nishimaki (TCC 2023) achieved **one-out-of-many unclonable predicate encryption** from LWE.

**Thesis opportunities**: (1) Determine whether fake-key techniques provide an alternative path to UFE with potentially weaker assumptions. (2) Achieve UFE with classical decryption keys. (3) Study the relationship between UFE and unbounded collusion-resistant FE with copy-protected keys.

---

## Direction 5: The one-to-many fake-key generalization is open and promising

The professor's question—whether the fake-key property can be extended to produce *multiple* fake keys from a single ciphertext, each decrypting to a different message—identifies a **genuinely open problem** that no paper has explicitly studied.

**Why it matters**: The current fake-key property supports 1-to-2 cloning security proofs. For m-to-(m+1) security, the reduction would need to produce m+1 fake keys from the same ciphertext, each embedding a different message for a different simulated adversary. This "one-to-many fake-key property" would require the joint distribution (ct, fk₁, fk₂, ..., fk_t) to be indistinguishable from the real setting—substantially stronger than individual indistinguishability.

**The private-key case appears trivially satisfiable.** In Ananth-Kaleoglu's construction, FakeGen samples an independent random key k′ᵢ and sets otp′ᵢ = θ ⊕ PRF_{k′ᵢ}(r) ⊕ mᵢ. Multiple invocations produce independent fake keys since each k′ᵢ is independently random. Joint indistinguishability likely follows from PRF security under a standard hybrid argument. The **public-key case via functional encryption** is more delicate, potentially requiring multi-query simulation guarantees from the underlying FE scheme.

**Multi-copy security has been achieved through entirely different techniques.** Çakan, Goyal, Kitagawa, Nishimaki, and Yamakawa (2025) constructed the first unbounded multi-copy secure UE via a generic compiler that upgrades collusion-resistant primitives using one-way functions. Their approach explicitly avoids the fake-key path: they connect multi-challenge UE to collusion-resistant single-decryptor encryption (swapping the roles of keys and ciphertexts), sidestepping the hybrid argument difficulties in the UE setting. Ananth, Mutreja, and Poremba (2024) achieved multi-copy revocable encryption in oracle models but showed that BB84 states, subspace coset states, and Gaussian states are all **learnable given many copies**, ruling them out as bases for multi-copy secure schemes.

**The classical analog (NCE) supports multiple equivocations.** In NCE, a simulator can produce a ciphertext that is later "opened" to arbitrarily many different messages. The equivocality parameter in "Somewhat NCE" (Garay-Wichs-Zhou, CRYPTO 2009) explicitly measures the number of equivocations possible. This suggests the quantum one-to-many version should be feasible, at least in principle.

**Thesis opportunities**: (1) Formally define the one-to-many fake-key property with joint indistinguishability. (2) Prove the private-key case holds trivially and identify the exact conditions needed for the public-key case. (3) Determine whether a one-to-many fake-key property yields a more direct or assumption-efficient proof of multi-copy UE security than the existing compiler approach. (4) Connect the one-to-many fake-key property to classical NCE equivocability, potentially yielding new insight into both fields.

---

## Conclusion: a map of open questions for the thesis

The five directions form a coherent research program. The **deepest unexplored territory** lies at the intersection of Directions 1, 3, and 5: formalizing the fake-key/NCE/deniable-encryption triangle, defining quantum NCE, and extending the fake-key property to the public-key and one-to-many settings. No paper has unified these classical concepts with unclonable encryption techniques—this represents a genuine gap in the literature.

Direction 4 (unclonable FE) is the most technically mature, with Mehta-Müller's 2024 construction and multiple related works, but open problems remain around achieving UFE from weaker assumptions or with classical keys. Direction 2 reveals that the field has recently achieved two watershed results—unconditional UE (Bhattacharyya-Culf, 2025) and multi-copy security (Çakan et al., 2025)—leaving **standard-model UE with classical keys and indistinguishability security** as the central remaining frontier.

A thesis combining the formalization of public-key and one-to-many fake-key properties (Directions 1 and 5) with the NCE/deniability connection (Direction 3) would address multiple open questions simultaneously and position the student at a productive intersection of classical and quantum cryptographic theory.