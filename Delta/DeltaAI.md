
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
---

# 🔐 9. Data Management — Delta

Managing data efficiently is critical for successful work on Delta.  
Delta provides multiple storage systems optimized for different use cases — from long-term storage to fast temporary space.

---

## 🧱 Storage Types on Delta

Delta provides several key storage areas:

| Storage Area | Purpose | Typical Use |
|--------------|---------|-------------|
| **HOME** | Personal user directory | Store scripts, configs, small data |
| **PROJECT** | Shared project space | Team data and collaboration |
| **WORK** | Scratch space | High-speed space for running jobs |
| **Node-Local SSD** | Local scratch | Ultra fast temporary space per compute node |

---

## 📂 HOME Directory

- Personal, persistent space
- Good for:
  - Scripts
  - Small datasets
  - Configuration files
- Quotas may apply — avoid putting large data here

Example:

```bash
cd ~/   # HOME directory
```

---

## 🤝 PROJECT Directory

- Shared among project members
- Designed for:
  - Collaboration
  - Shared input datasets
  - Model checkpoints and results
- Visible to all users on the project

Example:

```bash
cd /projects/<project_id>/
```

---

## ⚡ WORK Directory

- High-performance **scratch space**
- Designed for:
  - Temporary storage during job execution
  - Large intermediate files
- Not backed up — data may be removed after job completion

Example:

```bash
cd /work/<yourusername>/
```

---

## 📦 Node-Local SSD

- Ultra-fast storage local to a compute node
- Ideal for:
  - I/O heavy workloads
  - Temporary intermediate results
- Data is erased when job completes
- Accessed inside SLURM jobs

Example from within a job:

```bash
LOCAL_SCRATCH=/tmp/scratch
mkdir -p $LOCAL_SCRATCH
```

---

## 💡 Best Practices on Delta

- Store **permanent data** in HOME or PROJECT
- Use **WORK** for job input + output
- Save large intermediate results only when necessary
- Copy important output back to HOME/PROJECT at job end
- Avoid storing large data in HOME

---

## 📊 Quotas and Cleanup

- **HOME** and **PROJECT** may have quotas
- Large data should NOT be stored in HOME
- Scratch space is flushed — **always back up important data**

---

## 🧠 Typical Workflow

1. Upload raw data to **PROJECT**
2. Copy data into **WORK** in your job script
3. Run computation
4. Save results back to **PROJECT**
5. Clean up **WORK / local scratch**

Example in a job script:

```bash
cp /projects/myproj/data/*.dat $WORK
# run training
cp results/* /projects/myproj/output/
```

---

## 📝 Summary — Delta Data Management

Delta uses a tiered storage system:

- **HOME** → personal, persistent  
- **PROJECT** → shared, persistent  
- **WORK** → scratch, fast  
- **Node-Local SSD** → very fast but temporary  

Understanding these helps you use Delta efficiently and avoid data loss.

---
---

# 🔐 10. Data Management — DeltaAI

DeltaAI provides a similar storage layout to Delta but optimized for AI workflows and large data movement.  
Efficient data management is key for large AI training jobs and multi-node workflows.

---

## 🧱 Storage Areas on DeltaAI

DeltaAI provides:

| Storage Area | Purpose | Typical Use |
|--------------|---------|-------------|
| **HOME** | Personal directory | Scripts, small datasets |
| **PROJECTS** | Shared project space | Large datasets, model checkpoints |
| **WORK** | High-speed scratch space | Temporary space during jobs |
| **Node-Local Storage** | Local fast storage | I/O heavy workloads |

---

## 📂 HOME Directory

- Persistent personal directory
- Good for:
  - Scripts
  - Configuration files
  - Small data
- Not for large datasets or training data

Example:

```bash
cd ~/   # HOME directory
```

---

## 🤝 PROJECTS Directory

- Shared among collaborators
- Designed for:
  - Training datasets
  - Model weights and checkpoints
  - Large AI outputs
- Often mounted from high-capacity storage

Example:

