# AWS 기반 고가용성 보안 NAS 구축 프로젝트 ☁️

### 포트폴리오를 위해 AWS 클라우드 환경에서 **보안**과 **고가용성**을 최우선으로 고려하여 개인용 NAS(Network Attached Storage)를 구축한 프로젝트입니다.

단순한 파일 서버를 넘어, 실제 서비스 환경에서 발생할 수 있는 장애에 자동으로 대응하고 데이터를 안전하게 보호하는 안정적이고 탄력적인 클라우드 인프라를 설계하고 구현하는 데 중점을 두었습니다.

<br>

## 🚀 아키텍처 (Architecture)

이 시스템의 모든 구성 요소는 아래 아키텍처 다이어그램에 따라 배치되었습니다. Multi-AZ 구성과 네트워크 망 분리를 통해 장애 대응 능력과 보안을 동시에 확보했습니다.

![프로젝트 아키텍처 다이어그램](https://github.com/Imirain/AWS-Security-Portfolio-Project/blob/main/images/aws_nas_architecture.png)

---

## ✨ 핵심 기능 (Key Features)

* **⚙️ 고가용성 및 자동 장애 복구 (High Availability & Automatic Failover)**
  * **Multi-AZ** 환경에 EC2 인스턴스를 이중으로 배치하고 **Application Load Balancer(ALB)**와 **Auto Scaling Group(ASG)**을 연동하여 구성했습니다.
  * 하나의 가용 영역 또는 인스턴스에 장애가 발생하면, ALB가 이를 자동으로 감지하여 모든 트래픽을 건강한 인스턴스로 즉시 전환함으로써 **서비스 중단을 방지**합니다.

* **🛡️ 강화된 다계층 보안 (Enhanced Multi-Layered Security)**
  * **Public/Private Subnet**을 분리하여 외부에는 서비스 접근점(ALB, Bastion Host)만 노출하고, 핵심 데이터가 처리되는 NAS 서버(EC2)는 Private Subnet에 안전하게 격리했습니다.
  * 관리자 접근은 지정된 보안 통로인 **Bastion Host**를 통해서만 가능하도록 제한하여 시스템 보안을 강화했습니다.

* **🗂️ 중앙화된 공유 스토리지 (Centralized Shared Storage)**
  * **Amazon EFS**를 도입하여 여러 EC2 인스턴스가 동일한 파일 시스템을 공유합니다.
  * 이를 통해 어느 서버로 접속하든 항상 **일관된 데이터를 읽고 쓸 수 있으며**, EFS 자체도 Multi-AZ로 구성되어 데이터의 내구성이 매우 높습니다.

* **🔒 안전한 아웃바운드 통신 (Secure Outbound Communication)**
  * **NAT Gateway**를 통해 Private Subnet의 EC2 인스턴스가 OS 업데이트 등을 안전하게 수행할 수 있도록 구성했습니다. 외부에서 내부로의 직접적인 연결은 차단됩니다.

---

## 🛠️ 기술 스택 (Tech Stack & Key Services)

| 구분 | 기술 스택 |
| :--- | :--- |
| **네트워크** | `VPC`, `Subnet`, `Route Table`, `Internet Gateway`, `NAT Gateway` |
| **컴퓨팅** | `EC2`, `Auto Scaling Group` |
| **스토리지** | `EFS` |
| **로드 밸런싱** | `Application Load Balancer (ALB)` |
| **보안 및 접근 제어** | `Security Group`, `NACL`, `Bastion Host`, `IAM` |
| **모니터링** | `CloudWatch` |