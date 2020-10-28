[![License: CC BY-SA 4.0](https://licensebuttons.net/l/by-sa/4.0/80x15.png)](https://creativecommons.org/licenses/by-sa/4.0/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
# Certified Kubernetes Security Specialist - CKS  
**Coming soon November 2020**

Online curated resources that will help you prepare for taking the Kubernetes Certified Kubernetes Security Specialist **CKS** Certification exam.

**Disclaimer**: This is not likely a comprehensive list as the exam is not general availability **GA** yet , most likely will be a moving target with the fast pace of k8s development

- Please raise an issue, or make a pull request for fixes, new additions, or updates.

I will try to restrict the cross references of resources primarly to [kubernetes.io](kubernetes.io) as CNCF/Linux Foundation exam rules allows you search **kubernetes.io/{docs|blog}** and [kuernetes github repo](https://github.com/kubernetes) only. Youtube videos and other third party resources e.g. blogs will be provided as an optional complimentary material and any 3rd party material not allowed in the exam will be designated with :triangular_flag_on_post: in the curriculum sections below.

Ensure you have the right version of Kubernetes documentation selected (e.g. v1.19 as of 15th July announcement) especially for API objects and annotations, however for third party tools, you might find that you can still find references for them in old releases and blogs [e.g. falco install](https://github.com/kubernetes/website/issues/24184).

## Exam Objectives

These are the exam objectives you review and understand in order to pass the test.

* [CNCF Exam Curriculum repository ](https://github.com/cncf/curriculum/blob/master/CKS_Curriculum_%20v1.19%20Coming%20Soon%20November%202020.pdf)

## CKS repo topics overview

  - [ ] [Cluster Setup - 10%](#cluster-setup---10)
  - [ ] [Cluster Hardening - 15%](#cluster-hardening---15)
  - [ ] [System Hardening - 15%](#system-hardening---15)
  - [ ] [Minimize Microservice Vulnerabilities - 20%](#minimize-microservice-vulnerabilities---20)
  - [ ] [Supply Chain Security - 20%](#supply-chain-security---20)
  - [ ] [Monitoring, Logging and Runtime Security - 20%](#monitoring-logging-and-runtime-security---20)
  
  #### Extra helpful material
  
  - [ ] [Slack](#slack)
  - [ ] [Books](#books)
  - [ ] [Youtube Videos](#youtube-videos)
  - [ ] [Containers and Kubernetes Security Training](#containers-and-kubernetes-security-training)
  - [ ] [Extra Kubernetes security resources](#extra-kubernetes-security-resources)
    - [CVEs](#cves)
  - [ ] [Stargazers over time](#stargazers-over-time)

<hr style="border:3px solid blue"> </hr>
<p align="center">
  <img width="360" src="kubernetes-security-specialist-logo-300x285.png">
</p>


### Cluster Setup - 10%
:white_circle: [Securing a Cluster](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/) 

1. [Use Network security policies to restrict cluster level access](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
2. :triangular_flag_on_post: [Use CIS benchmark to review the security configuration of Kubernetes components](https://www.cisecurity.org/benchmark/kubernetes/)  (etcd, kubelet, kubedns, kubeapi)
3. Properly set up Ingress objects with security control
4. Protect node metadata and endpoints
5. [Minimize use of, and access to, GUI elements](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/#accessing-the-dashboard-ui)
6. Verify platform binaries before deploying

### Cluster Hardening - 15%

1. [Restrict access to Kubernetes API](https://kubernetes.io/docs/reference/access-authn-authz/controlling-access/)
2. [Use Role-Based Access Controls to minimize exposure](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
    * :triangular_flag_on_post: [handy site collects together articles, tools and the official documentation all in one place](https://rbac.dev/)
3. Exercise caution in using service accounts e.g. [disable defaults](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#use-the-default-service-account-to-access-the-api-server), minimize permissions on newly created ones
  
  
<details><summary> :clipboard: opt out of automounting API credentials for a service account </summary>
  
#### service account scope
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: build-robot
automountServiceAccountToken: false
```
#### pod scope
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cks-pod
spec:
  serviceAccountName: default
  automountServiceAccountToken: false

```

</details>


4. [Update Kubernetes frequently](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-upgrade/)

### System Hardening - 15%

1. Minimize host OS footprint (reduce attack surface)
2. Minimize IAM roles
3. Minimize external access to the network
4. Appropriately use kernel hardening tools such as AppArmor, seccomp
   - [AppArmor](https://kubernetes.io/docs/tutorials/clusters/apparmor/)
   - [Seccomp](https://kubernetes.io/docs/tutorials/clusters/seccomp/)


### Minimize Microservice Vulnerabilities - 20%

1. Setup appropriate OS-level security domains e.g. using PSP, OPA, security contexts
   - [Pod Security Policies](https://kubernetes.io/docs/concepts/policy/pod-security-policy/)
   - [Open Policy Agent](https://kubernetes.io/blog/2019/08/06/opa-gatekeeper-policy-and-governance-for-kubernetes/)
   - [Security Contexts](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)
2. [Manage kubernetes secrets](https://kubernetes.io/docs/concepts/configuration/secret/)
3. Use [container runtime](https://kubernetes.io/docs/concepts/containers/runtime-class/) sandboxes in multi-tenant environments (e.g. [gvisor, kata containers](https://github.com/kubernetes/enhancements/blob/5dcf841b85f49aa8290529f1957ab8bc33f8b855/keps/sig-node/585-runtime-class/README.md#examples))
4. Implement pod to pod encryption by use of mTLS

### Supply Chain Security - 20%

1. Minimize base image footprint
2. Secure your supply chain: [whitelist allowed image registries](https://kubernetes.io/blog/2019/03/21/a-guide-to-kubernetes-admission-controllers/#why-do-i-need-admission-controllers), sign and validate images
3. Use static analysis of user workloads (e.g. [kubernetes resources](https://kubernetes.io/blog/2018/07/18/11-ways-not-to-get-hacked/#7-statically-analyse-yaml), docker files)
4. [Scan images for known vulnerabilities](https://kubernetes.io/blog/2018/07/18/11-ways-not-to-get-hacked/#10-scan-images-and-run-ids)


### Monitoring, Logging and Runtime Security - 20%

1. Perform behavioural analytics of syscall process and file activities at the host and container level to detect malicious activities
2. Detect threats within a physical infrastructure, apps, networks, data, users and workloads
3. Detect all phases of attack regardless where it occurs and how it spreads
4. Perform deep analytical investigation and identification of bad actors within the environment
5. [Ensure immutability of containers at runtime](https://kubernetes.io/blog/2018/03/principles-of-container-app-design/)
6. [Use Audit Logs to monitor access](https://kubernetes.io/docs/tasks/debug-application-cluster/audit/)

### Slack
[Kubernetes Community Slack channel - #cks-exam-prep](https://kubernetes.slack.com)

### Books
1. [Aqua Security Liz Rice:Free Container Security Book](https://info.aquasec.com/container-security-book)
1. [Learn Kubernetes security: Securely orchestrate, scale, and manage your microservices in Kubernetes deployments](https://www.amazon.com/Learn-Kubernetes-Security-orchestrate-microservices/dp/1839216506)

### Youtube Videos
1. [Code in Action for the **book Learn Kubernetes Security** playlist](https://www.youtube.com/playlist?list=PLeLcvrwLe1859Rje9gHrD1KEp4y5OXApB)

### Containers and Kubernetes Security Training
1. [Andrew Martin Control Plane Security training](https://control-plane.io/training/)
1. [Linux Academy/ACloudGuru Kubernetes security](https://acloud.guru/learn/7d2c29e7-cdb2-4f44-8744-06332f47040e)
1. [Cloud native security defending containers and kubernetes](https://www.sans.org/event/stay-sharp-blue-team-ops-and-cloud-dec-2020/course/cloud-native-security-defending-containers-kubernetes)
1.[Tutorial: Getting Started With Cloud-Native Security - Liz Rice, Aqua Security & Michael Hausenblas](https://youtu.be/MisS3wSds40)
    - [hands-on tutorial](https://tutorial.kubernetes-security.info/)
1. [K21 academy CKS step by step activity hands-on-lab activity guide](https://k21academy.com/docker-kubernetes/certified-kubernetes-security-specialist-cks-step-by-step-activity-guide-hands-on-lab)
1. [Killer.sh CKS practice exam](https://killer.sh/cks)       &#x27F9; use code **walidshaari** for **20%** discount


### Extra Kubernetes security resources
1. [kubernetes-security.info](https://kubernetes-security.info/)
1. [Aquasecurity Blogs](https://blog.aquasec.com/)
1. [control-plane/Andrew Martin @sublimino: 11 ways not to get hacked](https://control-plane.io/posts/11-ways-not-to-get-hacked/)
1. [How to Train your Red Team (for Cloud-Native) - Andrew Martin, ControPlane](https://youtu.be/LJrSAPUNHvE)
1. [InGuardians/Jay Beale: Kubernetes Practical attacks and defences](https://youtu.be/LtCx3zZpOfs)
1. [Google/Ian Lewis: Kubernetes security best practices](https://youtu.be/wqsUfvRyYpw)
1. [Kubernetes Goat](https://github.com/madhuakula/kubernetes-goat)
1. [securekubernetes](https://securekubernetes.com/)
1. [Simulator: A distributed systems and infrastructure simulator for attacking and debugging Kubernetes](https://github.com/kubernetes-simulator/simulator)
1. [Kubernetes security concepts and demos](https://youtu.be/VjlvS-qiz_U)


#### CVEs
1. [CNCF Kubernetes Security Anatomy and the Recently Disclosed CVEs (CVE-2020-8555, CVE-2020-8552)](https://youtu.be/Dp1RCYCpyJk)


## Stargazers over time

[![Stargazers over time](https://starchart.cc/walidshaari/Certified-Kubernetes-Security-Specialist.svg)](https://starchart.cc/walidshaari/Certified-Kubernetes-Security-Specialist)

    