```bash
cd /projects/<project_id>/
```

---

## ⚡ WORK Directory

- Fast scratch space for active jobs
- Good for:
  - Large intermediate data
  - Batch processing
  - Distributed training temporary files
- Not backed up — **data may be deleted after job finishes**

Example:

```bash
cd /work/<yourusername>/
```

---

## 🚀 Node-Local Storage (Inside Job)

- Very fast local scratch
- Ideal for:
  - GPU I/O intensive tasks
  - On-node temporary caches
- Must copy results out before job ends

Example (in SLURM job):

```bash
LOCAL_SCRATCH=/tmp/ai_scratch
mkdir -p $LOCAL_SCRATCH
```

---

## 💡 Best Practices on DeltaAI

- Store stable training data in **PROJECTS**
- Use **WORK** for temporary training files and checkpoints
- Copy output checkpoints back to **PROJECTS**
- Always backup important data from WORK
- Don’t run training using HOME alone

---

## 🗂 Quotas & Cleanup

- **HOME** and **PROJECTS** may enforce quotas
- **WORK** and local scratch are ephemeral
- Always copy important files out of WORK

---

## 🧠 Typical AI Workflow

1. Upload datasets to **PROJECTS**
2. Copy datasets to **WORK** in job script
3. Run distributed training
4. Save checkpoints back to **PROJECTS**
5. Clean up temporary files

Example snippet in SLURM script:

```bash
cp /projects/my_ai/data/* $WORK
python train.py --data $WORK
cp $WORK/checkpoints/* /projects/my_ai/output/
```

---

## 📝 Summary — DeltaAI Data Management

DeltaAI’s storage is tailored for large deep learning and AI workloads:

- **HOME** → persistent and personal  
- **PROJECTS** → shared, large capacity  
- **WORK** → fast, temporary  
- **Node-Local Storage** → fastest but temporary  

Good data management helps prevent data loss and speeds up workflows.

---
---

# ⚙️ 11. Running Jobs on Delta

Running jobs on Delta is done through the **SLURM workload manager**.  
Instead of running tasks interactively on the login node, you submit jobs to the scheduler, which then runs them on compute nodes.

---

## 🔹 SLURM Job Basics

A job script is a plain text file with:

- Resource requests (CPUs, GPUs, memory)
- The executable or command to run
- Any environment setup

Example high-level structure:

```bash
#!/bin/bash
#SBATCH --job-name=my_delta_job
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --time=01:00:00
#SBATCH --mem=8000
#SBATCH --output=out.txt

module load python
python script.py
```

---

## 📌 Key SLURM Options

| Option | Meaning |
|---------|---------|
| `--job-name` | Name of the job |
| `--ntasks` | Number of tasks/processes |
| `--cpus-per-task` | CPU cores per task |
| `--time` | Max runtime |
| `--mem` | Memory per node |
| `--output` | File for stdout |

---

## 🔹 Requesting GPUs on Delta

To request GPU resources:

```bash
#SBATCH --gpus=1           # request one GPU
#SBATCH --gpus-per-task=1
```

For multiple GPUs:

```bash
#SBATCH --gpus=4
```

---

## 👷‍♂️ Job Submission

Submit your batch script:

```bash
sbatch my_job.sh
```

List your running jobs:

```bash
squeue -u yourusername
```

Cancel a job:

```bash
scancel <job_id>
```

---

## 📊 Monitoring & Job Details

Check job info:

```bash
sacct -j <job_id>
```

Get detailed status:

```bash
scontrol show job <job_id>
```

---

## 🔁 Interactive Jobs

If you want an interactive session (e.g., for testing):

```bash
srun --pty --ntasks=1 --cpus-per-task=4 --time=00:30:00 bash
```

Once granted, you can work as if logged into a compute node.

---

## ⏱– Time Limits and Priorities

- Jobs must specify a **time limit**
- If time expires, SLURM terminates the job
- Larger requests may wait longer in queue

---

## 🔧 Environment Modules

Delta uses *modules* to load software:

