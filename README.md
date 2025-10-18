# container-hardway


<summary>Traditional Software Deployment - Dependency Hell</summary>
<details>
# 🧩 Traditional Software Deployment — The “Dependency Hell”

Before containers and modern DevOps, deploying software was a **nightmare**.  
Let’s explore how **dependency hell**, **library conflicts**, and **environment drift** created chaos across teams — from application developers to infrastructure operators.

---

## ⚙️ 1. Overview

Traditional software deployment meant installing applications **directly on the host machine** (bare-metal or VM).  
Everything — libraries, configurations, binaries — lived together in the **same OS environment**.

While this worked for small systems, it quickly fell apart as complexity grew.

---

## 💣 2. The “Dependency Hell”

**Dependency Hell** refers to the pain of managing software dependencies across environments.

### 🔸 Example Scenario
You build an app requiring:
- Python 3.8  
- `numpy==1.21.0`  
- `pandas==1.3.0`

But the production server already runs:
- Python 3.10  
- `numpy==1.18.0` (used by another app)

Result:  
Your app **fails** due to version mismatches — and updating breaks other applications.

### 🔸 Causes
- Shared system libraries between multiple apps  
- Conflicting package versions  
- OS-level dependency differences (Ubuntu vs CentOS)  
- Manual installs & lack of isolation  
- No reproducible environment (works on my machine 😅)

---

## 🧱 3. Application Layer Problems

| Problem | Description |
|----------|--------------|
| 🧩 Library Conflicts | Different apps require different versions of the same library. |
| 🧠 Environment Drift | Dev, staging, and production environments slowly become inconsistent. |
| 🔄 Manual Deployment | Developers manually copy code, run scripts, install libs — error-prone and inconsistent. |
| 🧍 Human Dependency | Deployment success often depends on a specific person who “knows the setup.” |

---

## 📦 4. Library & System Dependency Problems

| Issue | Impact |
|-------|---------|
| Global package installs | Breaks other apps sharing the same host. |
| Different OS versions | Missing or incompatible system libs. |
| Manual package management | Difficult to track what’s installed where. |
| No rollback mechanism | Once broken, hard to recover previous working state. |

---

## 🧰 5. Operations (Ops) Problems

| Problem | Description |
|----------|-------------|
| 🔧 Configuration Drift | Configs change manually over time — no single source of truth. |
| ⚠️ Hard to Reproduce | Rebuilding a server requires manual steps and tribal knowledge. |
| ⏳ Slow Provisioning | Installing dependencies, setting up databases, etc., takes hours/days. |
| 🧨 No Isolation | One app crash or update may affect all apps on the same host. |

---

## 🏗️ 6. Infrastructure Problems

| Problem | Description |
|----------|-------------|
| 🧱 Static Infrastructure | Servers are manually configured and long-lived. |
| 🚫 No Scalability | Hard to scale apps quickly — provisioning new servers is slow. |
| 🧩 Inconsistent Environments | Every server might be slightly different. |
| 💀 Hard Recovery | When a server dies, rebuilding is time-consuming. |

---

## 🔥 7. The Result — Chaos Everywhere

- “**Works on my machine**” syndrome  
- Downtime during deployments  
- Conflicts between dev, ops, and infra teams  
- No automation or repeatability  
- Complex rollback and debugging  
- Tight coupling between app and environment  

---

## 🌈 8. The Turning Point

To solve these problems came **modern solutions**:
- **Virtual Machines (VMs)** → First level of isolation  
- **Containers (Docker, Kubernetes)** → Lightweight, portable environments  
- **Infrastructure as Code (IaC)** → Automate provisioning (Terraform, Ansible)  
- **CI/CD Pipelines** → Automate build, test, and deployment  

---

## ✅ 9. Summary

| Layer | Traditional Problem | Modern Fix |
|--------|----------------------|-------------|
| Application | Dependency conflicts | Containers / Virtual Environments |
| Libraries | Version mismatch | Dependency managers (pip, npm, etc.) |
| Operations | Manual config & deploy | CI/CD pipelines |
| Infrastructure | Static servers | IaC (Terraform, Ansible, CloudFormation) |

---

## 🧭 10. Key Takeaway

> Traditional deployment bound **applications, dependencies, and infrastructure tightly together** — making systems fragile, slow to change, and painful to maintain.  
>  
> Modern DevOps and containerization **decouple these layers**, bringing consistency, scalability, and reproducibility.

---


</details>


<summary>Virtual Machine</summary>
<details>

Each VM behaves like a **separate computer**, isolated from others, even though they share the same physical hardware.

