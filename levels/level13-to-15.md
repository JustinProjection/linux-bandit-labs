# OverTheWire Bandit: Level 13 → Level 14

## 🚩 Objective
Retrieve the password for `bandit14` stored in `/etc/bandit_pass/bandit14`. Instead of a standard password, authentication requires using a provided SSH private key (`sshkey.private`).

## 🔑 Key Concepts Covered
* Public Key Authentication (`ssh -i`)
* Linux File Ownership & Permissions (`chmod`)
* Understanding SSH Security Rules (Key File Protection)
* Workarounds for File Ownership Constraints

---

## 🛠️ Step-by-Step Solution & Methodology

### 1. Inspection & Identifying the Problem
Upon logging into `bandit13`, inspecting the home directory revealed two files: `HINT` and `sshkey.private`. Checking their detailed permissions with `ls -la`:

```bash
ls -la
