
# 🚀 Delta & DeltaAI — Beginner’s Guide to NCSA Supercomputing

*A Comprehensive Introduction to Delta and DeltaAI at the National Center for Supercomputing Applications (NCSA)*

# What Are Delta and DeltaAI?

Delta and DeltaAI are advanced high-performance computing (HPC) systems operated by National Center for Supercomputing Applications (NCSA) at the University of Illinois Urbana-Champaign. 

These are powerful computing systems that help scientists and researchers solve very large or complex problems using high-performance computing (HPC).

They are available to researchers across the United States through the ACCESS allocation program.
https://allocations.access-ci.org/login

They are designed for:

- High-performance computing (HPC)
- AI/ML model training
- GPU-accelerated research
- Large-scale simulations

# System-Level Architecture Overview
Both systems follow the same HPC design pattern:
- All researchers connecting through SSH or Open OnDemand.
- Delta and DeltaAI each have their own independent login node.
- Each system has its own independent Slurm controller.
- Jobs are submitted from login nodes and dispatched to compute nodes.
- Both systems connect to shared high-performance work file systems, however, the home directories are separate



```text
                     Users (Researchers)
                              │
                       SSH / OnDemand
                              │
       ┌──────────────────────┴──────────────────────┐
    (Delta)                                      (DeltaAI) 
       │                                             │
  Login Nodes                                   Login Nodes
       │                                             │
Slurm Controller                              Slurm Controller
       │                                             │
    CPU + GPU Nodes                              GPU Nodes
       │                                             │
       │                                             │
       ├───────────── Shared Work Storage ───────────┤
       │        /work/hdd         /work/nvme         │
       │                                             │
Separate Home FS                         Separate Home FS


```

---

# 1️⃣ Introduction

## What Are Delta and DeltaAI?

**Delta** and **DeltaAI** are advanced supercomputing systems operated by the National Center for Supercomputing Applications (NCSA) at the University of Illinois Urbana-Champaign.

They are funded by the National Science Foundation (NSF) and are part of the national ACCESS (Advanced Cyberinfrastructure Coordination Ecosystem: Services & Support) program.

These systems allow researchers and students across the United States to run:

- Large-scale simulations  
- Scientific modeling  
- Data-intensive analysis  
- Artificial intelligence (AI)  
- Machine learning (ML)  
- GPU-accelerated computing  

They provide computational power far beyond what personal laptops or standard university servers can handle.

---

# 2️⃣ Why Do These Systems Exist?

Modern research depends on:

- Massive datasets  
- High-performance GPUs  
- Parallel computing  
- Fast networking between machines  
- Large shared storage systems  

Delta and DeltaAI provide:

- Hundreds of compute nodes  
- High-speed Slingshot interconnect networking  
- Parallel file systems  
- Nationally allocated computing infrastructure  

These systems support discoveries in AI, physics, climate science, biomedical engineering, materials science, and more.

---

# 3️⃣ Delta vs DeltaAI — What’s the Difference?

| Feature | Delta | DeltaAI |
|----------|--------|---------|
| Primary Focus | General HPC workloads | AI / Machine Learning |
| Architecture | Heterogeneous (multiple node types) | Homogeneous GH200 architecture |
| GPU Types | A40, A100, H200, MI100 | H100 (Grace Hopper) |
| CPU Support | AMD EPYC | NVIDIA Grace (ARM-based) |
| Best For | Mixed scientific computing | Large-scale AI training |

Think of:

- **Delta** → A flexible, multi-purpose supercomputer  
- **DeltaAI** → A specialized AI supercomputer optimized for deep learning  

---

# 4️⃣ System Architecture

---

## 🖥️ 4.1 Delta Architecture

Delta is a heterogeneous HPC cluster with multiple node types optimized for different workloads.

### Node Types in Delta

| Node Type | Description |
|------------|-------------|
| Login Nodes | Log in, edit code, submit jobs |
| CPU Compute Nodes | Dual AMD EPYC processors |
| NVIDIA A40 GPU Nodes | 4 × A40 GPUs |
| NVIDIA A100 GPU Nodes | 4 × A100 GPUs |
| Large-Memory GPU Nodes | Up to 2 TB RAM + multiple GPUs |
| AMD MI100 GPU Nodes | 8 × AMD MI100 GPUs |

This flexibility allows users to match hardware with their specific computational needs.

---

### 🌐 Network Architecture (Delta)

Delta uses the **HPE/Cray Slingshot interconnect**, which:

- Connects all compute nodes  
- Enables high-speed communication  
- Allows parallel jobs to scale  
- Provides low-latency data transfer  

---

### 💾 Storage Systems (Delta)

