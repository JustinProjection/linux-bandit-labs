# 🚩 Bandit Level 15 → Level 16

### **Objective**

Retrieve the password for `bandit16` by submitting the current level's password (`bandit15`) to TCP port `30001` on `localhost` using **SSL/TLS encryption**.

---

### **Key Concepts Covered**

* **Encrypted Network Communications (SSL/TLS):** Understanding how TLS wraps raw TCP sockets in an encrypted tunnel to protect data in transit.
* **`openssl s_client`:** Using OpenSSL’s diagnostic client tool to execute manual TLS handshakes and interact with secure remote or local services.
* **Plaintext vs. Encrypted Services:** Recognizing why standard Netcat (`nc`) fails on secure ports and why a dedicated cryptographic client is required.

---

### **Step-by-Step Solution & Methodology**

#### **1. Identifying the Encryption Requirement**

Unlike the previous level where port `30000` accepted plaintext via Netcat, port `30001` enforces SSL/TLS encryption right from the connection phase. Standard raw sockets will fail because the service expects a cryptographic handshake before exchanging data.

---

#### **2. Establishing a Secure Connection with OpenSSL**

To connect to the encrypted service, the OpenSSL client diagnostic tool (`s_client`) was utilized to target `localhost` on port `30001`:

```bash
openssl s_client -connect localhost:30001

```

* **What this command does:**
* `openssl`: Invokes the cryptography and SSL/TLS toolkit.
* `s_client`: Acts as a TLS client, initiating a secure connection to the target.
* `-connect localhost:30001`: Specifies the destination address and encrypted port.



Upon execution, the terminal displayed the full TLS handshake output, certificate details, and cipher information before establishing a secure, encrypted tunnel.

---

#### **3. Submitting the Payload**

With the secure session successfully open and waiting for input, the current password for `bandit15` was typed and entered into the stream:

```text
[Current Level Password for bandit15]

```

*Response:*

```text
Correct!
[Password for bandit16]



---

