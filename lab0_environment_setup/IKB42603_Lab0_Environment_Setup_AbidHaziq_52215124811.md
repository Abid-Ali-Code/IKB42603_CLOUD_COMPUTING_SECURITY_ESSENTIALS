# IKB42603 Cloud Computing Security Essentials
## Lab 0 — Lab Environment Setup

> **Docker · AWS CLI · Kubernetes (kind) · kubectl · Helper Tools · LocalStack**

---

## Student Information

| Item | Details |
|---|---|
| **Student Name** | Muhammad Abid Haziq Bin Muhammad Ali |
| **Student ID** | 52215124811 |
| **Module Code** | IKB42603 |
| **Module Name** | Cloud Computing Security Essentials |
| **Lab** | Lab 0 — Lab Environment Setup |
| **Institution** | Universiti Kuala Lumpur Malaysian Institute of Information Technology (UniKL MIIT) |
| **Lecturer** | Prof. Dr. Shahrulniza Musa |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Setup Objectives](#2-setup-objectives)
3. [Environment and Tools](#3-environment-and-tools)
4. [Docker Verification](#4-docker-verification)
5. [AWS CLI Verification](#5-aws-cli-verification)
6. [kind and kubectl Verification](#6-kind-and-kubectl-verification)
7. [Helper Tool Verification](#7-helper-tool-verification)
8. [LocalStack and AWS CLI Connectivity](#8-localstack-and-aws-cli-connectivity)
9. [Kubernetes Cluster Verification](#9-kubernetes-cluster-verification)
10. [Pre-Lab Verification Checklist](#10-pre-lab-verification-checklist)
11. [Security and Operational Notes](#11-security-and-operational-notes)
12. [Conclusion](#12-conclusion)
13. [References](#13-references)

---

# 1. Introduction

Lab 0 prepares the local environment required for the upcoming **IKB42603 Cloud Computing Security Essentials** practical labs. The setup is designed to run locally on the student's machine so that cloud security exercises can be performed without requiring a real public-cloud account.

The environment uses **Docker** to run containers, **LocalStack** to emulate AWS services locally, **AWS CLI v2** to interact with the simulated AWS environment, and **kind** together with **kubectl** to create and manage a local Kubernetes cluster.

The setup cheatsheet also identifies helper tools such as **OpenSSL**, **oathtool**, and **Trivy** for later labs. This report documents the setup evidence available from the supplied Kali Linux screenshots and connects each screenshot to the relevant Lab 0 verification requirement.

> **Evidence Scope:** This report intentionally uses only the screenshots supplied for the current Lab 0 submission. Where a command is required by the cheatsheet but no screenshot was supplied, the report states this rather than inventing evidence.

---

# 2. Setup Objectives

The objectives of Lab 0 are to prepare and verify the tools needed before Lab 1:

- Verify that Docker can successfully run containers.
- Confirm that AWS CLI v2 is installed.
- Confirm that `kind` and `kubectl` are available.
- Verify relevant helper tools such as OpenSSL.
- Configure the AWS CLI to communicate with LocalStack instead of a real AWS account.
- Verify LocalStack connectivity using AWS STS.
- Create a local Kubernetes cluster using kind.
- Confirm that the Kubernetes control-plane node reaches the `Ready` state.
- Ensure the local environment is usable for later cloud security labs.

---

# 3. Environment and Tools

The Lab 0 setup cheatsheet identifies the following tools:

| Tool | Purpose | Use in Module |
|---|---|---|
| **Docker** | Runs containers and the LocalStack cloud simulator | All labs |
| **AWS CLI v2** | Sends AWS-compatible commands to LocalStack | Labs 1, 3 and 5 |
| **kind** | Runs a local Kubernetes cluster inside Docker | Labs 1, 2 and 4 |
| **kubectl** | Controls and queries the Kubernetes cluster | Labs 1, 2 and 4 |
| **OpenSSL** | Provides encryption, key and certificate utilities | Lab 3 |
| **oathtool** | Generates MFA/TOTP codes | Lab 4 |
| **Trivy** | Scans container images for vulnerabilities through Docker | Lab 4 |

The screenshots show the work being carried out inside **Kali Linux**, which provides a Bash-compatible command-line environment suitable for the lab commands.

---

# 4. Docker Verification

The Lab 0 cheatsheet requires Docker to be verified using both the version command and the `hello-world` container test.

## 4.1 Docker Version

```bash
docker --version
```

![Docker Version Verification](images/01_docker_version.png)

*Figure 1: Docker version verification showing Docker version `28.5.2+dfsg4`.*

The evidence confirms:

```text
Docker version 28.5.2+dfsg4
```

This verifies that Docker is installed and accessible from the Kali Linux terminal.

## 4.2 Docker Functional Test

The functional test was then performed using:

```bash
docker run --rm hello-world
```

![Docker Hello World Verification](images/02_docker_hello_world.png)

*Figure 2: Successful execution of Docker's `hello-world` container. The `Hello from Docker!` message confirms that the Docker client communicated with the Docker daemon, pulled the image, created the container and returned its output.*

Together, these two pieces of evidence show that Docker is both installed and operational.

---

# 5. AWS CLI Verification

AWS CLI v2 is required to send AWS-compatible commands to LocalStack.

The verification command is:

```bash
aws --version
```

![AWS CLI Version](images/03_aws_cli_version.png)

*Figure 3: AWS CLI version verification showing `aws-cli/2.36.8` running under Python 3.14.6 on Kali Linux.*

The supplied evidence shows:

```text
aws-cli/2.36.8
Python/3.14.6
Linux/6.16.8+kali-amd64
```

This confirms that the installed AWS command-line client is version 2.x, which satisfies the Lab 0 requirement.

---

# 6. kind and kubectl Verification

The Kubernetes tools are verified using:

```bash
kind --version
kubectl version --client
```

![kind and kubectl Versions](images/04_kind_kubectl_versions.png)

*Figure 4: Verification of `kind` and `kubectl`. The screenshot shows kind version `0.23.0`, kubectl client version `v1.33.4`, and Kustomize version `v5.5.0`.*

The observed versions are:

| Component | Version |
|---|---|
| **kind** | 0.23.0 |
| **kubectl Client** | v1.33.4 |
| **Kustomize** | v5.5.0 |

This confirms that both Kubernetes command-line components required by the lab are available.

---

# 7. Helper Tool Verification

The Lab 0 cheatsheet lists OpenSSL, oathtool and Trivy as helper tools for later practical work.

## 7.1 OpenSSL

OpenSSL is checked using:

```bash
openssl version
```

![OpenSSL Version](images/05_openssl_version.png)

*Figure 5: OpenSSL version verification showing OpenSSL `3.5.3` dated 16 September 2025.*

The screenshot confirms:

```text
OpenSSL 3.5.3 16 Sep 2025
```

This verifies that OpenSSL is available for later encryption, key and certificate exercises.

## 7.2 oathtool and Trivy

The current screenshot set does not include separate evidence for `oathtool --version`.

The cheatsheet notes that `oathtool` is used for **Lab 4** and that **Trivy does not require a separate installation**, because it is executed through Docker when needed.

Therefore, no unsupported installation result is claimed for these two tools in this report.

---

# 8. LocalStack and AWS CLI Connectivity

The Lab 0 environment uses **LocalStack** as a local AWS-compatible endpoint. The cheatsheet requires LocalStack to be running and responding on port `4566` before AWS CLI commands are tested against it.

## 8.1 LocalStack Health Check

The LocalStack health endpoint was checked with:

```bash
curl http://localhost:4566/_localstack/health
```

![LocalStack Health Check](images/06_localstack_health.png)

*Figure 6: Output from the LocalStack health endpoint. The response lists the available simulated AWS services and confirms that the LocalStack API is responding locally.*

The screenshot shows the health response from:

```text
http://localhost:4566/_localstack/health
```

and identifies the LocalStack version as:

```text
2026.7.0
```

This confirms that the LocalStack service was reachable from the local machine.

## 8.2 LocalStack Container Status

Docker was then queried to confirm that the LocalStack container was actually running:

```bash
docker ps
```

![LocalStack Docker Container Status](images/07_localstack_container_status.png)

*Figure 7: `docker ps` output showing the LocalStack container running with a `healthy` status and the LocalStack gateway mapped to local port `4566`.*

The screenshot shows the LocalStack container in an **Up / healthy** state. It also confirms the port mapping that exposes the LocalStack gateway through:

```text
127.0.0.1:4566 -> 4566/tcp
```

This supports the health-check evidence by showing both the API response and the underlying Docker container state.

## 8.3 AWS CLI Configuration and STS Test

The cheatsheet specifies dummy AWS credentials and the following endpoint variable:

```bash
aws configure set aws_access_key_id test
aws configure set aws_secret_access_key test
aws configure set region us-east-1

EP='--endpoint-url=http://localhost:4566'
```

Connectivity is then tested with:

```bash
aws $EP sts get-caller-identity
```

![LocalStack STS Caller Identity](images/08_localstack_sts_identity.png)

*Figure 8: Successful AWS STS `get-caller-identity` request using the LocalStack endpoint on `localhost:4566`.*

The evidence shows the endpoint variable:

```text
--endpoint-url=http://localhost:4566
```

and a successful identity response containing:

```text
UserId: AKIAIOSFODNN7EXAMPLE
Account: 000000000000
Arn: arn:aws:iam::000000000000:root
```

This confirms that the AWS CLI was successfully communicating with the LocalStack AWS-compatible API.

> **Important:** The identity shown here belongs to the LocalStack simulation. It is not evidence of access to a real AWS cloud account.

---

# 9. Kubernetes Cluster Verification

The Lab 0 cheatsheet requires a local Kubernetes cluster to be created using kind:

```bash
kind create cluster --name ccse
```

The cluster is then checked using:

```bash
kubectl cluster-info --context kind-ccse
kubectl get nodes
```

![Kubernetes Cluster Verification](images/09_kubernetes_cluster_verification.png)

*Figure 9: Creation and verification of the `ccse` kind cluster. The Kubernetes control plane and CoreDNS endpoint are shown as running, while `kubectl get nodes` reports `ccse-control-plane` in the `Ready` state.*

The screenshot demonstrates the complete cluster lifecycle used in the setup exercise:

1. `kind create cluster --name ccse`
2. kind prepares the node and installs the required cluster components.
3. The kubectl context is set to `kind-ccse`.
4. `kubectl cluster-info --context kind-ccse` confirms the control plane is running.
5. `kubectl get nodes` reports the control-plane node as `Ready`.
6. `kind delete cluster --name ccse` removes the temporary cluster after verification.

The important node result is:

```text
NAME                 STATUS   ROLES           VERSION
ccse-control-plane   Ready    control-plane   v1.30.0
```

This confirms that the Kubernetes environment was successfully created and became operational before being cleaned up.

---

# 10. Pre-Lab Verification Checklist

The Lab 0 cheatsheet provides a checklist that should be completed before beginning Lab 1.

Based strictly on the supplied screenshots:

| Verification Requirement | Status | Evidence |
|---|:---:|---|
| `docker run --rm hello-world` works | ✅ | Figure 2 |
| `docker --version` prints a version | ✅ | Figure 1 — Docker 28.5.2+dfsg4 |
| `aws --version` prints AWS CLI 2.x | ✅ | Figure 3 — AWS CLI 2.36.8 |
| `kind --version` works | ✅ | Figure 4 — kind 0.23.0 |
| `kubectl version --client` works | ✅ | Figure 4 — kubectl v1.33.4 |
| OpenSSL is available | ✅ | Figure 5 — OpenSSL 3.5.3 |
| LocalStack AWS endpoint responds | ✅ | Figures 6–8 — health response, healthy container and successful STS response |
| `curl .../_localstack/health` responds | ✅ | Figure 6 — LocalStack health response |
| `aws $EP sts get-caller-identity` returns an identity | ✅ | Figure 8 |
| `kind create cluster` succeeds | ✅ | Figure 9 |
| `kubectl get nodes` shows a node | ✅ | Figure 9 |
| Kubernetes node reaches `Ready` state | ✅ | Figure 9 |
| `oathtool --version` evidence | ➖ | Not supplied; tool is identified for Lab 4 |
| Windows Git Bash/WSL requirement | N/A | Environment shown is Kali Linux |

### Overall Verification

The core environment required to begin the cloud and Kubernetes labs is demonstrated as functional:

```text
Docker installation/version       → PASS
Docker container execution          → PASS
AWS CLI v2                          → PASS
kind                                → PASS
kubectl                             → PASS
OpenSSL                             → PASS
LocalStack health endpoint          → PASS
LocalStack Docker container status  → PASS
LocalStack AWS API connectivity     → PASS
Kubernetes cluster creation         → PASS
Kubernetes node readiness           → PASS
```

The newly added evidence completes the previously missing Docker version and LocalStack health verification steps.

---

# 11. Security and Operational Notes

## 11.1 Local Environment Instead of Real AWS

The Lab 0 design uses LocalStack so that AWS-style commands can be tested against:

```text
http://localhost:4566
```

This avoids requiring a real AWS account for the practical setup.

## 11.2 Dummy AWS Credentials

The cheatsheet specifies dummy credentials:

```text
Access key: test
Secret key: test
Region: us-east-1
```

These values are intended for LocalStack. Real cloud access keys should never be committed to source-code repositories or screenshots.

## 11.3 Docker as the Local Runtime

Docker provides the underlying container runtime for both LocalStack and kind. The successful `hello-world` output is therefore an important early verification because later exercises depend on the Docker daemon working correctly.

## 11.4 Temporary Kubernetes Cluster

The cluster is intentionally disposable. After successful verification, the screenshot shows:

```bash
kind delete cluster --name ccse
```

Removing the temporary cluster after use helps keep the local environment clean and demonstrates that the lab infrastructure can be recreated when required.

## 11.5 Useful Troubleshooting Areas

The setup cheatsheet highlights common issues that may affect later labs:

- Docker daemon not running.
- Hardware virtualization not enabled.
- Port `4566` already being used.
- LocalStack endpoint unavailable.
- AWS CLI or kubectl missing from `PATH`.
- Insufficient Docker memory for kind.
- System clock issues affecting MFA/TOTP in later work.

These checks are useful because most later lab tasks depend on the Lab 0 environment being configured correctly.

---

# 12. Conclusion

Lab 0 established the local environment required for the IKB42603 Cloud Computing Security Essentials practical work.

The supplied evidence demonstrates that Docker version `28.5.2+dfsg4` is installed and can successfully run a container. AWS CLI v2, kind, kubectl and OpenSSL are also available. LocalStack was verified through its health endpoint, its healthy Docker container status, and a successful AWS STS caller identity request.

A Kubernetes cluster named `ccse` was then created with kind. The control plane started successfully, `kubectl` was able to communicate with the cluster, and the `ccse-control-plane` node reached the `Ready` state before the temporary cluster was deleted.

Overall, the available evidence now confirms the key Docker, LocalStack, AWS CLI and Kubernetes setup checks required by the Lab 0 cheatsheet. The environment is ready for the upcoming cloud security labs.

---

# 13. References

1. **IKB42603 Cloud Computing Security Essentials — Lab 0 Setup Cheatsheet: Lab Environment Setup.** UniKL MIIT, Prof. Dr. Shahrulniza Musa.

2. **Docker Documentation**  
   https://docs.docker.com/

3. **AWS CLI Documentation**  
   https://docs.aws.amazon.com/cli/

4. **LocalStack Documentation**  
   https://docs.localstack.cloud/

5. **kind Documentation**  
   https://kind.sigs.k8s.io/

6. **Kubernetes kubectl Documentation**  
   https://kubernetes.io/docs/reference/kubectl/

---

## Repository Structure

```text
IKB42603_Lab0_GitHub_Ready/
├── README.md
├── .gitignore
└── images/
    ├── 01_docker_version.png
    ├── 02_docker_hello_world.png
    ├── 03_aws_cli_version.png
    ├── 04_kind_kubectl_versions.png
    ├── 05_openssl_version.png
    ├── 06_localstack_health.png
    ├── 07_localstack_container_status.png
    ├── 08_localstack_sts_identity.png
    └── 09_kubernetes_cluster_verification.png
```
