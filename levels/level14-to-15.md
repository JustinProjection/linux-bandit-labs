# 🚩 Bandit Level 14 → Level 15

### **Objective**

Retrieve the password for `bandit15` by submitting the current level's password (`bandit14`) to TCP port `30000` on `localhost`.

---

### **Key Concepts Covered**

* **Netcat (`nc`) as a Networking Utility:** Using the "Swiss Army knife of networking" for port verification and raw TCP communication.
* **Understanding `localhost`:** Interacting with local loopback services (`127.0.0.1`) running directly on the target machine.
* **Interactive TCP Sockets vs. Scanning Mode:** Distinguishing between port-checking flags (`-z`) and live data streaming.

---

### **Step-by-Step Solution & Methodology**

#### **1. Reconnaissance & Port Verification (`-vz`)**

Before throwing data at a port, it is standard practice to confirm that a service is actually listening. Netcat was used in verbose (`-v`) and zero-I/O scanning mode (`-z`):

```bash
nc -vz localhost 30000

```

*Output:*

```text
Connection to localhost (127.0.0.1) 30000 port [tcp/*] succeeded!

```

* **Why this matters:** The `-z` flag tells Netcat to check the port and close immediately without sending or receiving data. The `succeeded!` message confirmed that a listener was live on port `30000` and ready to talk.

---

#### **2. Establishing an Interactive Connection**

To talk to the service, the `-z` flag was dropped to keep the TCP socket open as an interactive pipe:

```bash
nc -v localhost 30000

```

---

#### **3. Submitting the Payload**

With the interactive connection open and waiting for input, the current level's password for `bandit14` was entered:

```text
[Current Level Password]

```

*Response:*

```text
Correct!
[Password for bandit15]

```

---


---
