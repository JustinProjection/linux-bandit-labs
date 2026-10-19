# 🚩 Bandit Level 13 → Level 15

### **Objective**

Retrieve the password for `bandit14` stored in `/etc/bandit_pass/bandit14`. For this level, password-based authentication is not used; instead, an SSH private key (`sshkey.private`) is provided to log in directly as `bandit14`.

---

### **Key Concepts Covered**

* **Public Key Authentication (`ssh -i`)**
* **Linux File Ownership & Permissions (`chmod`)**
* **Understanding SSH Security Rules (Key File Protection)**
* **Workarounds for File Ownership Constraints**

---

### **Step-by-Step Solution & Methodology**

#### **1. Inspection & Identifying the Problem**

Upon logging into `bandit13`, inspecting the home directory revealed two files: `HINT` and `sshkey.private`. Checking their detailed permissions with `ls -la`:

```bash
ls -la

```

*Output:*

```text
-rw-r-----  1 bandit14 bandit13  2602 Sep 26 21:54 sshkey.private

```

* **Observation:** The key file was owned by `bandit14`, but readable by the `bandit13` group.
* **Challenge:** Attempting to modify its permissions directly on `bandit13` resulted in `chmod: Operation not permitted` because `bandit13` does not own the file.

---

#### **2. Extracting and Recreating the Private Key**

Because SSH requires strict permissions on private key files to operate (and `bandit13` could not alter the original file's mode), the raw key content was extracted:

```bash
cat sshkey.private

```

The key string (`-----BEGIN OPENSSH PRIVATE KEY-----` to `-----END OPENSSH PRIVATE KEY-----`) was copied and created in a session where file ownership belonged to the operator:

```bash
nano sshkey.private

```

---

#### **3. Restricting Key Permissions (`chmod 600`)**

OpenSSH rejects private keys if they are accessible by other group members or system users (`WARNING: UNPROTECTED PRIVATE KEY FILE!`).

To make the key acceptable to `ssh`, permissions were set so only the file owner has read and write access:

```bash
chmod 600 sshkey.private

```

* **Permission breakdown (`600`):**
* `6` (Owner: `r+w` = 4 + 2)
* `0` (Group: no access)
* `0` (Others: no access)



---

#### **4. Authenticating via SSH Identity Flag (`-i`)**

With valid permissions applied to the identity file, the connection was initiated targeting `bandit14` on port `2220`:

```bash
ssh -p 2220 -i sshkey.private bandit14@bandit.labs.overthewire.org

```

Once authenticated inside the `bandit14` shell, the password for the next level was retrieved:

```bash
cat /etc/bandit_pass/bandit14

```

---

