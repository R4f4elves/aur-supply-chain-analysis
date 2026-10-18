# Arch Linux AUR Supply Chain Vulnerability Analysis

## 📌 Overview
This repository contains a technical research presentation analyzing a supply chain attack within the **Arch Linux User Repository (AUR)**. The project investigates how threat actors exploited the community-driven repository by hijacking orphaned packages to distribute malware via fake updates and code injection.

## 🚨 The Attack Vector & Code Analysis
The attack leverages the blind compilation of `PKGBUILD` scripts using the `makepkg` command. 
By inspecting the malicious `PKGBUILD`:
* **Attack Vector:** The `source` variable is altered to download malicious payloads.
* **Malicious Execution:** The `package()` function is hijacked to execute unauthorized bash commands during installation.

## 💥 Consequences
If executed, the compromised packages lead to severe system impacts:
* Credential and security key theft.
* Cryptojacking (hardware hijacking for crypto mining).
* Full Root access for the attacker.
* System lockdown to contain the damage.

## 🛡️ Proposed Solutions & Mitigation
The research outlines practical problem-solving strategies divided into two fronts:

**User-Side Solutions:**
* **The Golden Rule:** Mandatory reading of the `PKGBUILD` file before any installation.
* Source verification and command analysis within the `package` function.
* The end of "blind compilation": Never execute `makepkg` automatically without prior review.

**System-Side Solutions (Arch Policy):**
* Permanent freezing policy for abandoned packages.
* Inactivity rules (freezing after 18-24 months) with a depreciation countdown timer.
* Mandatory "Fork" (new name) for continuity.