```bash
module avail           # list available modules
module load python     # load Python module
```

Always load required modules in your script.

---

## ♻️ Best Practices on Delta

- Test small before large jobs
- Include clear output redirection
- Save key results back to PROJECT
- Avoid long interactive sessions
- Use environment modules

---

## 🧠 Summary — Running Jobs on Delta

- Use `sbatch` to run jobs
- Request CPU/GPU cores
- Use `squeue`, `sacct` to monitor
- Use modules to manage software

---
---

# ⚙️ 12. Running Jobs on DeltaAI

Job submission on **DeltaAI** is also handled by the **SLURM scheduler**, with additional options tailored for large GPU jobs.

Because DeltaAI nodes provide powerful GPU resources, specifying GPU and memory efficiently is essential.

---

## 🔹 DeltaAI SLURM Script Example

Basic SLURM script on DeltaAI:

```bash
#!/bin/bash
#SBATCH --job-name=my_dai_job
#SBATCH --ntasks=1
#SBATCH --gpus=4
#SBATCH --cpus-per-task=16
#SBATCH --time=02:00:00
#SBATCH --mem=128000
#SBATCH --output=deltaai_out.txt

module load cuda
python train.py
```

---

## 🎯 Key SLURM Directives

| Directive | Purpose |
|-----------|---------|
| `--gpus` | Total GPUs requested |
| `--cpus-per-task` | CPU cores per task |
| `--time` | Maximum runtime |
| `--mem` | Memory per node |
| `--output` | Job stdout file |

---

## 🚀 Multi-GPU / Multi-Node Jobs

DeltaAI supports **multi-GPU and multi-node jobs**:

Example:

```bash
#SBATCH --nodes=2
#SBATCH --gpus-per-node=8
```

This requests 2 nodes × 8 GPUs each.

MPI and distributed training tools (like PyTorch DDP) can use this configuration.

---

## 📤 Job Submission

Submit with:

```bash
sbatch deltaai_job.sh
```

Check status:

```bash
squeue -u yourusername
```

Cancellations:

```bash
scancel <job_id>
```

---

## 📊 Monitoring & Feedback

DeltaAI supports the same monitoring tools:

- `squeue`
- `sacct`
- `scontrol`

Example:

```bash
sacct -j <job_id>
```

This shows memory, CPU and GPU usage.

---

## 💡 GPU Environment Modules

DeltaAI loads CUDA and related modules:

```bash
module avail
module load cuda
```

Verify libraries (e.g., cuDNN) for your framework.

---

## ⏱ Tips for DeltaAI Jobs

- Request correct number of GPUs
- Use proper memory requests for big training jobs
- Allocate longer time for large models
- Use distributed training flags

---

## 🧠 Summary — Running Jobs on DeltaAI

- Submit with `sbatch`
- Request GPUs effectively
- Use multi-node config for distributed training
- Monitor with standard SLURM tools

---
---

# 🧰 13. Job Management Tools & Tips (Delta & DeltaAI)

This section highlights commonly used SLURM commands and job management tips you’ll use on both Delta and DeltaAI.

---

## 🔍 Monitor Jobs

### List jobs for your account:

```bash
squeue -u yourusername
```

### Check job history:

```bash
sacct --format=JobID,JobName,State,Elapsed
```

---

## 🛑 Cancel a Job

```bash
scancel <job_id>
```

---

## 📋 Detailed Job Information

```bash
scontrol show job <job_id>
```

This provides information about node allocation, resource usage, and timing.

---

## 📁 Check Job Output Files

By default, SLURM writes job output to the file you specify:

```bash
#SBATCH --output=job_output.txt
```

You can then view it with:

```bash
less job_output.txt
```

---

## 🧠 Best Job Practices

✅ Always specify resource requests  
✅ Use meaningful job names  
✅ Save important output to PROJECT storage  
✅ Test with small jobs before scaling  
✅ Log both stdout and stderr

---

## 📊 Troubleshooting Jobs

### If a job fails:

