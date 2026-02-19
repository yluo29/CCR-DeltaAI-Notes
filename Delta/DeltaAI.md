
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

# 2. Delta Architecture

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

# 3. DeltaAI Architecture

https://docs.ncsa.illinois.edu/systems/deltaai/en/latest/user-guide/architecture.html

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


# 4. How Users Interact with the System: System-Level Architecture Overview
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


# 5. Hands-On Tutorial

This section walks you through submitting your **first job** on Delta or DeltaAI. We will:

Local Computer -> SSH Login -> Login Node -> Submit Job -> Compute Nodes Run Job -> Results Saved -> Download Results  


## Step 0 — Before Login

- Approved ACCESS allocation  
- Registered ACCESS account  
- SSH public key uploaded  
- Internet access (VPN is required outside of campus)

  
## Step 1 — Log In

```bash
ssh username@delta.ncsa.illinois.edu
```

or

```bash
ssh username@dtai-login.delta.ncsa.illinois.edu
```

Replace 'username' with your real account name

After running the command:

- Enter your NCSA password when prompted (the terminal won’t show characters as you type).
- Complete DUO multi-factor authentication (enter your 6-digit Duo passcode)

Upon successful login, you’ll see a welcome message on the login node.
```bash
      ΔΔΔΔΔ    ΔΔΔΔΔΔ   ΔΔ     ΔΔΔΔΔΔ   ΔΔ
      ΔΔ  ΔΔ   ΔΔ       ΔΔ       ΔΔ    ΔΔΔΔ
      ΔΔ  ΔΔ   ΔΔΔΔ     ΔΔ       ΔΔ   ΔΔ  ΔΔ
      ΔΔ  ΔΔ   ΔΔ       ΔΔ       ΔΔ   ΔΔΔΔΔΔ
      ΔΔΔΔΔ    ΔΔΔΔΔΔ   ΔΔΔΔΔΔ   ΔΔ   ΔΔ  ΔΔ
```
or
```bash
    ΔΔΔΔΔ    ΔΔΔΔΔΔ   ΔΔ    ΔΔΔΔΔΔ   ΔΔ         ΔΔ    ΔΔΔΔ
    ΔΔ  ΔΔ   ΔΔ       ΔΔ      ΔΔ    ΔΔΔΔ       ΔΔΔΔ    ΔΔ
    ΔΔ  ΔΔ   ΔΔΔΔ     ΔΔ      ΔΔ   ΔΔ  ΔΔ     ΔΔ  ΔΔ   ΔΔ
    ΔΔ  ΔΔ   ΔΔ       ΔΔ      ΔΔ   ΔΔΔΔΔΔ     ΔΔΔΔΔΔ   ΔΔ
    ΔΔΔΔΔ    ΔΔΔΔΔΔ   ΔΔΔΔΔΔ  ΔΔ   ΔΔ  ΔΔ     ΔΔ  ΔΔ  ΔΔΔΔ
```
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



## Step 3 — Create a SLURM Script

```bash
nano job.sh
```

Paste:

```bash
#!/bin/bash
#SBATCH --job-name=hello_test
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --time=24:00:00
#SBATCH --mem=1000
#SBATCH --output=hello_output.txt

module load python
python hello.py
```

Save and exit.


## Step 4 — Submit the Job

```bash
sbatch job.sh
```

You will see:

```
Submitted batch job <job_id>
```


## Step 5 — Monitor Job

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



## What Happens Behind the Scenes?

1. You submit a job.
2. SLURM checks available resources.
3. When resources free up, your job starts.
4. Compute nodes execute your code.
5. Output is written to storage.
6. You retrieve results.

This system allows thousands of users to share the supercomputer efficiently.


---

# 6. Data Management — Delta/DeltaAI
They provides multiple storage systems optimized for different use cases — from long-term storage to fast temporary space.

## 6.1 Storage Types
Each user has a home directory, $HOME, located at /u/$USER. For each project they are assigned to, they will also have access to shared file space under /projects and /work/hdd.

Delta provides several key storage areas:

| **File System** | **Path**     | **Quota**                                                                                                | **Snapshots** | **Key Features**                                                                                               |                               |
| --------------- | ------------ | -------------------------------------------------------------------------------------------------------- | ------------- | -------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| **HOME**        | `/u`         | 90 GB; 500,000 files per user                                                                            | Yes (30 days) | Area for software, scripts, job files, and so on. Not intended as a source or destination for I/O during jobs. |                               |
| **PROJECTS**    | `/projects`  | 500 GB. Up to 1–25 TB by allocation request. Large requests may have a fee.                              | No/TBA        | Area for shared data for a project, common data sets, software, results, and so on.                            |                               |
| **WORK – HDD**  | `/work/hdd`  | 1000 GB. Up to 1–100 TB by allocation request. Submit a support request.                                 | No            | Area for computation, largest allocations, where I/O from jobs should occur (your scratch volume).             |                               |
| **WORK – NVME** | `/work/nvme` | NVME space is available upon request; submit a support request.                                          | No            | Area for computation; NVME is best for lots of small I/O from jobs.                                            |                               |
| **`/tmp`**      | `/tmp`       | 0.74 TB (CPU) or 1.50 TB (GPU) shared or dedicated depending on node usage by job(s), no quotas in place | No            | Locally attached disk for fast small file I/O.                                          




