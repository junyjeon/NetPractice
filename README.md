# NetPractice

<div align="center">
  <img src="assets/10_netpractice_review.jpg" alt="NetPractice Review" width="800"/>
  
  [![42 Score](https://img.shields.io/badge/Score-100%2F100-success?style=for-the-badge&logo=42)](https://github.com/junyjeon/NetPractice)
  [![Network](https://img.shields.io/badge/Network-TCP%2FIP-blue.svg?style=for-the-badge&logo=cisco)](https://github.com/junyjeon/NetPractice)
</div>

## Table of Contents
- [About](#about)
- [Basic Theory](#basic-theory)
  - [IP Address](#ip-address)
  - [Subnet Mask](#subnet-mask)
  - [Network Layers](#network-layers)
- [Network Configuration](#network-configuration)
  - [Switch (L2)](#switch-l2)
  - [Router (L3)](#router-l3)
  - [Gateway](#gateway)
- [Practice Levels](#practice-levels)
  - [Level 1-3: Basic](#level-1-3-basic)
  - [Level 4-6: Subnet](#level-4-6-subnet)
  - [Level 7-10: Advanced](#level-7-10-advanced)
- [Checklist](#checklist)
- [Reference](#reference)

### 🗣️ About
TCP/IP 주소 체계와 서브넷 마스크를 이해하고 네트워크를 구성하는 과제입니다.
스위치(L2)와 라우터(L3)를 사용해 네트워크를 연결하고 통신이 가능하도록 설정합니다.

### Basic Theory
#### IP Address
• A클래스: 255.0.0.0 (0-127)
• B클래스: 255.255.0.0 (128-191)
• C클래스: 255.255.255.0 (192-223)

사용할 수 없는 주소:
• 127.0.0.0/8: 루프백
• 사설IP:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16
• 각 네트워크의 .0과 .255

#### Subnet Mask
• 2진수 기본값
  - 128 = 1000 0000
  - 192 = 1100 0000
  - 224 = 1110 0000
  - 240 = 1111 0000
  - 248 = 1111 1000
  - 252 = 1111 1100

• 서브넷 범위
  - /24 = 256개 (0~255)
  - /25 = 128개씩 2개
  - /26 = 64개씩 4개
  - /27 = 32개씩 8개
  - /28 = 16개씩 16개
  - /29 = 8개씩 32개
  - /30 = 4개씩 64개 (라우터 연결용)

• 실제 분할 예시
192.168.1.0/24를 /26으로 분할:
  - 192.168.1.0~63 (첫 번째)
  - 192.168.1.64~127 (두 번째)
  - 192.168.1.128~191 (세 번째)
  - 192.168.1.192~255 (네 번째)

#### Network Layers
• L2 데이터링크 계층
  - MAC 주소로 통신
  - 스위치로 연결
  - 같은 네트워크 내 통신

• L3 네트워크 계층
  - IP 주소로 통신
  - 라우터로 연결
  - 다른 네트워크 간 통신

### Network Configuration
#### Switch (L2)
• 특징
  - MAC 주소 기반 통신
  - 같은 네트워크 내에서만 통신
  - 브로드캐스트 도메인 공유

• 설정 시 주의점
  - 모든 장비는 같은 네트워크여야 함
  - IP 주소 중복되면 안 됨
  - 게이트웨이 설정 불필요

#### Router (L3)
• 특징
  - IP 주소 기반 통신
  - 다른 네트워크 연결 가능
  - 최적 경로 설정

• 라우터 간 연결
  - /30 서브넷 마스크 사용
  - 4개 IP 중 2개만 사용 가능
  예) 10.0.0.0/30
      - R1: 10.0.0.1
      - R2: 10.0.0.2
      - .0과 .3은 사용 불가

#### Gateway
• 설정 규칙
  - 반드시 같은 네트워크에 있어야 함
  - 보통 네트워크의 첫/마지막 번호 사용
  - 실제 존재하는 IP여야 함

• 예시
  192.168.1.0/24 네트워크:
  - 게이트웨이: 192.168.1.254
  - 호스트: 192.168.1.1~253 사용

### Practice Levels
#### Level 1-3: Basic
• Level 1: PC 직접 연결
  - 두 PC를 직접 연결
  - 같은 네트워크로 설정
  예) PC1: 192.168.0.1
      PC2: 192.168.0.2

• Level 2: 스위치 연결
  - 여러 PC를 스위치로 연결
  - 모두 같은 네트워크여야 함
  예) PC1: 192.168.0.10
      PC2: 192.168.0.11
      PC3: 192.168.0.12

• Level 3: 라우터 연결
  - 서로 다른 네트워크 연결
  - 게이트웨이 설정 필수
  예) A망: 192.168.0.x (게이트웨이 .254)
      B망: 192.168.1.x (게이트웨이 .254)

#### Level 4-6: Subnet
• Level 4: 기본 서브넷
  - 네트워크 크기 조절
  - 적절한 마스크 선택

• Level 5: 라우터 간 연결
  - /30 서브넷 사용
  - IP 낭비 최소화

• Level 6: 인터넷 연결
  - 사설IP와 공인IP 구분
  - NAT 개념 이해

#### Level 7-10: Advanced
• Level 7: 복잡한 라우팅
  - 여러 구간의 게이트웨이
  - 경로 설정 순서 중요
  예) A → R1 → R2 → B
      A의 게이트웨이는 R1
      R1은 R2로 전달
      R2는 B로 전달

• Level 8: 다중 라우터
  - 3개 이상 라우터 연결
  - 각 구간 다른 네트워크
  예) R1 - R2 - R3
      R1-R2: 10.0.0.0/30
      R2-R3: 10.0.0.4/30

• Level 9: 효율적 서브넷
  - 필요한 크기만큼 분할
  - IP 낭비 최소화
  예) 50대 필요 → /26 (64개)
      10대 필요 → /28 (16개)

• Level 10: 종합 구성
  - 모든 개념 통합
  - 전체 네트워크 통신
  예) Client망 ↔ R1 ↔ R2 ↔ Server망
      192.168.0.x ↔ 10.0.0.x ↔ 10.0.1.x ↔ 192.168.1.x

### Checklist
#### 기본 설정
[] 네트워크 구조 파악
[] 필요한 IP 개수 확인
[] 서브넷 크기 결정
[] IP 범위 계획
[] 게이트웨이 위치 선정

#### IP/마스크 검증
[] .0/.255 미사용 확인
[] IP 중복 확인
[] 게이트웨이 동일 네트워크 확인
[] 라우터 연결 /30 확인
[] 서브넷 크기 적절성 확인

#### 통신 검증
[] 같은 네트워크 통신
[] 다른 네트워크 통신
[] 양방향 통신
[] 불필요한 IP 낭비
[] 확장 가능성

### Reference
• 공식 문서
  - [RFC 1918 - Private Address Space](https://datatracker.ietf.org/doc/html/rfc1918)
  - [Subnet Calculator](https://www.subnet-calculator.com/)

• 유용한 도구
  - [Visual Subnet Calculator](https://www.davidc.net/sites/default/subnets/subnets.html)
  - [IP Subnet Calculator](http://jodies.de/ipcalc)

• 학습 자료
  - [OSI 7계층과 TCP/IP](https://popcorntree.tistory.com/107)
  - [chanheki의 NetPractice](https://github.com/chanheki/NetPractice)
  - [Practical Networking](https://www.practicalnetworking.net/)
  - [Subnet Guide](https://www.subnet-calculator.com/subnet.php)