---

```
+-----------------------------------+
| Physical Hardware (CPU, RAM, Disk)|
+-----------------------------------+
| Host OS (e.g., Ubuntu, Windows) |
+-----------------------------------+
| Hypervisor (VMware, VirtualBox) |
+-----------------------------------+
| Guest OS 1 | Guest OS 2 | Guest OS 3 |
| (Ubuntu) | (CentOS) | (Windows) |
+-----------------------------------+
| App A | App B | App C |
```

## 🧩 2. Key Components

| Component | Description |
|------------|--------------|
| **Host OS** | The operating system installed on the physical machine. |
| **Guest OS** | The OS running inside the VM (can be different from the host). |
| **Hypervisor** | The layer that manages VMs, allocating CPU, memory, and disk resources. |
| **Virtual Hardware** | Virtual CPU, memory, disk, and network interfaces that mimic real hardware. |

---

## 🧱 3. Types of Hypervisors

| Type | Description | Examples |
|------|--------------|-----------|
| **Type 1 (Bare-metal)** | Runs directly on hardware, no host OS. Best performance. | VMware ESXi, Microsoft Hyper-V, Xen |
| **Type 2 (Hosted)** | Runs on top of a host OS. Easier to use but slower. | VirtualBox, VMware Workstation |

---

## 🧰 4. How VMs Solve Traditional Problems

| Traditional Problem | How VMs Help |
|----------------------|--------------|
| 🧩 Dependency Conflicts | Each VM has its own OS and libraries — no interference. |
| 🧠 Environment Drift | VM images can be cloned, ensuring consistent environments. |
| ⚙️ Ops Overhead | Automate provisioning using VM templates. |
| 💀 Server Failure | Snapshots and backups allow quick recovery. |
| 🔒 Security | Isolation prevents one app from crashing another. |

---

## ⚡ 5. VM Workflow Example

1. **Create VM image** with OS + dependencies (e.g., Ubuntu + Python 3.8).  
2. **Deploy app** into the VM.  
3. **Snapshot or clone** the VM for staging/production.  
4. **Run multiple VMs** on one server, each isolated.  
5. **Monitor and manage** using hypervisor tools.

---

## 🧱 6. Benefits of Virtual Machines

| Advantage | Description |
|------------|--------------|
| ✅ **Isolation** | Each VM runs independently, preventing conflicts. |
| 🔁 **Reproducibility** | VM images can be replicated exactly. |
| 🔒 **Security** | Compromise in one VM doesn't affect others. |
| ⚙️ **Flexibility** | Can run different OS types (Linux, Windows, etc.) on one host. |
| 💾 **Snapshots** | Easy backup and rollback. |
| ☁️ **Cloud Adoption** | Enabled cloud computing (AWS EC2, Azure VMs). |

---

## 🧨 7. Limitations of Virtual Machines

| Limitation | Description |
|-------------|--------------|
| 🐢 **Heavyweight** | Each VM runs a full OS — consumes large memory & disk. |
| ⚡ **Slow Startup** | Booting a VM takes minutes (vs. seconds for containers). |
| 💽 **Resource Duplication** | Multiple OS instances duplicate system resources. |
| 🔄 **Complex Management** | Requires hypervisor-level setup and patching. |
| 🧩 **Limited Portability** | Moving VMs between platforms can be slow and large (GBs). |

---

## 🏗️ 8. Virtual Machines vs. Traditional Deployment

| Feature | Traditional Deployment | Virtual Machines |
|----------|------------------------|------------------|
| Environment Isolation | ❌ Shared OS | ✅ Full OS per app |
| Dependency Conflicts | ❌ Frequent | ✅ Eliminated |
| Portability | ❌ Low | ⚙️ Moderate |
| Resource Usage | ⚡ Light | 🐢 Heavy |
| Startup Speed | ⚡ Fast | 🐢 Slow |
| Rollback | ❌ Hard | ✅ Easy (snapshots) |

---

## 🌍 9. VMs in Modern Infrastructure

Even today, VMs remain **the foundation of the cloud**:
- **AWS EC2**, **Azure Virtual Machines**, **Google Compute Engine** → all are VM-based.  
- Containers (like Docker) often run **on top of VMs** for extra isolation.

> 💡 VMs provide hardware-level isolation,  
> while containers provide process-level isolation — lightweight but less isolated.

---

## ✅ 10. Summary

| Concept | Key Idea |
|----------|-----------|
| Virtual Machine | A full OS running inside another OS. |
| Hypervisor | The software that manages VMs. |
| Benefit | Isolation, reproducibility, security. |
| Downside | Heavy, slower, and resource-hungry. |
| Modern Role | Foundation for cloud platforms and container hosts. |

