

# ** MODULE 1 — The Evolution of Deployment: Why Containers? (Context)**

### *“At the end of the day… people just want their application to run.”*

---

## **1.0 The Real-World Story — Why This Topic Even Exists**

Think of Swiggy, Zomato, Ola, Uber, Amazon, Flipkart, Netflix.

Behind every order you place…
behind every cab you book…
behind every movie you watch…

There is **code**.

That code is written by developers, but **a developer writing code does not automatically make it available to millions of users**.

For a user to use an application, the code needs to be:

* deployed somewhere
* running continuously
* scalable when load increases
* recoverable when something crashes
* and predictable in behaviour across environments

This brings us to the fundamental challenge in IT for the last 30 years:

> **“How do we run applications in the fastest, most reliable, most scalable way possible?”**

For decades, the world struggled to answer this question.
And the answer evolved slowly…

---

# **1.1 Deployment Era #1 — Physical Servers (Bare Metal)**

### *The Early Days: When a single server ran a single application*

In the early 2000s, applications were deployed on **bare metal servers** — physical machines placed in data centers.

Developers wrote code → Ops Team installed OS → Installed dependencies → Ran the app.

### **But huge problems appeared.**

---

### ** Problem 1: Dependency Hell**

Different applications required different versions of:

* Java
* Python
* Node
* MySQL
* Libraries
* Packages

If Version A required Python 2.7
and Version B required Python 3.10
— both could NOT run on the same machine.

Result?
One server = One application.

---

### ** Problem 2: Ultra-low Utilization**

A typical server:

* 16 CPU
* 64 GB RAM
* 2 TB storage

Running ONE application would use:

* CPU: 10–20%
* RAM: 10–15%
* Storage: 5–10%

So **80% of the resources were wasted**.
This is called **underutilization**.

Companies had 1000 servers but were using the power of only 200.

---

### ** Problem 3: Scaling Was Painful**

If Swiggy suddenly got 10,000 orders in 1 minute:

* A new physical server had to be purchased
* Installed
* Racked
* Connected
* OS configured
* App deployed

This took **days or weeks**.

---

### ** Problem 4: Different Environments Behaved Differently**

Developer machine → QA server → Production server
All had different libraries and versions.

So the classic pain:

> **“Works on my machine but not in production.”**

---

### **Conclusion: Bare Metal Could Not Scale with Modern Apps**

Applications became more complex, users increased, load became unpredictable.
Bare metal was slow, expensive, and rigid.

Thus came the next revolution…

---

# **1.2 Deployment Era #2 — Virtual Machines (VMs)**

### *A breakthrough: Multiple apps on a single physical server.*

When companies realized bare-metal was wasteful, virtualization was invented.

---

## **How VMs Solved the Bare-Metal Problems**

Virtualization introduced a magical layer:

### ** The Hypervisor**

A hypervisor allowed a single physical server to be split into multiple **Virtual Machines**, each acting like a separate computer.

Types of hypervisors:

* **Type 1**: Bare-metal hypervisors (VMware ESXi, Hyper-V, Xen)
* **Type 2**: Hosted hypervisors (VMware Workstation, VirtualBox)

---

### **Advantages of VMs**

Better resource utilization
Each VM had its own OS → strong isolation
Conflicting dependencies solved
Easier to create new servers
Improved security
Snapshots, cloning, and templates made life easier

For almost a decade, VMs ruled the world.

Netflix, Amazon, Google — all built their early systems on massive VM fleets.

---

# **But VMs Introduced New Problems Too**

As applications grew… so did deployments.

Microservices started appearing.
An app had 20, 50, or even 200 components.

Running each as a VM meant:

* Each VM needed its own OS (heavy!)
* Boot time was minutes
* Images were large (GBs)
* Scaling required minutes
* Overhead per VM was huge

### **Example:**

If Swiggy needs to scale its 10 microservices to 100 instances each → 1000 VMs?

**Impossible. Slow. Expensive. Inefficient.**

VMs could not keep up with *cloud-native* speed.

The world needed something:

* faster
* lightweight
* portable
* reproducible
* developer-friendly

And voilà…

---

# **1.3 Deployment Era #3 — Rise of Containers**

### *The single biggest revolution after virtualization.*

Containers were not new — Linux had cgroups and namespaces.
But **Docker** made containers accessible to everyone.

---

## **Why Containers Became the Game-Changer**

###  **1. Lightweight (No separate OS)**

Containers share the host OS kernel → no need to boot a full OS.

VM boot time: **30–90 seconds**
Container boot time: **100–500 milliseconds**

###  **2. High Density**

1 server → can run **100s of containers**
(Instead of 5–10 VMs)

###  **3. Same Code, Same Environment Everywhere**

Dev = QA = Prod
ZERO configuration drift.

###  **4. Perfect for Microservices**

Each microservice gets its own container.
Easy scaling.
Easy CI/CD.
Easy debugging.

###  **5. Portability**

Build once → Run anywhere:

* Laptop
* On-prem servers
* AWS
* Azure
* GCP
* Kubernetes
* Edge devices

---

# **1.4 What Problems Containers Solve (Summary)**

| Problem           | Bare Metal | VM     | Container  |
| ----------------- | ---------- | ------ | ---------- |
| Dependency Hell   | ❌          | ✔️     | ✔️         |
| Resource Wastage  | ❌          | ✔️     | ✔️✔️       |
| Boot Time         | Slow       | Medium | Ultra-fast |
| Portability       | ❌          | ❌      | ✔️         |
| Scaling           | Painful    | Slow   | Instant    |
| Dev/Prod mismatch | High       | Medium | Zero       |
| Image Size        | GBs        | GBs    | MBs        |

---

# **1.5 Key Concepts**

## ** What is a Container?**

A **container** is a lightweight, isolated environment that runs an application with its own dependencies, libraries, and filesystem — but **shares the host OS kernel**.

The magic lies in:
namespaces → isolation
cgroups → resource control
union file systems → layered images

## ** Container vs. VM (Deep Comparison)**

* VMs virtualize hardware → each needs full OS
* Containers virtualize OS → share kernel

Result?
Containers are **10× faster**, **10× smaller**, and **10× more scalable**.

## ** Docker Images & Layers**

A Docker image is built in **layers** using a **union filesystem**.
Each instruction in Dockerfile creates a new layer.

Layers = caching → faster builds.

## ** Container Engine (Docker)**

Docker provides:

* Docker daemon
* Docker CLI
* Docker registry
* Container runtime

Docker standardised container usage worldwide.

---

# **1.6 LABS — Hands-on**

###  **Lab 1: Install Docker**

On Linux, Windows, or Mac.

###  **Lab 2: Run first container**

```bash
docker run hello-world
```

###  **Lab 3: Compare VM Boot vs Container Boot**

* Start a VM → measure time
* Start a container → measure time
* Observe difference

### **Lab 4: Inspect Container Filesystem**

```bash
docker run -it ubuntu bash
ls -l /
```

Explore how the container sees the filesystem.

---



