
## What Are Delta and DeltaAI?

Delta and DeltaAI are advanced high-performance computing (HPC) systems operated by National Center for Supercomputing Applications (NCSA) at the University of Illinois Urbana-Champaign

They are available to researchers across the United States through the ACCESS allocation program.
https://allocations.access-ci.org/login

They are designed for:

- High-performance computing (HPC)

- AI/ML model training

- GPU-accelerated research

- Large-scale simulations

## System-Level Architecture Overview

                Users (Researchers)
                       │
                 SSH / OnDemand
                       │
                ────────────────
                Login Nodes
                ────────────────
                       │
               Slurm Scheduler
                       │
       ────────────────┴────────────────
      
      │                                 │
   Delta Cluster                    DeltaAI Cluster
      │                                 │
CPU + GPU Nodes                 GH200 GPU Nodes
      │                                 │
 Shared Parallel File Systems (High-Speed Storage)