---

## 🧭 11. Key Takeaway

> Virtual Machines were the **first major solution** to dependency hell and environment inconsistency.  
> They brought **isolation, portability, and disaster recovery**,  
> but at the cost of **performance and efficiency** — leading to the rise of **containers** (Docker, Kubernetes).

---



</details>

<summary>What is Container</summary>
<details>
# 📦 Containers — Lightweight, Portable, and Fast Deployment

After Virtual Machines (VMs), the next revolution in software deployment was **Containers** —  
a lightweight way to package, ship, and run applications **consistently** across environments.

---

## ⚙️ 1. What Is a Container?

A **Container** is a **lightweight, isolated environment** that bundles:
- Your **application code**
- All its **dependencies**, **libraries**, and **configurations**

It shares the **same host OS kernel**, unlike a Virtual Machine (which runs a full OS per app).

---

### 🧩 Simplified View
```
Traditional Deployment:
App A + Libs ---> Host OS
App B + Libs ---> Host OS → Conflicts!

Virtual Machines:
App + Libs + Guest OS ---> Hypervisor ---> Host OS
App + Libs + Guest OS ---> Hypervisor ---> Host OS

Containers:
App + Libs ---> Container Runtime ---> Host OS (shared kernel)
App + Libs ---> Container Runtime ---> Host OS
```


Each container runs **isolated**, but they all share the **same OS kernel**, making them **lightweight and fast**.

---

## 🧱 2. Core Components

| Component | Description |
|------------|--------------|
| **Container Image** | A read-only template that defines what’s inside the container (OS libs, app code, env vars). |
| **Container Runtime** | The engine that runs containers (e.g., Docker, containerd). |
| **Dockerfile** | Blueprint for building images (defines base image, commands, dependencies). |
| **Container Registry** | Storage for images (Docker Hub, AWS ECR, GCP Artifact Registry). |

---

## 🧰 3. How Containers Work

1. **Build** an image from a `Dockerfile`  
   → includes code, dependencies, configs.

2. **Run** the image as a container  
   → isolated environment with its own filesystem, processes, and network.

3. **Ship** the same image to dev, test, and prod  
   → runs identically everywhere.


## Containers vs Virtual Machines
| Feature            | Virtual Machines                   | Containers                   |
| ------------------ | ---------------------------------- | ---------------------------- |
| **Isolation**      | Full OS isolation                  | Process-level isolation      |
| **Startup Time**   | Minutes                            | Seconds                      |
| **Size**           | GBs                                | MBs                          |
| **Performance**    | Heavy (hypervisor overhead)        | Near-native                  |
| **Portability**    | High (image-based)                 | Very high                    |
| **Resource Usage** | Each VM duplicates OS              | Shared kernel — efficient    |
| **Use Case**       | Full OS isolation, strong security | Fast, scalable microservices |

## 🔒 5. Container Isolation Mechanisms

### Containers use Linux kernel features:

- Namespaces → isolate processes (PID, network, mount, user)
- cgroups (Control Groups) → limit CPU, memory, I/O usage
- UnionFS → layer filesystem for images (fast & space-efficient)

🧠 Essentially, containers are isolated processes, not virtual machines.

## Benefits of Containers
| Benefit            | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| 🚀 **Lightweight** | No need for full OS per app — faster and smaller.            |
| 🔁 **Portable**    | Runs anywhere (dev, test, prod, cloud).                      |
| ⚙️ **Consistent**  | Same image = same environment across all systems.            |
| 🧱 **Modular**     | Each service can run in its own container (microservices).   |
| 🧩 **Scalable**    | Easily scale up/down using orchestration tools (Kubernetes). |
| 🔒 **Isolated**    | Apps run independently, reducing interference.               |

## Limitations of Containers
| Limitation                   | Description                                                         |
| ---------------------------- | ------------------------------------------------------------------- |
| 🔐 **Shared Kernel**         | Containers share the same OS kernel — less isolation than VMs.      |
| 🧱 **State Persistence**     | Containers are ephemeral; data must be stored externally (volumes). |
| 🧰 **Security Risks**        | Kernel vulnerabilities can affect all containers.                   |
| ⚙️ **Complex Orchestration** | Managing hundreds of containers needs tools like Kubernetes.        |

</details>


# Linux Container - Main Components

## NameSpace
<summary>What is NameSpace</summary>
<details>
# 🧩 Linux Namespaces — The Core of Container Isolation

