# Awesome-Distributed-AI-On-Kubernetes

## Top Distributed AI on Kubernetes Ecosystem



**Curated List of SaaS Products & Open-Source GitHub Projects**  

*Focused on Cluster Orchestration, Distributed Training & GPU Scheduling*  

**Last updated: October 2026**



This repository tracks notable **SaaS platforms** and **open-source projects** for **Distributed AI on Kubernetes**. These tools enable organizations to run machine learning training, batch inference, and model serving across Kubernetes clusters—from managed cloud services that abstract the control plane away to open-source operators that give you full control over scheduling, fault tolerance, and resource quotas.



**Examples** include Google GKE, AWS EKS, Azure AKS, Red Hat OpenShift, Kubeflow, KubeRay, Volcano, Kueue, KServe, and Seldon Core (the category leaders).



**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, gang scheduling, and open inference infrastructure—ideal for platform engineers, ML engineers, and organizations seeking transparent, vendor-independent AI infrastructure.



Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.



## Table of Contents

- [SaaS/Hosted Platforms](#saas-hosted-platforms)

- [Open-Source GitHub Projects](#open-source-github-projects)

- [How to Contribute](#how-to-contribute)

- [Disclaimer](#disclaimer)



## SaaS/Hosted Platforms

| Platform | Company Valuation / Market Cap | Pricing (Starting Tier) | Free Tier / Trial Limits | Description | Best For |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Google GKE** | ~$4.1T (Alphabet Market Cap) | $0.10/cluster/hour (approx. $74.40/month standard control plane fee; compute billed separately) | **$74.40/month recurring credits** per billing account (covers 100% of 1 zonal Standard or Autopilot cluster control plane) + $300 90-day GCP new account trial credits | **Google Kubernetes Engine** with **GKE Autopilot** for fully managed nodes. Features **GKE Dataplane V2** (Cilium-based), **Node Auto-Provisioning**, and **GKE Sandbox** (gVisor) for workload isolation. | Teams on GCP wanting managed Kubernetes with integrated AI/ML tooling. |
| **Azure AKS** | ~$3.9T (Microsoft Market Cap) | $0.00/hour for Free cluster management tier; Standard tier starts at $0.10/cluster/hour (approx. $73/month with 99.9% uptime SLA) | **Free Forever Tier**: $0/hour control plane for clusters up to 1,000 nodes (best-effort SLA; compute billed separately) + $200 30-day Azure trial credits | **Azure Kubernetes Service** with **Kueue integration** for Ray AI workloads. Features **GPU node pools**, **Workload Identity** for credential-free access to Azure Blob Storage, and **Terraform/Helm** provisioning. | Teams on Azure wanting managed Kubernetes with Ray and Kueue for distributed AI. |
| **AWS EKS** | ~$2.8T (Amazon Market Cap) | $0.10/cluster/hour (approx. $73/month per standard cluster control plane; compute/EC2 billed separately) | **No permanent free control plane tier**; new AWS accounts receive a 6-month trial plan with **$100 sign-up credits** (up to $200 via console onboarding tasks) applicable toward EKS & EC2 compute | **Amazon Elastic Kubernetes Service** with **managed node groups**, **Fargate** for serverless pods, and **EKS Anywhere** for hybrid. **The AWS-native choice**—integrates with IAM, VPC, CloudWatch, and **EFA** for multi-node GPU communication. | Teams on AWS running distributed training with FSx for Lustre and EFA. |
| **Databricks** | ~$134B (Private Valuation) | $0.07/DBU (Genie/Light) to $0.15–$0.20/DBU for Standard Data Engineering Jobs; compute billed separately | **Free Edition (Forever Free)**: Non-commercial personal tier with daily fair-use quotas, 1 serverless SQL warehouse (2X-Small), and max 5 concurrent jobs. **Business Free Trial**: 14 days with **$400 in usage credits** | **Managed lakehouse platform** with **managed Kubernetes** under the hood. Features **MLflow integration**, **Delta Lake**, and **Unity Catalog** governance. | Teams wanting managed infrastructure without Kubernetes operational burden. |
| **Red Hat OpenShift** | ~$34B (IBM Acquisition Valuation; IBM Market Cap ~$225B) | $0.171/hour per 4 vCPUs (ROSA on-demand service fee) or $0.09/hour per 4 vCPUs (ROSA Hosted Control Plane) + infrastructure costs | **Developer Sandbox (30-day free environment, renewable)**: Up to 3 vCPU cores, 14 GB RAM, and 40 GB persistent storage. **Self-Managed 60-day free product trial** (user covers underlying cloud infrastructure) | **Enterprise Kubernetes platform** with **OpenShift AI** (built on Kubeflow) for ML workloads. Features **built-in CI/CD**, **security policies**, and **Operator Lifecycle Manager**. | Enterprises needing compliance-heavy Kubernetes with integrated MLOps. |

## Open-Source GitHub Projects



- **KubeRay**

  **Toolkit to run Ray applications on Kubernetes** (Apache-2.0) — **the Ray-native choice** . **Three custom resources**: **RayCluster** (full lifecycle management with autoscaling and fault tolerance), **RayJob** (auto-creates a RayCluster and submits a job when ready), and **RayService** (zero-downtime upgrades and high availability for Ray Serve deployments) . **Integrates with Volcano, YuniKorn, and Kueue** for queuing and gang scheduling . **Best for**: teams already invested in Ray who want Kubernetes-native Ray cluster management .



- **Volcano**

  **Cloud native batch computing system for intensive workloads** (Apache-2.0) — **the HPC-heritage scheduler** . **CNCF incubating project** extending kube-scheduler with **gang scheduling, priority, preemption, backfilling, and topology-aware scheduling** . **Supports AI frameworks** including Ray, TensorFlow, PyTorch, Spark, Flink, and Kubeflow . **Unified scheduling** for both batch and native Kubernetes workloads . **Best for**: teams coming from Slurm or running heavy distributed training with complex priority and preemption needs .



- **Kueue**

  **Kubernetes-native job queueing system** (Apache-2.0) — **the modern default for quota management** . **Three resources**: **ResourceFlavor** (hardware profile), **ClusterQueue** (quota pool), and **LocalQueue** (namespace-scoped submission point) . **Workload-level admission** provides native gang scheduling—jobs are admitted all-or-nothing based on available quota . **Integrates with Karpenter** for just-in-time node provisioning . **Best for**: most teams running distributed training who need fair quotas across teams with low adoption cost .



- **Kubeflow Training Operator**

  **Kubernetes-native project for scalable distributed training** (Apache-2.0) — **the framework-agnostic choice** . **Supports PyTorch, TensorFlow, HuggingFace, JAX, DeepSpeed, XGBoost, PaddlePaddle, and MPI** . **Python SDK** simplifies job creation for data scientists . **MPIJob support** for HPC workloads . **Best for**: MLOps-governed training clusters with multi-team job tracking and framework diversity .



- **KServe**

  **Standardized Serverless ML Inference Platform on Kubernetes** (Apache-2.0) — **the inference standard** . **Multi-node inference** with **LeaderWorkerSet (LWS)** for distributed LLM serving . **KV cache offloading** for vLLM workloads . **Confidential model serving** with TEE-based decryption . **Traffic splitting and canary rollouts** for controlled deployments . **Best for**: teams serving LLMs at scale with Kubernetes-native inference infrastructure.



- **Seldon Core**

  **Kubernetes-native model serving** (Apache-2.0) — **the pipeline-focused choice**. **Multi-step inference pipelines**, **drift detection**, **MLServer** for multi-model per GPU, and **Prometheus/ELK/Jaeger integrations**. **Best for**: teams running complex inference graphs with observability built in.



### Additional Strong Open-Source Options



- **Kubeflow Pipelines** — **Workflow orchestration for ML** (Apache-2.0) — DAG-based pipeline execution with artifact tracking and UI. **Best for**: reproducible ML pipelines on Kubernetes.

- **Katib** — **Hyperparameter tuning and neural architecture search** (Apache-2.0) — Kubernetes-native HPO with multiple search algorithms. **Best for**: automated model tuning on clusters.

- **Argo Workflows** — **Container-native workflow engine** (Apache-2.0) — DAG-based orchestration for ML pipelines with branching logic . **Best for**: pipeline-heavy workflows that need resume-from-failure.

- **Slinky** — **Run Slurm workloads on Kubernetes** (Apache-2.0) — **the migration adapter** for teams transitioning from Slurm without rewriting . **Best for**: gradual cutover from HPC to Kubernetes.

- **Flyte** — **Orchestration for AI workflows** (Apache-2.0) — Python-native, durable, reproducible workflows with native Ray integration . **Best for**: teams wanting Ray's compute with Flyte's durability and caching .

- Community **n8n** workflows for cluster alerting and training job notification.



**Frameworks for building custom systems**: Combine **KubeRay** for Ray-native workloads with **Kueue** for quota admission, **Volcano** for complex gang scheduling, **Kubeflow Training Operator** for framework-agnostic training, and **KServe** for LLM inference—creating a comprehensive Kubernetes AI stack .



## How to Contribute



1. Fork the repo.

2. Add/edit entries in `README.md` (follow existing format).

3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.

4. Submit PR with a short explanation.



Star the repo if you find it useful!



## Disclaimer



- This is a **community-curated** list — not exhaustive and not an endorsement.

- Distributed AI platforms on Kubernetes handling enterprise data must comply with data protection regulations (GDPR, CCPA, etc.) and implement appropriate access controls.

- **The "scheduler choice" matters more than the managed platform.** **Kueue + JobSet** is the modern default for most teams—Kubernetes-native, low adoption cost, native gang scheduling via workload-level admission . **Volcano** is for teams with Slurm heritage or complex priority/preemption needs—more concepts, but mature gang scheduling and topology awareness . **KubeRay** is for Ray-native teams—Ray clusters as CRDs with autoscaling . **Don't adopt Volcano for a three-service app.**

- **Ray Train wraps PyTorch DDP/FSDP.** You get PyTorch idioms with Ray's fault tolerance, elastic scaling, and checkpoint management on top—default to Ray Train unless the team explicitly prefers bare PyTorch + a Job manifest .

- **Gang scheduling prevents deadlocks.** Without it, Job A gets 4 of 8 needed GPUs while Job B gets the other 4, and neither can start. Kueue provides native gang scheduling via Workload-level admission .

- Self-hosted open-source solutions require proper cluster management, GPU provisioning, and ongoing maintenance. **Distributed systems on Kubernetes are operationally complex**—budget for platform engineering expertise regardless of scheduler choice.



---



**Made for platform engineers, ML engineers, and organizations building transparent distributed AI on Kubernetes.**  

Let's make Distributed AI on Kubernetes more open, data-driven, and scalable.