DeltaAI provides several key storage areas:

| **File System** | **Path**     | **Quota**                                                                        | **Snapshots** | **Key Features**                                                                                               |                               |
| --------------- | ------------ | -------------------------------------------------------------------------------- | ------------- | -------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| **HOME**        | `/u`         | 90 GB; 600,000 files per user                                                    | Yes (30 days) | Area for software, scripts, job files, and so on. Not intended as a source or destination for I/O during jobs. |                               |
| **PROJECTS**    | `/projects`  | 500 GB. Up to 1–25 TB by allocation request. Large requests may have a fee.      | No            | Area for shared data for a project, common data sets, software, results, and so on.                            |                               |
| **WORK – HDD**  | `/work/hdd`  | 1000 GB. Up to 1–100 TB by allocation request. Submit a support request.         | No            | Area for computation, largest allocations, where I/O from jobs should occur. Shared between Delta and DeltaAI. |                               |
| **WORK – NVME** | `/work/nvme` | 1000 GB. Up to 1–100 TB by allocation request; support request.                  | No            | Area for computation; NVME is best for lots of small I/O from jobs. Shared between Delta and DeltaAI.          |                               |
| **`/tmp`**      | `/tmp`       | 3.9 TB shared or dedicated depending on node usage by job(s), no quotas in place | No            | Locally attached disk for fast small file I/O.                                                                 



## 6.2 HOME Directory

- Personal, persistent space
- Good for:
  - Scripts
  - Small datasets
  - Configuration files
  - avoid putting super large data here

Example:

```bash
cd ~/   # HOME directory
```



## 6.3 PROJECT Directory

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


## 6.4 WORK Directory

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
- Jobs must specify a **time limit**
- If time expires, SLURM terminates the job
- Larger requests may wait longer in queue

---

# 7. SLURM Partitions

If you do not specify them in your batch script, SLURM will assume a 30-minute wall-clock limit and 1 GB memory per CPU core. 
| **Property**                | **Value**      |
| --------------------------- | -------------- |
| **Default Memory per core** | 1000 MB (1 GB) |
| **Default Wall-clock time** | 30 minutes     |


## 7.1 DeltaAI
You can use ```sinfo -s``` to see which partitions are currently available.
DeltaAI uses a smaller set of SLURM partitions - only 2:

| **Partition/Queue** | **Node Type** | **Max Nodes per Job** | **Max Duration** | **Max Running in Queue/user** |
| ------------------- | ------------- | --------------------- | ---------------- | ----------------------------- |
| `ghx4*`             | GPU           | TBD                   | 48 hr            | TBD                           |
| `ghx4-interactive`  | GPU           | 4                     | 2 hr             | TBD                           |

When submitting a job script to DeltaAI, include the partition name like:
```bash
#SBATCH --partition=ghx4
```

## 7.2 Delta

| **Partition/Queue**      | **Node Type** | **Max Nodes per job** | **Max Duration** | **Max Running in Queue/user** |
| ------------------------ | ------------- | --------------------- | ---------------- | ----------------------------- |
| `cpu`                    | CPU           | ALL                   | 48 hr            | TBD                           |
| `cpu-interactive`        | CPU           | 4                     | 1 hr             | TBD                           |
| `cpu-preempt`            | CPU           | ALL                   | 48 hr            | TBD                           |
| `gpuA100x4*` *(default)* | quad-A100     | ALL                   | 48 hr            | TBD                           |
| `gpuA100x4-interactive`  | quad-A100     | 4                     | 1 hr             | TBD                           |
| `gpuA100x4-preempt`      | quad-A100     | ALL                   | 48 hr            | TBD                           |
| `gpuA100x8`              | octa-A100     | ALL                   | 48 hr            | TBD                           |
| `gpuA100x8-interactive`  | octa-A100     | 2                     | 1 hr             | TBD                           |
| `gpuH200x8`              | octa-H200     | 1                     | 48 hr            | TBD                           |
| `gpuH200x8-interactive`  | octa-H200     | 1                     | 1 hr             | TBD                           |
| `gpuA40x4`               | quad-A40      | ALL                   | 48 hr            | TBD                           |
| `gpuA40x4-interactive`   | quad-A40      | 4                     | 1 hr             | TBD                           |
| `gpuA40x4-preempt`       | quad-A40      | ALL                   | 48 hr            | TBD                           |
| `gpuMI100x8`             | octa-MI100    | ALL                   | 48 hr            | TBD                           |
| `gpuMI100x8-interactive` | octa-MI100    | ALL                   | 1 hr             | TBD                           |


- The ```gpuA100x4*``` partition is shown with an asterisk in the table and is the default submission queue if no partition is explicitly requested in your SLURM script.
- Max Duration is the maximum wall-clock time allowed for jobs in that queue.
- If you want to do a quick debugging, partitions with ```Max Duration = 1h``` are recommended. 

```bash
#SBATCH --partition=gpuH200x8
#SBATCH --nodes=1
#SBATCH --cpus-per-task=4
#SBATCH --mem=16G
#SBATCH --time=01:00:00
#SBATCH --pty bash
```


# 8. 