**Namespaces** are one of the key mechanisms that make **containers** possible.  
They provide **process isolation** — giving each container its own view of system resources.

---

## ⚙️ 1. What Is a Namespace?

A **namespace** is a **Linux kernel feature** that wraps a set of system resources and presents them to a process as if it were the only process using those resources.

> 🧠 Think of a namespace as a "private world" for a process —  
> it sees only its own processes, network, mounts, and users.

Namespaces allow containers to appear **independent**, even though they share the same kernel.

---

## 🔒 2. Why Namespaces Exist

Without namespaces:
- All processes see the same PID list.
- All network interfaces are shared.
- All users belong to the same system.

With namespaces:
- Each process gets its **own PID tree**, **network stack**, and **mount view**.
- Processes are **isolated**, even while running on the same OS.

---

## 🧱 3. Types of Namespaces

| Namespace | System Resource Isolated | Example | Description |
|------------|---------------------------|----------|--------------|
| 🗂️ **Mount (mnt)** | Filesystem mounts | `/proc`, `/etc` | Each container has its own view of the filesystem. |
| 🧍 **Process ID (pid)** | Process tree | `ps`, `top` | A container sees only its own processes (PID 1 = its init). |
| 🧠 **UTS (Unix Timesharing System)** | Hostname, domain | `hostname` | Each container can have its own hostname. |
| 👤 **User (user)** | User and group IDs | `root`, `uid/gid` | A process can be root inside a container but unprivileged outside. |
| 🌐 **Network (net)** | Network stack | `eth0`, `lo`, IPs | Each container gets its own network interfaces and routing tables. |
| ⚙️ **CGroup (cgroup)** | Resource management | CPU, memory | Used with cgroups to limit CPU/memory usage per container. |
| 💬 **IPC (Inter-Process Communication)** | Shared memory, message queues | `shm`, `sem` | Processes communicate only within their own IPC namespace. |
| ⏰ **Time (time)** | System clock | `date`, `hwclock` | Each container can have its own view of system time. (newer feature) |

---

## 🧩 4. Example: PID Namespace

### 🧠 Concept
Each container thinks it has its own process tree starting from **PID 1**.

### 🔍 Without Namespace
```bash
ps aux
# Shows all system processes
```
### 🧱 With Namespace
```
unshare --pid --fork --mount-proc bash
ps aux

# Shows only processes inside this namespace
```
The process inside sees itself as PID 1 — just like an independent OS.

### User Namespace Example

Allows mapping of user IDs inside and outside containers.

Example:
A process can run as root (UID 0) inside the container,
but as a non-root user on the host.

```
unshare --user --map-root-user bash
whoami
# Output: root
```

The process believes it’s root, but it’s safely mapped to an unprivileged user outside.

### Working With Namespaces
| Command       | Purpose                                             |
| ------------- | --------------------------------------------------- |
| **`unshare`** | Create a new namespace and run a command inside it. |
| **`nsenter`** | Enter an existing namespace from another process.   |


#### Example 1 — Create a new namespace
```
unshare --uts --pid --net --mount bash
```

=> Creates new hostname, process, network, and mount namespaces.

### Example 2 — Enter a namespace
```
nsenter --target <pid> --net
```

=> oins the network namespace of another process.

### Combining Namespaces

| Namespace | Purpose                                               |
| --------- | ----------------------------------------------------- |
| `mnt`     | Isolate filesystem mounts                             |
| `pid`     | Isolate process tree                                  |
| `uts`     | Isolate hostname                                      |
| `user`    | Isolate permissions                                   |
| `net`     | Isolate network interfaces                            |
| `ipc`     | Isolate inter-process communication                   |
| `time`    | Isolate clock                                         |
| `cgroup`  | Limit resource usage (works together with namespaces) |

</details>

## Control Group
<summary>What is Cgroup</summary>
<details>
# ⚙️ Linux Control Groups (cgroups) — Resource Management for Containers

**Control Groups (cgroups)** are a **Linux kernel feature** that allow the system to **limit, isolate, and measure resource usage** (CPU, memory, I/O, etc.) for groups of processes.  
They work **together with namespaces** to make containers truly isolated and efficient.

---

## 🧩 1. What Are Control Groups?

> **cgroups = control + groups**

They let you:
- **Allocate** specific hardware resources to a group of processes  
- **Limit** how much CPU, memory, or disk I/O they can use  
- **Measure** their usage and performance  
- **Isolate** them from other groups

> 🧠 Think of cgroups as “resource fences” around processes —  
> ensuring one container cannot starve others.

---

