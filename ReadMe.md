# Consulting Engagement Report

## ABG - OpenShift Container Platform 4.20.23 - Cluster1

**Version:** 2.1

**Copyright:** © 2026 Red Hat, Inc. All Rights Reserved.

---

## 1. Preface

### 1.1. Confidentiality, Copyright, and Disclaimer

This is a customer-facing document between Red Hat, Inc. and ABG ("Client"). Copyright © 2026 Red Hat, Inc. All Rights Reserved. No part of the work covered by the copyright herein may be reproduced or used in any form or by any means graphic, electronic, or mechanical, including photocopying, recording, taping, or information storage and retrieval systems without permission in writing from Red Hat.

This document is not a quote and does not include any binding commitments by Red Hat. If acceptable, a formal quote can be issued upon request, which will include the scope of work, cost, and any customer requirements as necessary.

This Consulting Engagement Report (CER) contains both Red Hat Confidential Information and Client Confidential Information subject to the confidentiality terms of the agreement governing the Services provided by Red Hat.

### 1.2. Audience

This document is intended for Client technical staff responsible for the environment.

### 1.3. Additional Background and Related Documents

This document does not contain step-by-step details of installation or other tasks, as they are covered in the relevant documentation on [Red Hat Customer Portal](http://access.redhat.com/). Links to the appropriate documents will be made when required.

### 1.4. Scripts and Playbooks

Any scripts provided are being provided as-is, without any form of support or warranty. All provided scripts can be modified by the customer at will.

### 1.5. Customer Satisfaction Survey (CSat)

Red Hat is committed to a quality customer experience and continuous improvement in our services. Your feedback is the most important factor in determining if we've met your expectations and what we can do to improve. You will be receiving a customer satisfaction survey at the conclusion of our engagement. Please take just a few minutes to provide us with an honest snapshot of your experience.

In the meantime, if there are any areas of concern, issues or problems on the project, please don't hesitate to reach out to Shailendra Hedaoo.

---

## 2. Project Information

* **Originator:** Red Hat Consulting 

* **Owner:** Red Hat Services 


### 2.3. Document Conventions

#### 2.3.1. Admonitions and Call-Outs

* ℹ️ Additional detail about a topic will be called out with the "info" symbol.

* 💡 Tips and advice will appear with a "lightbulb" admonition.

* ⚠️ Warnings and strong recommendations will appear next to a caution exclamation.

* 🛑 Crucial advice and information will appear next to a red exclamation.



#### 2.3.2. Single-line Commands and Code

If instructed to type a single command, it will be displayed in a monospace font and highlighted like this example:
`ipa-vvv cert-find --all` 

#### 2.3.3. Multi-line Commands, Code / File Contents

If instructed to type multi-line commands, create or modify code blocks and/or file contents, the information will be monospaced and placed in a callout box:

```ruby
require 'sinatra'
get '/hi' do
  "Hello World!"
end

```

### 2.4. Additional Copies

To request additional copies of this Consulting Engagement Report, please contact the Red Hat Project Manager identified in Participants of the Engagement section or your current Red Hat account team.

### 2.5. Participants of the Engagement
It looks like you are working on formatting the tables for the participants section. Here are the clean, properly formatted Markdown tables for both **Red Hat** and **ABG** without the extraneous line breaks inside the cells:

#### 2.5.1. Red Hat

| Name | Role | E-mail address |
| --- | --- | --- |
| Misha Joshi | Sr. Director, Services | mijoshi@redhat.com |
| Sushil More | Director, Services | sumore@redhat.com |
| Anupam Arora | Consulting Services | anuarora@redhat.com |
| Shailendra Hedaoo | Project Manager | shhedaoo@redhat.com |
| Jatan Malde | Sr. Consultant | jmalde@redhat.com |
| Sandeep Anuragi | Sr. Consultant | sanuragi@redhat.com |
| Vaibhav Shelke | Consultant | vshelke@redhat.com |

#### 2.5.2. ABG

| Name | Role | Company | E-mail address |
| --- | --- | --- | --- |
| Deepak Dubey | Infrastructure Director | Aditya Birla Capital | deepak.dubey@adityabirlacapital.com |
| Sandesh Saval | Project Manager | Aditya Birla Capital | sandesh.saval@adityabirlacapital.com |
| Manish Patel | Sr. Technology Architect | Aditya Birla Capital | manish.patel@adityabirlacapital.com |
| Dinesh Rane | Principal Technology Architect | Aditya Birla Capital | dinesh.rane1-v@adityabirlacapital.com |
| Shared Service DCO | Sr. Technology Architect | Aditya Birla Capital | sharedservices.dco@adityabirlacapital.com |
| Pratap Sawant | Project Manager | Aditya Birla Capital | pratap.sawant-v@adityabirlacapital.com |

---

## 3. Executive Summary

Red Hat Consulting was engaged by ABG to assist in the implementation of Red Hat OpenShift Container Platform 4.20 for the Production Environment.

---

## 4. Overview

### 4.1. About Aditya Birla Group

Aditya Birla Group is an Indian multinational conglomerate headquartered in Mumbai. The group's business interests include metals, cement, fashion and retail, financial services, renewables, fibre, textiles, chemicals, real estate, trading, mining, and entertainment. Red Hat Consulting was engaged by ABG to collaborate for their OpenShift 4 cluster deployment and Roadmap to meet the above needs.

### 4.2. Purpose and Engagement Approach

> ℹ️ This design includes six Red Hat OpenShift Container Platform (OCP) 4.20 clusters deployed using a combination of Connected UPI Bare Metal, ACM Assisted Installer, and Hosted Control Plane (HCP) architectures.
> 
> 

The environment consists of both physical bare-metal servers and virtual machine-based worker nodes, with cluster lifecycle management provided through Red Hat Advanced Cluster Management (ACM). Connectivity is established through enterprise proxy services, F5 load balancers, and dedicated API and Ingress VIPs for each cluster.

#### 4.2.1. Business & Technical Objectives for Aditya Birla Group

* Deploy and manage six Red Hat OpenShift Container Platform (OCP) 4.20 clusters supporting multiple deployment architectures, including Connected UPI Bare Metal, ACM Assisted Installer, and Hosted Control Planes (HCP).


* Establish a centralized cluster management platform using Red Hat Advanced Cluster Management (ACM) to simplify cluster provisioning, governance, lifecycle management, and observability.


* Improve application testing, validation, and production rollout processes through standardized OpenShift platforms across development, testing, and production environments.


* Enable scalable microservices-based application architectures with improved performance, resiliency, and operational efficiency.


* Provide high availability through dedicated F5 Load Balancer VIPs for API and Ingress endpoints across all clusters.


* Support both bare-metal and virtualized workloads, including Linux and Windows virtual machine hosting capabilities.


* Establish a disaster recovery (DR) OpenShift environment to improve business continuity and operational resilience.


* Enable future adoption of cloud-native, virtualization, and edge computing workloads through a consistent OpenShift platform strategy.



#### 4.2.1.1. Cluster Design Summary

| Cluster | Version | Deployment Type | Purpose |
| --- | --- | --- | --- |
| **cluster1** | 4.20 | Connected UPI Bare Metal (OKE) | Primary OpenShift Cluster |
| **cluster2** | 4.20 | ACM Assisted HCP Management Cluster | Centralized Management Cluster |
| **cluster3** | 4.20 | ACM Assisted Bare Metal Windows VM Cluster | Windows Virtualization Workloads |
| **cluster4** | 4.20 | ACM Assisted Bare Metal Linux VM Cluster | Linux Virtualization Workloads |
| **cluster5** | 4.20 | Hosted Control Plane (HCP) Managed Cluster on VMs | Hosted Control Plane Workloads |
| **cluster6** | 4.20 | Connected UPI Bare Metal (OKE DR) | Disaster Recovery Cluster |

#### 4.2.1.2. Design Considerations

* Red Hat OpenShift Container Platform 4.20 is the selected version for deployment across all six clusters.
* F5 Load Balancer will provide dedicated API and Ingress VIPs for each cluster.
* For cluster5 (Hosted Control Plane), MetalLB may be used to host the API VIP if the primary API VIP configuration is not available. The required IP address will be allocated from the cluster2 routable network.
* Cluster names, DNS domains, API VIPs, Ingress VIPs, and networking details will be documented in dedicated prerequisite worksheets for each cluster.
* A dedicated bastion host VM will be provisioned for cluster1, while a shared bastion host will be used for cluster3 and cluster4.
* Cluster6 will serve as the disaster recovery (DR) environment for business continuity and resiliency requirements.



---

## 5. Implementation Details

### 5.1. Deployed Architecture

Architecture and design for Aditya Birla Group is covered in the detailed design document (LLD) and should be referenced before proceeding further.

#### 5.1.3. Environment Setup

Steps to prepare or create the environment for the proposed architecture. This setup includes configuration for the production setup (`abfstclospcls1`). The only change with the production OpenShift setup includes the configuration of 3 master nodes which is a compact cluster. To collect network, DNS, load balancer, etc. configuration, refer to the `*ABG OCP - Pre req_Staging_v1.xlsx` file.

Other OpenShift setups documented in the prerequisites file are:

* cluster2 (`abfstclospcls2`)
* cluster3 (`abfstclospcls3`)
* cluster4 (`abfstclospcls4`)
* cluster5 (`abfstclospcls5`)
* cluster6 (`abfstclospcls6`)

#### 5.1.3.1. Network Information

| Name | IP Address Pool | Comments |
| --- | --- | --- |
| **Cluster Network** | 192.170.0.0/16 | Non Routable |
| **Service Network** | 192.176.0.0/20 | Non Routable |
| **Host Network** | 10.21.134.0/24 | Routable  |

#### 5.1.3.2. Network Services

| Services | Host | Comments |
| --- | --- | --- |
| **DNS Server** | 10.158.5.88, 10.158.5.89, 10.120.5.127 | Nameserver IP for OCP nodes. |
| **DHCP Server** | N/A | Static IPs will be used for OCP nodes. |

#### 5.1.3.3. Load Balancer Config Details

| VIP | URL | Port | Type |
| --- | --- | --- | --- |
| 10.21.134.16 | api.abfstclospcls1.bsli.com | 6443, 22623 | Passthrough (layer 4 routing)  |
| 10.21.134.15 | api-int.abfstclospcls1.bsli.com | 6443, 22623 | Passthrough (layer 4 routing) |
| 10.21.134.14 | *.apps.abfstclospcls1.bsli.com | 443, 80 | Passthrough (layer 4 routing)  |

#### 5.1.3.4. Internet Access

The RHOCP-4.20.23 is a connected mode implementation where internet access is provided via proxy on the OpenShift cluster.

#### 5.1.3.5. Node Information

| Server FQDN | IP | Role | Subs Used | OS |
| --- | --- | --- | --- | --- |
| abfstclospc1n1.abfstclospcls1.bsli.com | 10.21.134.17 | control plane, master, worker  | N/A | RHCOS |
| abfstclospc1n2.abfstclospcls1.bsli.com | 10.21.134.18 | control plane, master, worker  | N/A | RHCOS |
| abfstclospc1n3.abfstclospcls1.bsli.com | 10.21.134.19 | control plane, master, worker  | N/A | RHCOS |

#### 5.1.3.6. Storage Information

| Application | Storage Type | CSI Driver | Mount Path | Size |
| --- | --- | --- | --- | --- |
| **Internal Registry** | File Object (S3 compatible) | Internal Image Registry | - | 100Gi |
| **Monitoring Prometheus** | Block | Dell CSI | prometheus | 200 GB (100x2) |
| **Monitoring Alert Manager** | Block | Dell CSI | user-prometheus-0 | 20 GB (10x2) |
| **LokiStack** | Block | Dell CSI | Compactor | 250 GB |
| **Logging** | Object (S3 compatible) | Dell Isilon Object | - | 200GB  |
| **ETCD Backup** | External storage (any) | Backup NFS | - | 200GB |
| **ACM** | Block | Dell CSI | alertmanager | 200GB |
| **ACM** | Block | Dell CSI | thanos-compact | 200GB  |
| **ACM** | Block | Dell CSI | thanos-receivey | 200GB  |
| **ACM** | Block | Dell CSI | thanos-rule | 200GB |
| **ACM** | Block | Dell CSI | thanos-store | 200GB |
| **ACM** | Block | Dell CSI | redis | 200GB  |
| **ACM** | Object (S3 compatible) | Dell CSI | Observability | 200GB  |

#### 5.1.3.7. Certificates

Aditya Birla Group has planned to use self-signed certificates by their internal CA for Wild Card (`*.apps`) Domain Ingress Controller.

---

### 5.2. Technical Implementation

### 5.2.1. Configure Bastion Node

#### 5.2.1.1. Operating System Details

```bash
[root@ABFSTCLBSTNPA1 ~]# cat /etc/redhat-release
Red Hat Enterprise Linux 9.6 (Plow)

```

#### 5.2.1.2. Block Device (Hard Disk) Details

Checking Disk Free details:

```bash
[root@ABFSTCLBSTNPA1 ~]# df -h
Filesystem                    Size  Used Avail Use% Mounted on
devtmpfs                      4.0M     0  4.0M   0% /dev
tmpfs                         7.7G   84K  7.7G   1% /dev/shm
tmpfs                         3.1G   18M  3.1G   1% /run
/dev/mapper/osvg-rootlv        30G  5.9G   25G  20% /
/dev/mapper/osvg-usrlv         20G  5.2G   15G  26% /usr
/dev/sdb2                     2.0G  372M  1.6G  19% /boot
/dev/mapper/osvg-opt           20G  1.4G   19G   7% /opt
/dev/mapper/osvg-tmplv         10G  104M  9.9G   2% /tmp
/dev/mapper/osvg-varlv         10G  3.9G  6.2G  39% /var
/dev/mapper/osvg-homelv        20G  724M   20G   4% /home
/dev/mapper/osvg-varloglv      10G  491M  9.5G   5% /var/log
/dev/mapper/osvg-varauditlv   5.0G   70M  4.9G   2% /var/log/audit
tmpfs                         1.6G   52K  1.6G   1% /run/user/42
/dev/mapper/datavg-datalv     150G  1.1G  149G   1% /data
tmpfs                         1.6G   40K  1.6G   1% /run/user/0
/dev/sr0                       12G   12G     0 100% /mnt

```

Listing disks:

```bash
[root@ABFSTCLBSTNPA1 ~]# lsblk
NAME                    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                       8:0    0  150G  0 disk 
└─datavg-datalv         253:9    0  150G  0 lvm  /data
sdb                       8:16   0  150G  0 disk 
├─sdb1                  8:17   0    2M  0 part 
├─sdb2                  8:18   0    2G  0 part /boot
└─sdb3                  8:19   0  141G  0 part 
  ├─osvg-rootlv         253:0    0   30G  0 lvm  /
  ├─osvg-swaplv         253:1    0   16G  0 lvm  [SWAP]
  ├─osvg-usrlv          253:2    0   20G  0 lvm  /usr
  ├─osvg-tmplv          253:3    0   10G  0 lvm  /tmp
  ├─osvg-varlv          253:4    0   10G  0 lvm  /opt/sentinelone/rpm_mount
  │                                              /var
  ├─osvg-homelv         253:5    0   20G  0 lvm  /home
  ├─osvg-varloglv       253:6    0   10G  0 lvm  /var/log
  ├─osvg-varauditlv     253:7    0    5G  0 lvm  /var/log/audit
  └─osvg-opt            253:8    0   20G  0 lvm  /opt
sr0                      11:0    1 11.9G  0 rom  /mnt

```

Checking hostname and DNS configuration:

```bash
[root@ABFSTCLBSTNPA1 ~]# hostname
ABFSTCLBSTNPA1

[root@ABFSTCLBSTNPA1 ~]# cat /etc/resolv.conf
# Generated by NetworkManager
nameserver 10.158.5.88
nameserver 10.158.5.89
nameserver 10.120.5.127

```

#### 5.2.1.3. Route and Default Gateway Details

```bash
[root@ABFSTCLBSTNPA1 ~]# ip r
default via 10.21.6.1 dev eth0 proto static metric 100 
10.21.6.0/24 dev eth0 proto kernel scope link src 10.21.6.95 metric 100 

[root@ABFSTCLBSTNPA1 ~]# ip -br a
lo               UNKNOWN        127.0.0.1/8 ::1/128 
eth0             UP             10.21.6.95/24 

```

#### 5.2.1.4. Enabling Yum Repositories

The Aditya Birla Group Team created a KVM with RHEL 9.4 with GUI install registered with the Red Hat CDN network via proxy.

```bash
[root@ABFSTCLBSTNPA1 ~]# yum repolist
Updating Subscription Management repositories.
repo id                          repo name
rhel-9-for-x86_64-appstream-rpms Red Hat Enterprise Linux 9 for x86_64 - AppStream (RPMs)
rhel-9-for-x86_64-baseos-rpms    Red Hat Enterprise Linux 9 for x86_64 - BaseOS (RPMs)

```

#### 5.2.1.5. Checking OCP Binary Version

```bash
[root@ABFSTCLBSTNPA1 Downloads]# oc version
Client Version: 4.20.23
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3

[root@ABFSTCLBSTNPA1 Downloads]# openshift-install version
openshift-install 4.20.23
built from commit 9598d638ef8acb62cb963b3a944a8bdced3840f3
release image quay.io/openshift-release-dev/ocp-release@sha256:7aacace57ab6ec468dd98b0b3e0f3fc440b29afce21b90bd716fed0db487e9e9
release architecture amd64

```

#### 5.2.1.6. Checking DNS Records

```bash
[root@ABFSTCLBSTNPA1 ~]# for a in 10.21.134.{17..19}; do dig -x $a +short ; done
abfstclospc1n1.abfstclospcls1.bsli.com.
abfstclospc1n2.abfstclospcls1.bsli.com.
abfstclospc1n3.abfstclospcls1.bsli.com.

[root@ABFSTCLBSTNPA1 ~]# for a in abfstclospc1n{1..3}.abfstclospcls1.bsli.com.; do dig $a +short ; done
10.21.134.17
10.21.134.18
10.21.134.19

```

#### 5.2.1.7. SSH KeyGen

```bash
[root@ABFSTCLBSTNPA1 ~]# ssh-keygen
[root@ABFSTCLBSTNPA1 ~]# cat .ssh/id_rsa.pub
ssh-rsa REDACTED root@ABFSTCLBSTNPA1

```

---

### 5.2.2. Installing an OpenShift Cluster 4.20.23 Using Agent-Based Installation

#### 5.2.2.1. Preparing to Install with the Agent-Based Installer

The Agent-based installation comprises a bootable ISO that contains the Assisted discovery agent and the Assisted Service. The `openshift-install agent create image` subcommand generates an ephemeral ISO based on two manifests:

* `install-config.yaml`
* `agent-config.yaml`

#### 5.2.2.2. Creating Install Config YAML

```yaml
# install-config.yaml
apiVersion: v1
baseDomain: bsli.com
proxy:
  httpProxy: http://185.46.212.88:80
  httpsProxy: http://185.46.212.88:443
  noProxy: 10.21.134.0/24,.bsli.com,localhost,127.0.0.1
compute:
- name: worker
  replicas: 0
controlPlane:
  name: abfstclospc1n
  replicas: 3
metadata:
  name: abfstclospcls1
networking:
  clusterNetwork:
  - cidr: 192.170.0.0/16
  hostPrefix: 23
  machineNetwork:
  - cidr: 10.21.134.0/24
  networkType: OVNKubernetes
  serviceNetwork:
  - 192.171.0.0/16
platform:
  none: {}
fips: false
pullSecret: 'paste Pull Secret'
sshKey: 'ssh-rsa REDACTED root@ABFSTCLBSTNPA1'

```

#### 5.2.2.3. Create Agent Config YAML

This configuration includes manifests for bond and VLAN interfaces with MTU 8500.

```yaml
# agent-config.yaml
apiVersion: v1alpha1
kind: AgentConfig
metadata:
  name: abfstclospcls1
rendezvousIP: 10.21.134.17
additionalNTPSources:
- 10.158.5.88
- 10.158.5.89
- 10.120.5.127
hosts:
  - hostname: abfstclospc1n1.abfstclospcls1.bsli.com
    role: abfstclospc1n
    rootDeviceHints:
      deviceName: "/dev/sda"
    interfaces:
    - name: ens6f0np0
      macAddress: "6C:83:75:12:3F:E4"
    - name: ens6f1np1
      macAddress: "6C:83:75:12:3F:E5"
    networkConfig:
      interfaces:
      - name: bond0
        type: bond
        state: up
        link-aggregation:
          mode: 802.3ad
          options:
            miimon: "100"
        port:
        - eno5
        - eno7
      - name: bond0.372
        type: vlan
        state: up
        vlan:
          base-iface: bond0
          id: 372
        ipv4:
          enabled: true
          address:
          - ip: 10.21.134.17
            prefix-length: 24
          dhcp: false
        dns-resolver:
          config:
            server:
            - 10.158.5.88
            - 10.158.5.89
            - 10.120.5.127
        routes:
          config:
          - destination: 0.0.0.0/0
            next-hop-address: 10.21.134.1
            next-hop-interface: bond0.372
            table-id: 254

  - hostname: abfstclospc1n2.abfstclospcls1.bsli.com
    role: abfstclospc1n
    rootDeviceHints:
      deviceName: "/dev/sda"
    interfaces:
    - name: eno5
      macAddress: "6C:83:75:12:7B:BA"
    - name: eno7
      macAddress: "6C:83:75:12:7B:BB"
    networkConfig:
      interfaces:
      - name: bond0
        type: bond
        state: up
        link-aggregation:
          mode: 802.3ad
          options:
            miimon: "100"
        port:
        - eno5
        - eno7
      - name: bond0.372
        type: vlan
        state: up
        vlan:
          base-iface: bond0
          id: 372
        ipv4:
          enabled: true
          address:
          - ip: 10.21.134.18
            prefix-length: 24
          dhcp: false
        dns-resolver:
          config:
            server:
            - 10.158.5.88
            - 10.158.5.89
            - 10.120.5.127
        routes:
          config:
          - destination: 0.0.0.0/0
            next-hop-address: 10.21.134.1
            next-hop-interface: bond0.372
            table-id: 254

  - hostname: abfstclospc1n3.abfstclospcls1.bsli.com
    role: abfstclospc1n
    rootDeviceHints:
      deviceName: "/dev/sda"
    interfaces:
    - name: eno5
      macAddress: "6C:83:75:12:83:52"
    - name: eno7
      macAddress: "6C:83:75:12:83:53"
    networkConfig:
      interfaces:
      - name: bond0
        type: bond
        state: up
        link-aggregation:
          mode: 802.3ad
          options:
            miimon: "100"
        port:
        - eno5
        - eno7
      - name: bond0.372
        type: vlan
        state: up
        vlan:
          base-iface: bond0
          id: 372
        ipv4:
          enabled: true
          address:
          - ip: 10.21.134.19
            prefix-length: 24
          dhcp: false
        dns-resolver:
          config:
            server:
            - 10.158.5.88
            - 10.158.5.89
            - 10.120.5.127
        routes:
          config:
          - destination: 0.0.0.0/0
            next-hop-address: 10.21.134.1
            next-hop-interface: bond0.372
            table-id: 254

```

To initialize creation:

```bash
[root@ABFSTCLBSTNPA1 ~]# mkdir ocp4 && cd ocp4/
[root@ABFSTCLBSTNPA1 ocp4]# cp ../install-config.yaml ../agent-config.yaml .

```

#### 5.2.2.4. Create Agent ISO

```bash
[root@ABFSTCLBSTNPA1 ocp4]# openshift-install agent create image
INFO Configuration has 3 abfstclospc1n replicas, 0 arbiter replicas, and 0 worker replicas
INFO The rendezvous host IP (node0 IP) is 10.21.134.17
INFO Extracting base ISO from release payload
INFO Generated ISO at agent.x86_64.iso.

[root@ABFSTCLBSTNPA1 ocp4]# ls
agent.x86_64.iso   auth   rendezvousIP

```

#### 5.2.2.5. Install Apache Web Server for Bootable Media URL

```bash
[root@ABFSTCLBSTNPA1 ocp4]# yum install httpd -y
[root@ABFSTCLBSTNPA1 ocp4]# mkdir -p /var/www/html/agent
[root@ABFSTCLBSTNPA1 ocp4]# cp agent.x86_64.iso /var/www/html/agent/agent.iso
[root@ABFSTCLBSTNPA1 ocp4]# chown apache:apache -R /var/www/html/agent/
[root@ABFSTCLBSTNPA1 ocp4]# chmod 755 -R /var/www/html/agent/
[root@ABFSTCLBSTNPA1 ocp4]# systemctl restart httpd

```

#### 5.2.2.6. Waiting Bootkube Complete

```bash
[root@ABFSTCLBSTNPA1 ocp4]# openshift-install agent wait-for bootstrap-complete --log-level=debug
...
INFO Host: abfstclospc1n1.abfstclospcls1.bsli.com, reached installation stage Joined
INFO Host: abfstclospc1n3.abfstclospcls1.bsli.com, reached installation stage Waiting for bootkube
INFO Host: abfstclospc1n2.abfstclospcls1.bsli.com, reached installation stage Done
INFO Bootstrap is complete
INFO cluster bootstrap is complete

```

#### 5.2.2.7. Waiting for Installation Complete

```bash
[root@ABFSTCLBSTNPA1 ocp4]# openshift-install agent wait-for install-complete --log-level=debug
...
INFO Cluster is installed
INFO Install complete!
INFO Login to the console with user: "kubeadmin", and password: "XXXXXXXXXXXXX"

[root@ABFSTCLBSTNPA1 ~]# export KUBECONFIG=/root/ocp4/auth/kubeconfig

```

#### 5.2.2.8. Cluster Status

```bash
[root@ABFSTCLBSTNPA1 ocp4]# oc get nodes
NAME                                      STATUS   ROLES                         AGE   VERSION
abfstclospc1n1.abfstclospcls1.bsli.com   Ready    control-plane,master,worker   15m   v1.33.11
abfstclospc1n2.abfstclospcls1.bsli.com   Ready    control-plane,master,worker   44m   v1.33.11
abfstclospc1n3.abfstclospcls1.bsli.com   Ready    control-plane,master,worker   45m   v1.33.11

[root@ABFSTCLBSTNPA1 ~]# oc get clusterversion
NAME      VERSION   AVAILABLE   PROGRESSING   SINCE   STATUS
version   4.20.23   True        False         7m48s   Cluster version is 4.20.23

```

---

### 5.2.3. Configure CyberArk OIDC OAuth Authentication

> 🛑 Please store the 'admin' password in a secured place as it has been granted with `cluster-admin` privileges to manage the entire OCP cluster.
> 
> 

#### Step 1: Collect CyberArk OIDC Details

* 
**Issuer URL:** `https://<tenant>.id.cyberark.cloud/oauth2/platform` 


* 
**Client ID:** `openshift` 


* 
**Redirect URI:** `https://oauth-openshift.apps.abfstclospcls1.bsli.com/oauth2callback/CyberArk` 



#### Step 3: Create OpenShift Secret

```bash
oc create secret generic cyberark-client-secret \
  --from-literal=clientSecret='<CLIENT_SECRET>' \
  -n openshift-config

```

#### Step 5: Configure OAuth Map

```bash
oc edit oauth cluster

```

```yaml
apiVersion: config.openshift.io/v1
kind: OAuth
metadata:
  name: cluster
spec:
  identityProviders:
  - name: CyberArk
    mappingMethod: claim
    type: OpenID
    openID:
      clientID: openshift
      clientSecret:
        name: cyberark-client-secret
      issuer: https://<tenant>.id.cyberark.cloud/oauth2/platform
      claims:
        preferredUsername:
        - email
        name:
        - name
        email:
        - email
        groups:
        - groups
      ca:
        name: cyberark-ca

```

#### Step 6: Verify Auth Operator Status

```bash
oc get co authentication

```

**Expected Output:** `authentication True False False` 

---

### 5.2.4. Configure Node Fencing + Node Health Check Operators

Performs IPMI-based fencing operations using Lenovo XCC/BMC interfaces to manage split-brain scenarios.

#### 5.2.4.1.1. Verify Fence Agent Connectivity

```bash
[root@ABFSTCLBSTNPA1 ~]# yum install -y fence-agents-all
[root@ABFSTCLBSTNPA1 ~]# fence_ipmilan -a 10.1.79.136 -l LENOVO -p Lenovo@123 -P -o status -u 623
Status: ON

```

#### Apply Fencing Agents Remediation Template

```bash
[root@ABFSTCLBSTNPA1 fencing]# oc apply -f fence-agent-credentials.yaml
[root@ABFSTCLBSTNPA1 fencing]# oc apply -f far-template.yaml

```

```yaml
# far-template.yaml excerpt
apiVersion: fence-agents-remediation.medik8s.io/v1alpha1
kind: FenceAgentsRemediationTemplate
metadata:
  name: fenceagentsremediationtemplate-default
  namespace: openshift-workload-availability
spec:
  template:
    spec:
      agent: fence_ipmilan
      nodeparameters:
        abfstclospc1n1.abfstclospcls1.bsli.com: 10.1.79.136
        abfstclospc1n2.abfstclospcls1.bsli.com: 10.1.79.137
        abfstclospc1n3.abfstclospcls1.bsli.com: 10.1.79.138
      remediationStrategy: OutOfServiceTaint
      retrycount: 5
      retryinterval: 5s
      sharedSecretName: fence-agent-credentials
      sharedparameters:
        --action: reboot
        --lanplus: ""
      timeout: 1m0s

```

---

### 5.2.5. Configure OpenShift Virtualization and NMState Operators

#### 5.2.5.1. Deploy and Configure OpenShift Virtualization Operator

1. Inside the console, navigate to **Operators** ➡️ **OperatorHub**.


2. Choose **OpenShift Virtualization Operator**, and click **Install**.


3. Ensure **All namespaces on the cluster** is selected under Installation Mode.


4. Set update channel to **stable** and strategy to **Automatic**.



Set storage profile default class:

```bash
[root@ABFSTCLBSTNPA1 fencing]# oc patch storageclass powerstore -p '{"metadata": {"annotations": {"storageclass.kubernetes.io/is-powerstore": "true"}}}'
storageclass.storage.k8s.io/powerstore patched

```

#### 5.2.5.2. Deploy and Configure NMState Operator

Map the OVN-Kubernetes secondary network to an Open vSwitch (OVS) bridge:

```bash
[root@ABFSTCLBSTNPA1 ~]# oc apply -f br-ex.yaml

```

```yaml
# br-ex.yaml
apiVersion: nmstate.io/v1
kind: NodeNetworkConfigurationPolicy
metadata:
  name: br-ex
spec:
  nodeSelector:
    node-role.kubernetes.io/worker: ""
  desiredState:
    ovn:
      bridge-mappings:
      - localnet: localnet-network
        bridge: br-ex
        state: present
---
apiVersion: k8s.cni.cncf.io/v1
kind: NetworkAttachmentDefinition
metadata:
  name: localnet-network
  namespace: default
spec:
  config: |
    {
    "cniVersion": "0.3.1",
    "name": "localnet-network",
    "type": "ovn-k8s-cni-overlay",
    "topology": "localnet",
    "netAttachDefName": "default/localnet-network"
    }

```

---

### 5.2.6. Configure Loki Stack and OpenShift Monitoring

#### 5.2.6.1. Configuring OpenShift Monitoring with Persistent Storage

```bash
[root@ABFSTCLBSTNPA1 ~]# oc project openshift-monitoring
[root@ABFSTCLBSTNPA1 monitoring]# oc apply -f cluster-monitor-config.yaml

```

```yaml
# cluster-monitor-config.yaml Excerpt
apiVersion: v1
kind: ConfigMap
metadata:
  name: cluster-monitoring-config
  namespace: openshift-monitoring
data:
  config.yaml: |
    alertmanagerMain:
      volumeClaimTemplate:
        spec:
          storageClassName: powerstore
          resources:
            requests:
              storage: 20Gi
    prometheusK8s:
      volumeClaimTemplate:
        spec:
          storageClassName: powerstore
          resources:
            requests:
              storage: 200Gi

```

#### 5.2.6.6. Apply LokiStack Configuration Manifests

```bash
[root@ABFSTCLBSTNPA1 ~]# oc create -f lokistack.yaml
[root@ABFSTCLBSTNPA1 ~]# oc create -f clusterlogging.yaml

```

---

### 5.2.7. Configure Dell CSM Storage

#### 5.2.7.1. Dell CSM PowerStore Deployment on OpenShift

Create multipath configuration via MachineConfig:

```bash
[root@ABFSTCLBSTNPA1 dell-csm]# oc apply -f 99-multipath-master.yaml

```

Create backend connectivity configuration properties layout:

```yaml
# config.yaml
arrays:
  - endpoint: "https://10.158.5.226/api/rest"
    globalID: "PRedHat259f17"
    username: "Username"
    password: "Passowrd"
    skipCertificateValidation: true
    blockProtocol: "FC"

```

```bash
[root@ABFSTCLBSTNPA1 dell-csm]# oc create secret generic powerstore-config --from-file=config=config.yaml -n powerstore
[root@ABFSTCLBSTNPA1 dell-csm]# oc apply -f csm-config.yaml
[root@ABFSTCLBSTNPA1 dell-csm]# oc apply -f sc-powerstore.yaml

```

---

### 5.2.8. Configure Advanced Cluster Management (ACM) Observability

#### Step 2: Create Thanos Object Storage Secret

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: thanos-object-storage
  namespace: open-cluster-management-observability
type: Opaque
stringData:
  thanos.yaml: |
    type: s3
    config:
      bucket: acmobservabilityclu1
      endpoint: abcarchival.bsli.com:9020
      insecure: true
      access_key: '2_BSLI\ss070631_accid'
      secret_key: 'suS13TMFaN1KEV3xXfDzcLCJLvXq'

```

```bash
[root@ABFSTCLBSTNPA1 ~]# oc apply -f thanos-object-storage.yaml
[root@ABFSTCLBSTNPA1 ~]# oc apply -f mco.yaml

```

---

### 5.2.10. Configure Kubelet maxPods to 500 on Master MachineConfigPool

Increase maximum scheduled capacity limit per combined control node:

```bash
[root@ABFSTCLBSTNPA1 ~]# oc apply -f custom-max-pods.yaml

```

```yaml
apiVersion: machineconfiguration.openshift.io/v1
kind: KubeletConfig
metadata:
  name: custom-max-pods
spec:
  machineConfigPoolSelector:
    matchLabels:
      pools.operator.machineconfiguration.openshift.io/master: ""
  kubeletConfig:
    maxPods: 500

```

Verify enforcement verification check:

```bash
[root@ABFSTCLBSTNPA1 ~]# oc get node abfstclospc1n1.abfstclospcls1.bsli.com -o jsonpath='{.status.capacity.pods}{"\n"}'
500

```

---

### 5.2.12. Deploying OpenShift Internal Registry with S3 Object Storage

Leverages Dell PowerScale (Isilon) backend platform strategy infrastructure mapping configuration specs:

```bash
[root@ABFSTCLBSTNPA1 ~]# oc create secret generic image-registry-private-configuration-user \
  --from-literal=REGISTRY_STORAGE_S3_ACCESSKEY=registryuser \
  --from-literal=REGISTRY_STORAGE_S3_SECRETKEY='xxxxxxxxxxxx' \
  -n openshift-image-registry

```

Update Image Registry Management settings:

```bash
[root@ABFSTCLBSTNPA1 ~]# oc patch configs.imageregistry.operator.openshift.io cluster --type merge -p '{"spec":{"managementState":"Managed"}}'

```

---

### 5.2.16. Encrypting the ETCD Data

By default, etcd data is not encrypted in OpenShift Container Platform. You can enable etcd encryption for your cluster to provide an additional layer of data security. When enabled, it encrypts Secrets, ConfigMaps, Routes, and OAuth Tokens.

#### 5.2.16.1. ETCD Backup Using NFS Persistent Storage

```bash
[root@ABFSTCLBSTNPA1 ~]# showmount -e
Export list for ABFSTCLBSTNPA1:
/ocp_etcd *
/nfs-iso  *

```

Create backup namespaces and permissions mapping definitions:

```bash
[root@ABFSTCLBSTNPA1 etcd-backup]# oc create -f 01-namespace.yaml
[root@ABFSTCLBSTNPA1 etcd-backup]# oc create -f 02-cluster-role-etcd-bkp.yml
[root@ABFSTCLBSTNPA1 etcd-backup]# oc create -f 03-cluster-role-binding-etcd-bkp.yml
[root@ABFSTCLBSTNPA1 etcd-backup]# oc create -f 04-sa-etcd-bkp.yml
[root@ABFSTCLBSTNPA1 etcd-backup]# oc adm policy add-scc-to-user privileged -z openshift-backup -n ocp-etcd-backup

```

Apply automated CronJob schema definition script map:

```bash
[root@ABFSTCLBSTNPA1 etcd-backup]# oc create -f 05-cm-script.yaml
[root@ABFSTCLBSTNPA1 etcd-backup]# oc create -f 06-etcd-nfs.yaml
[root@ABFSTCLBSTNPA1 etcd-backup]# oc create -f 07-cron-job.yaml

```

---

## Appendix A: Engaging Red Hat Global Support Services

### Support Severity Level Definitions

* 
**Severity 1 (Urgent):** Your production system is severely impacted, or down, and your business operations are stopped.


* **Severity 2 (High):** The product is usable, but your business operations are severely restricted. No procedural workaround exists.


* **Severity 3 (Medium):** The product is usable, with non-critical components or features affected. A workaround exists.


* 
**Severity 4 (Low):** General usage questions, documentation errors, or future enhancement suggestions.



### Tips to Create a Good Support Case

1. Explicitly identify your specific accounts details and structural environment references inside descriptions fields.


2. Provide precise keywords inside problem definitions descriptions summaries blocks (e.g. `Ceph...`, `Nova...`).


3. Description formats should follow the format pattern convention:


`[Component][Region] Issue description`

*Example:* `[Nova][NL Region] Nova fails on one compute` 


4. Always generate and append standard troubleshooting files mappings blocks updates output context (`sosreport`) to speed up cases handling cycles lifetimes timeline chains.