Check:

- Resource requests
- Walltime limits
- Module load errors
- Path issues

Use:

```bash
sacct -j <job_id> --format=State,ExitCode
```

---

## 🌐 Job Arrays

For many similar jobs:

```bash
#SBATCH --array=1-100
```

This creates 100 similar jobs with a single script.

---

## 🧠 Quick SLURM Reference

| Command | Purpose |
|---------|---------|
| `sbatch` | Submit a job |
| `srun` | Run an interactive job |
| `squeue` | List pending/running jobs |
| `sacct` | Show accounting info |
| `scancel` | Cancel jobs |
| `scontrol` | Show detailed job info |

---

## 🏁 Summary — Job Management

Understanding SLURM basics makes running jobs on both Delta and DeltaAI efficient and predictable.

---
---

# 🚀 14. First Job — Hands-On Tutorial

This section walks you through submitting your **first job** on Delta or DeltaAI.

We will:

1. Log in
2. Create a simple Python script
3. Write a SLURM job file
4. Submit the job
5. View results

---

## Step 1️⃣ — Log In

```bash
ssh yourusername@delta.ncsa.illinois.edu
```

or

```bash
ssh yourusername@deltaai.ncsa.illinois.edu
```

---

## Step 2️⃣ — Create a Test Python Script

Create a file:

```bash
nano hello.py
```

Paste:

```python
print("Hello from Delta!")
```

Save and exit.

---

## Step 3️⃣ — Create a SLURM Script

```bash
nano job.sh
```

Paste:

```bash
#!/bin/bash
#SBATCH --job-name=hello_test
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --time=00:05:00
#SBATCH --mem=1000
#SBATCH --output=hello_output.txt

module load python
python hello.py
```

Save and exit.

---

## Step 4️⃣ — Submit the Job

```bash
sbatch job.sh
```

You will see:

```
Submitted batch job <job_id>
```

---

## Step 5️⃣ — Monitor Job

```bash
squeue -u yourusername
```

When finished, view output:

```bash
cat hello_output.txt
```

You should see:

```
Hello from Delta!
```

🎉 Congratulations — you just ran your first HPC job!

---
---

# 🔁 15. Visual SLURM Workflow

Below is a simplified diagram of how jobs run on Delta and DeltaAI.

```
+---------------------+
|  Local Computer     |
|  (Your Laptop)      |
+----------+----------+
           |
           |  SSH
           v
+---------------------+
|  Login Node         |
|  - Write code       |
|  - Submit job       |
+----------+----------+
           |
           |  sbatch
           v
+---------------------+
|  SLURM Scheduler    |
|  - Queues job       |
|  - Allocates nodes  |
+----------+----------+
           |
           v
+---------------------+
|  Compute Nodes      |
|  - CPUs / GPUs      |
|  - Run your code    |
+----------+----------+
           |
           v
+---------------------+
|  Storage System     |
|  - HOME             |
|  - PROJECT          |
|  - WORK             |
+---------------------+
```

---

## 🔎 What Happens Behind the Scenes?

1. You submit a job.
2. SLURM checks available resources.
3. When resources free up, your job starts.
4. Compute nodes execute your code.
5. Output is written to storage.
6. You retrieve results.

This system allows thousands of users to share the supercomputer efficiently.

---
---

## 🧠 PyTorch Example — Single GPU Training

### train.py

```python
import torch

print("CUDA available:", torch.cuda.is_available())
print("GPU count:", torch.cuda.device_count())

x = torch.randn(1000, 1000).cuda()
y = torch.matmul(x, x)

print("Computation successful!")
```

---

### SLURM Script

```bash
#!/bin/bash
#SBATCH --job-name=pytorch_test
#SBATCH --gpus=1
#SBATCH --cpus-per-task=4
#SBATCH --time=00:10:00
#SBATCH --mem=8000
#SBATCH --output=pytorch_out.txt

module load cuda
module load python

python train.py
```

Submit:

```bash
sbatch pytorch_job.sh
```

---