| Storage Type | Purpose |
|---------------|----------|
| HOME | Personal persistent storage |
| PROJECT | Shared project space |
| WORK | Scratch space for active jobs |
| Node-local SSD | Temporary high-speed job storage |

Parallel file systems such as Lustre and VAST allow fast shared access across nodes.

---

## 🤖 4.2 DeltaAI Architecture

DeltaAI is purpose-built for artificial intelligence and machine learning workloads.

Unlike Delta, it uses a homogeneous architecture — meaning every compute node is built the same way.

---

### 🧱 DeltaAI Compute Node Design

Each DeltaAI compute node includes:

- 4 × NVIDIA GH200 Grace Hopper Superchips  
- 4 × NVIDIA H100 GPUs  
- 288 CPU cores total  
- 480 GB system RAM  
- 96 GB HBM3 GPU memory per GPU  
- ~3.9 TB local storage  
- 4 × 200 Gbps network interfaces  

The GH200 Superchip tightly integrates the CPU and GPU using NVLink, allowing extremely fast data movement between processor and accelerator.

---

### 🌐 Networking in DeltaAI

DeltaAI also uses the **HPE/Cray Slingshot network**, optimized for:

- High bandwidth  
- Low latency  
- Large distributed AI workloads  

---

### 💾 Storage in DeltaAI

| Directory | Purpose |
|------------|----------|
| HOME | Personal storage |
| PROJECTS | Shared project data |
| WORK | Scratch space for active jobs |

Parallel storage ensures high-throughput access during AI training and simulations.

---

# 5️⃣ How Users Interact with the System

Typical workflow:

1. Apply for ACCESS allocation  
2. Receive account credentials  
3. Log in via SSH  
4. Transfer data  
5. Submit jobs using SLURM  
6. Retrieve results  

### Basic Workflow

Local Computer  
↓  
SSH Login → Login Node  
↓  
Submit Job (SLURM)  
↓  
Compute Nodes Execute Job  
↓  
Results Saved to Storage  

---

# 6️⃣ Why This Matters for Students

Understanding Delta and DeltaAI teaches:

- Parallel computing fundamentals  
- GPU acceleration  
- Distributed systems  
- High-performance networking  
- Real-world AI infrastructure  

These systems reflect how computing works in:

- National laboratories  
- AI research centers  
- Semiconductor companies  
- Climate modeling labs  
- Biomedical simulation research  

Learning HPC early provides a major advantage in research and industry careers.

---

# 7️⃣ Summary

Delta and DeltaAI are:

- NSF-funded supercomputing systems  
- Nationally accessible through ACCESS  
- Designed for advanced scientific and AI workloads  
- Equipped with high-speed networks and parallel storage  
- Scalable from single-node jobs to massive distributed workloads  

Delta = Flexible HPC platform  
DeltaAI = Specialized AI-optimized platform  

Together, they form one of the most powerful research computing environments available to U.S. researchers.

---

# 8️⃣ Logging In & Getting Started

Before running jobs, users must securely log in using SSH.

---

## Requirements Before Login

- Approved ACCESS allocation  
- Registered ACCESS account  
- SSH public key uploaded  
- Internet access (VPN may be required)

---

## Logging In via SSH

To connect to Delta:

```bash
ssh yourusername@delta.ncsa.illinois.edu
```

To connect to DeltaAI:

```bash
ssh yourusername@deltaai.ncsa.illinois.edu
```

Replace `yourusername` with your ACCESS username.

---

## What Is a Login Node?

The login node is where you:

- Write and edit code  
- Create SLURM job scripts  
- Manage files  
- Submit jobs  
- Monitor running jobs  

⚠️ Do NOT run heavy computations on login nodes.

---

## Transferring Files

Upload:

```bash
scp myfile.py yourusername@delta.ncsa.illinois.edu:/home/yourusername/
```

Download:

```bash
scp yourusername@deltaai.ncsa.illinois.edu:results.txt ~/Desktop/
```

---

## Submitting Jobs

1. Create a SLURM script (e.g., `job.sh`)
2. Submit:

```bash
sbatch job.sh
```

3. Monitor:

```bash
squeue -u yourusername
```

4. Check job history:

```bash
sacct
```

---

## Workflow Overview

Local Computer  
↓  
SSH Login  
↓  
Login Node  
↓  
Submit Job (SLURM)  
↓  
Compute Nodes Run Job  
↓  
Results Saved  
↓  
Download Results  

---

## Beginner Tip

- Start with small test jobs  
- Use sample SLURM scripts  
- Monitor resource usage  
- Always run compute-heavy tasks through the scheduler  

---
