# NETWOKRWALKS-B083-WK3-PMI-CYBERSECURITY
Cybersecurity Lab Environment Setup Building an isolated virtual lab for penetration testing and ethical hacking practice.
# 🔐 Password Cracking with John the Ripper — Cybersecurity Skills Report

**Course:** Networkwalks Academy — Cybersecurity & Ethical Hacking with AI (Week 3)
**Focus tool:** John the Ripper (JtR) — via the Johnny GUI front-end
**Target:** Password-protected PDF files
**Date completed:** September 2026

---

## 📌 Overview

This exercise walked through the full workflow a security tester follows when auditing
a password-protected document: extracting a crackable hash from the file, running a
wordlist attack against that hash, recovering the plaintext password, and using it to
unlock the original file. Three separate locked PDFs were used as practice targets,
each rewarding a capture-the-flag (CTF) style flag on successful recovery.

## 🎯 Skills Learned

- Extracting `pdf2john` / `hashcat`-compatible hashes from encrypted PDF files
- Reading and interpreting the `$pdf$` hash format (revision, key length, permissions, salts)
- Configuring **John the Ripper** (via the **Johnny** GUI) to point at a JtR executable and run an attack
- Running dictionary/wordlist-based password attacks against extracted hashes
- Using web-based auditing utilities (hash extractors and password crackers) to cross-check results
- Verifying a cracked password by using it to decrypt and open the original protected PDF
- General password-auditing mindset: patience, wordlist selection, and hash-format awareness

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| **John the Ripper (JtR)** | Core password-cracking engine used to brute-force/dictionary-attack the PDF hashes |
| **Johnny** | Graphical front-end for John the Ripper, used to configure and monitor cracking sessions |
| `pdf2john` (via onlinehashcrack.com PDF Hash Extractor) | Converts an encrypted PDF into a JtR/hashcat-crackable hash |
| networkwalks.com **Hash Calculator** | Alternate in-browser tool for extracting a PDF's crackable hash |
| networkwalks.com **Password Cracker** | In-browser wordlist attack demo against the extracted hash |

## 🧪 Hashes Extracted

Each target PDF was converted into a `$pdf$` (pdf2john) formatted hash before any
cracking attempt. Sample extracted hashes are included in [`/hashes`](./hashes):

```text
# hash1_pdf.txt
$pdf$4*4*128*-1028*1*16*ca7f72f11459cba469f1005a8765ed51*32*f32d8fa1bfbe2648226dffc39f7909ea0021446990b9e4114071a4d9104984c1*32*9322f50c29569712067a775264635e4954ccb1b99e209d664984054ffad30a6a

# hash2_pdf.txt
$pdf$4*4*128*-1028*1*16*0853f2cde0ef15b1c0f93ed229d3b1ad*32*8f13ce5aa39ad974364d36a057da76790021446990b9e4114071a4d9104984c1*32*ceecdac74b19b5a62688d3b3524e1374c955cbb9cc3c45316494d9446ef81af1

# hash3_pdf.txt
$pdf$4*4*128*-1028*1*16*34eb542eff4e1b0b32d25ce15a9a7281*32*b77872bfc9a24fb2f845066283a8fc1b0021446990b9e4114071a4d9104984c1*32*e7572256e4b552cd57988f5134214b91920d94d7a6bf550ea94a2995c7f2ab02
```

## 🪜 Walkthrough

### 1. Extract a crackable hash from the encrypted PDF
Used an online `pdf2john` utility to convert the encrypted PDF into a hash format that
John the Ripper / hashcat can process.

05-pdf1-unlocked-congrats.png
![PDF hash extractor output](./screenshots/06-pdf-hash-extractor-output.png)

### 2. Extract the hash for a second target PDF
Repeated the extraction using networkwalks.com's own Hash Calculator tool for a second
locked PDF, confirming the same `$pdf$` hash structure.

![Networkwalks hash calculator extracting PDF2 hash](./screenshots/04-hash-calculator-pdf2-extraction.png)

### 3. Run a dictionary attack against the extracted hash
Fed the extracted hash into a wordlist/dictionary attack. The attack iterated through
common password candidates until a match was found.

![Password cracker wordlist attack finds a match](./screenshots/03-password-cracker-wordlist-match.png)

### 4. Unlock the PDF with the recovered password
Used the cracked password to open the originally locked PDF, confirming the recovered
credential was correct and capturing the flag.

![PDF unlocked, flag captured](./screenshots/02-pdf2-unlocked-flag.png)

### 5. Configure John the Ripper via the Johnny GUI
Set up **Johnny** (the JtR graphical interface) by pointing it at the John the Ripper
Jumbo executable, ready to load a password/hash file and start a real cracking session.

![Johnny GUI configured with John the Ripper executable](./screenshots/08-johnny-jtr-gui-setup.png)

### 6. Crack and unlock the second PDF with JtR
Ran John the Ripper against a target hash and used the recovered password to decrypt
the corresponding PDF.

![Second PDF unlocked with JtR-recovered password](./screenshots/05-pdf1-unlocked-congrats.png)

### 7. Final flag — persistence pays off
The final exercise emphasized persistence and wordlist selection as key skills for a
real security tester — captured on successfully cracking the last target with JtR.

![Final flag captured via JtR](./screenshots/01-jtr-persistence-flag.png)

## 🏁 Flags Captured

- `nw{networkwalks_flag_260821_1}`
- `nw{networkwalks_persistence_jtr_270521}`

## 🗒️ Notes & Takeaways

- The `$pdf$` hash format encodes the PDF revision, encryption key length, permission
  flags, and the salted owner/user password hashes — understanding this structure makes
  it much easier to pick the right JtR/hashcat mode for an attack.
- Web-based extractor/cracker demos are useful for quickly validating a hash or password
  guess, but **John the Ripper run locally (via Johnny)** is the tool that scales to real
  wordlists, rules, and mask attacks.
- Cracking speed is entirely dependent on wordlist quality — this is the biggest lever
  for a security tester auditing password strength.

---

*This report documents a personal cybersecurity training exercise completed on
[Networkwalks Academy](https://networkwalks.com) for portfolio and learning-log purposes.
All target files were provided by the course for practice and contain no real
personal or sensitive data.*
