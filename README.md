[![License: CC BY-SA 4.0](https://licensebuttons.net/l/by-sa/4.0/80x15.png)](https://creativecommons.org/licenses/by-sa/4.0/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
# Certified Kubernetes Security Specialist - CKS  
**Coming soon November 2020**

Online resources that will help you prepare for taking the Kubernetes Certified Kubernetes Security Specialist **CKS** Certification exam.

**Disclaimer**: This is not likely a comprehensive list as the exam is not out yet, most likely will be a moving target with the fast pace of k8s development

- please make a pull request if there something wrong or that should be added, or updated in here.

I will try to restrict the cross references of resources to [kubernetes.io](kubernetes.io) as CNCF/Linux Foundation exam rules allows you search **kubernetes.io** and [kuernetes github repo](https://github.com/kubernetes) only. Youtube videos and other resources e.g. blogs will be provided as an optional complimentary material.

Content is scarse, we will update as we are preparing for our **CKS exam journey**.

Ensure you have the right version of Kubernetes documentation selected (e.g. v1.19 as of 15th July announcement) especially for API objects and annotations.

## Exam Objectives

These are the exam objectives you review and understand in order to pass the test.

* [CNCF Exam Curriculum repository ](https://github.com/cncf/curriculum/blob/master/CKS_Curriculum_%20v1.19%20Coming%20Soon%20November%202020.pdf)

### 10% - [Cluster Setup](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/)

1. [Use Network security policies to restrict cluster level access](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
2. [Use CIS benchmark to review the security configuration of Kubernetes components](https://www.cisecurity.org/benchmark/kubernetes/) (etcd, kubelet, kubedns, kubeapi)
3. Properly set up Ingress objects with security control
4. Protect node metadata and endpoints
5. [Minimize use of, and access to, GUI elements](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/#accessing-the-dashboard-ui)
6. Verify platform binaries before deploying

### 15% - Cluster Hardening

1. [Restrict access to Kubernetes API](https://kubernetes.io/docs/reference/access-authn-authz/controlling-access/)
2. [Use Role Based Access Controls to minimize exposure](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
    * [handy site collects together articles, tools and the official documentation all in one place](https://rbac.dev/)
3. Exercise caution in using service accounts e.g. disable defaults, minimize permissions on newly created ones
4. Update Kubernetes frequently

### 15% - System Hardening

1. Minimize host OS footprint (reduce attack surface)
2. Minimize IAM roles
3. Minimize external access to the network
4. Appropriately use kernel hardening tools such as AppArmor, seccomp
   - [AppArmor](https://kubernetes.io/docs/tutorials/clusters/apparmor/)
   - [Seccomp](https://kubernetes.io/docs/tutorials/clusters/seccomp/)

    !? where is selinux? assume exam systems are ubuntu

### 20% - Minimize Microservice Vulnerabilities

1. Setup appropriate OS level security domains e.g. using PSP, OPA, security contexts
   - [Pod Security Policies](https://kubernetes.io/docs/concepts/policy/pod-security-policy/)
   - [Open Policy Agent](https://kubernetes.io/blog/2019/08/06/opa-gatekeeper-policy-and-governance-for-kubernetes/)
   - [Security Contexts](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)
2. [Manage kubernetes secrets](https://kubernetes.io/docs/concepts/configuration/secret/)
3. Use container runtime sandboxes in multi-tenant environments (e.g. gvisor, kata containers)
4. Implement pod to pod encryption by use of mTLS

### 20% - Supply Chain Security

1. Minimize base image footprint
2. Secure your supply chain: whitelist allowed image registries, sign and validate images
3. Use static analysis of user workloads (e.g. kubernetes resources, docker files)
4. [Scan images for known vulnerabilities](https://kubernetes.io/blog/2018/07/18/11-ways-not-to-get-hacked/#10-scan-images-and-run-ids)


### 20% - Monitoring, Logging and Runtime Security

1. Perform behavioral analytics of syscall process and file activities at the host and container level to detect malicious activities
2. Detect threats within physical infrastructure, apps, networks, data, users and workloads
3. Detect all phases of attack regardless where it occurs and how it spreads
4. Perform deep analytical investigation and identification of bad actors within environment
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
1.[Tutorial: Getting Started With Cloud Native Security - Liz Rice, Aqua Security & Michael Hausenblas](https://youtu.be/MisS3wSds40)
    - [hands-on tutorial](https://tutorial.kubernetes-security.info/)
1. [K21 academy CKS step by step activity hands-on-lab activity guide](https://k21academy.com/docker-kubernetes/certified-kubernetes-security-specialist-cks-step-by-step-activity-guide-hands-on-lab)
1. [Killer.sh CKS practice exam](https://killer.sh/cks)       &#x27F9; use code **walidshaari** for **20%** discount


### Extra Kubernetes security resources
1. [kubernetes-security.info](https://kubernetes-security.info/)
1. [Aquasecurity Blogs](https://blog.aquasec.com/)
1. [control-plane/Andrew Martin @sublimino: 11 ways not to get hacked](https://control-plane.io/posts/11-ways-not-to-get-hacked/)
1. [How to Train your Red Team (for Cloud Native) - Andrew Martin, ControPlane](https://youtu.be/LJrSAPUNHvE)
1. [InGuardians/Jay Beale: Kubernetes Practical attacks and defenses](https://youtu.be/LtCx3zZpOfs)
1. [Google/Ian Lewis : Kubernetes security best practices](https://youtu.be/wqsUfvRyYpw)
1. [Kubernetes Goat](https://github.com/madhuakula/kubernetes-goat)
1. [securekubernetes](https://securekubernetes.com/)
1. [Simulator: A distributed systems and infrastructure simulator for attacking and debugging Kubernetes](https://github.com/kubernetes-simulator/simulator)
1. [Kubernetes security concepts and demos](https://youtu.be/VjlvS-qiz_U)


#### CVEs
1. [CNCF Kubernetes Security Anatomy and the Recently Disclosed CVEs (CVE-2020-8555, CVE-2020-8552)](https://youtu.be/Dp1RCYCpyJk)


## Stargazers over time

[![Stargazers over time](https://starchart.cc/walidshaari/Certified-Kubernetes-Security-Specialist.svg)](https://starchart.cc/walidshaari/Certified-Kubernetes-Security-Specialist)