## 🧱 2. How Containers Use cgroups

When you run a container (e.g., with Docker or Kubernetes):
- A **new cgroup** is created for that container.
- CPU, memory, and I/O usage are tracked and limited based on configuration.
- The kernel enforces these limits automatically.

Example:  
```bash
docker run --memory=256m --cpus=0.5 nginx
```
=> Docker translates these flags into cgroup settings behind the scenes.

### Types of cgroups (Controllers)
| Controller        | Description                                                              |
| ----------------- | ------------------------------------------------------------------------ |
| 🧠 **cpuset**     | Assigns specific CPUs and memory nodes to tasks. Useful for CPU pinning. |
| ⚙️ **cpu**        | Controls CPU scheduling — how much processing time tasks get.            |
| 📊 **cpuacct**    | Reports CPU usage for accounting and monitoring.                         |
| 🔢 **pids**       | Limits the number of processes in a group. Prevents fork bombs.          |
| 💾 **io / blkio** | Limits read/write operations to block devices (disk I/O).                |
| 🧮 **memory**     | Sets limits on RAM usage; can trigger OOM killer if exceeded.            |
| 💽 **devices**    | Controls access to device files (`/dev/sda`, `/dev/null`, etc.).         |
| 🧊 **freezer**    | Suspends or resumes all tasks in the group.                              |
| 🌐 **net_cls**    | Tags network packets with class IDs for traffic control.                 |
| 📶 **net_prio**   | Dynamically sets network interface priorities per group.                 |
| 🎯 **perf_event** | Restricts performance event monitoring.                                  |
| 📏 **hugetlb**    | Enables huge pages usage for memory-intensive workloads.                 |

### Common Use Cases
| Use Case                     | Example                                     |
| ---------------------------- | ------------------------------------------- |
| Limit memory per container   | `memory.limit_in_bytes = 512M`              |
| Limit CPU time               | `cpu.shares = 512`                          |
| Restrict number of processes | `pids.max = 100`                            |
| Control I/O throughput       | `blkio.throttle.write_bps_device = 1048576` |
| Assign specific CPU cores    | `cpuset.cpus = 0,1`                         |

### Working with cgroups (File System Interface)

cgroups expose a virtual filesystem (usually mounted at `/sys/fs/cgroup`).

```
/sys/fs/cgroup/
├── cpu/
│   ├── cgroup.procs
│   ├── cpu.shares
│   └── cpu.cfs_quota_us
├── memory/
│   ├── memory.limit_in_bytes
│   ├── memory.usage_in_bytes
│   └── cgroup.procs
└── pids/
    ├── pids.max
    └── cgroup.procs
```

### 🧩 Example: Create and Limit a Process

#### 1️⃣ Create a new cgroup for memory
```
mkdir /sys/fs/cgroup/memory/testgroup
```

#### 2️⃣ Set a 100MB memory limit
```
echo 104857600 > /sys/fs/cgroup/memory/testgroup/memory.limit_in_bytes
```

#### 3️⃣ Add a process (e.g., PID 12345) to that group
```
echo 12345 > /sys/fs/cgroup/memory/testgroup/cgroup.procs
```
 => ✅ That process can now use up to 100MB RAM only.

### Checking Usage

You can monitor usage directly via cgroup files:
```
cat /sys/fs/cgroup/memory/testgroup/memory.usage_in_bytes
cat /sys/fs/cgroup/cpu/testgroup/cpuacct.usage
```

=> These are updated in real-time by the kernel.

### Freezing and Resuming Processes

You can suspend or resume all processes in a cgroup:

```
# Freeze
echo FROZEN > /sys/fs/cgroup/freezer/testgroup/freezer.state

# Resume
echo THAWED > /sys/fs/cgroup/freezer/testgroup/freezer.state

```

### cgroups + namespaces = containers
| Mechanism      | Purpose                                                    |
| -------------- | ---------------------------------------------------------- |
| **Namespaces** | Isolate what a process can see (filesystem, PID, network). |
| **Cgroups**    | Control what a process can use (CPU, memory, I/O).         |

### Summary
| Concept         | Description                                                                      |
| --------------- | -------------------------------------------------------------------------------- |
| **cgroups**     | Kernel mechanism to control and account system resources per group of processes. |
| **Controllers** | Manage specific resources (CPU, memory, IO, etc.).                               |
| **Interface**   | Exposed via virtual filesystem `/sys/fs/cgroup/`.                                |
| **Integration** | Used by Docker, Kubernetes, and systemd.                                         |
| **Goal**        | Prevent one process or container from consuming all resources.                   |


</details>


