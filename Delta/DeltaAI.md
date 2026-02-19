
# 🚀 Delta & DeltaAI — Beginner’s Guide to NCSA Supercomputing

*A Comprehensive Introduction to Delta and DeltaAI at the National Center for Supercomputing Applications (NCSA)*

# 1. What Are Delta and DeltaAI?

Delta and DeltaAI are advanced high-performance computing (HPC) systems operated by National Center for Supercomputing Applications (NCSA) at the University of Illinois Urbana-Champaign. 

They are available to researchers across the United States through the ACCESS allocation program.
https://allocations.access-ci.org/login

They are are powerful computing systems designed for:

- High-performance computing (HPC)
- AI/ML model training
- GPU-accelerated research
- Large-scale simulations

--- 


# 2. Delta vs DeltaAI — Hardware Comparison

| Category | Delta | DeltaAI |
|-----------|--------|----------|
| Primary Focus | General HPC workloads | Large-scale AI/ML training |
| Architecture | Heterogeneous | Homogeneous |
| CPUs | AMD EPYC | NVIDIA Grace (ARM-based) |
| GPUs | A40, A100, H200, MI100 | H100 (GH200 Grace Hopper) |
| Node Variety | Multiple node types | Identical node configuration |
| Best For | Mixed scientific computing | Distributed deep learning |


---

# 3. Delta Architecture

https://docs.ncsa.illinois.edu/systems/delta/en/latest/user_guide/architecture.html

Node Types: 

- Login nodes (interactive access only)
- CPU compute nodes (dual AMD EPYC)
- NVIDIA A40 GPU nodes
- NVIDIA A100 GPU nodes
- Large-memory GPU nodes (up to 2 TB RAM)
- AMD MI100 GPU nodes

This flexibility allows researchers to match hardware to workload requirements.

---

# 4. DeltaAI Architecture

https://docs.ncsa.illinois.edu/systems/deltaai/en/latest/user-guide/architecture.html#

Delta and DeltaAI share a common HPC design model but differ in hardware architecture and optimization goals. DeltaAI is purpose-built for AI and machine learning.

Each compute node includes:

- 4 × NVIDIA GH200 Grace Hopper Superchips  
- 4 × NVIDIA H100 GPUs  
- 288 CPU cores total  
- 480 GB system RAM  
- 96 GB HBM3 GPU memory per GPU  
- ~3.9 TB local storage  
- 4 × 200 Gbps network interfaces  

The GH200 architecture tightly integrates CPU and GPU via NVLink, enabling extremely fast data movement for large AI models.

---


# 5. How Users Interact with the System: System-Level Architecture Overview
Both systems follow the same HPC design pattern:
- All researchers connecting through SSH or Open OnDemand.
- Delta and DeltaAI each have their own independent login node.
- Each system has its own independent Slurm controller.
- Jobs are submitted from login nodes and dispatched to compute nodes.
- Compute Nodes Execute Job.
- Results Written to Storage
- Both systems connect to shared high-performance work file systems, however, the home directories are separate.



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
Separate Home Directory                       Separate Home Directory

```

---


# 6. Hands-On Tutorial

This section walks you through submitting your **first job** on Delta or DeltaAI.

We will:

Local Computer -> SSH Login -> Login Node -> Submit Job -> Compute Nodes Run Job -> Results Saved -> Download Results  


---
## Step 0 - Before Login

- Approved ACCESS allocation  
- Registered ACCESS account  
- SSH public key uploaded  
- Internet access (VPN may be required)

  
## Step 1 — Log In

```bash
ssh yourusername@delta.ncsa.illinois.edu
```

or

```bash
ssh yourusername@deltaai.ncsa.illinois.edu
```

---

## Step 2 — Create a Test Python Script

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


## 🔎 What Happens Behind the Scenes?

1. You submit a job.
2. SLURM checks available resources.
3. When resources free up, your job starts.
4. Compute nodes execute your code.
5. Output is written to storage.
6. You retrieve results.

This system allows thousands of users to share the supercomputer efficiently.


---

# 7. Data Management — Delta/DeltaAI

Managing data efficiently is critical for successful work on Delta/DeltaAI.  
They provides multiple storage systems optimized for different use cases — from long-term storage to fast temporary space.

## 7.1 Storage Types

Delta provides several key storage areas:

| Storage Area | Purpose | Typical Use |
|--------------|---------|-------------|
| **HOME** | Personal user directory | Store scripts, configs, small data |
| **PROJECT** | Shared project space | Team data and collaboration |
| **WORK** | Scratch space | High-speed space for running jobs |
| **Node-Local SSD** | Local scratch | Ultra fast temporary space per compute node |

DeltaAI provides several key storage areas:

| Storage Area | Purpose | Typical Use |
|--------------|---------|-------------|
| **HOME** | Personal directory | Scripts, small datasets |
| **PROJECTS** | Shared project space | Large datasets, model checkpoints |
| **WORK** | High-speed scratch space | Temporary space during jobs |
| **Node-Local Storage** | Local fast storage | I/O heavy workloads |



## 7.2 HOME Directory

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



## 7.3 PROJECT Directory

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


## 7.4 WORK Directory

- High-performance **scratch space**
- Designed for:
  - Temporary storage during job execution
  - Large intermediate files
- Not backed up — data may be removed after job completion

Example:

```bash
cd /work/<yourusername>/
```


## Notes for Delta/DeltaAI

- Store **permanent data** in HOME/PROJECT
- Use **WORK** for job input + output
- Save large intermediate results only when necessary
- Copy important output back to HOME/PROJECT at job end
- Avoid storing large data in HOME


---

# 8. Key SLURM Options

| Option | Meaning |
|---------|---------|
| `--job-name` | Name of the job |
| `--ntasks` | Number of tasks/processes |
| `--cpus-per-task` | CPU cores per task |
| `--time` | Max runtime |
| `--mem` | Memory per node |
| `--output` | File for stdout |


## Requesting GPUs on Delta

To request GPU resources:

```bash
#SBATCH --gpus=1           # request one GPU
#SBATCH --gpus-per-task=1
```



## Time Limits and Priorities

- Jobs must specify a **time limit**
- If time expires, SLURM terminates the job
- Larger requests may wait longer in queue
