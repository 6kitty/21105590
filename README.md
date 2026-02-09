# KSMBD 커널 취약점 분석 연구

Linux 커널의 SMB 데몬(KSMBD)에서 발견된 취약점을 분석하고 학습한 내용을 정리한 저장소입니다.

## 개요

KSMBD는 Linux 커널에 내장된 SMB3 프로토콜 서버로, 이 저장소에서는 다음 두 가지 취약점을 중점적으로 분석합니다:

- **ZDI-23-979**: NULL 포인터 역참조를 통한 서비스 거부(DoS) 취약점
- **ZDI-23-980**: Out-of-Bounds Read를 통한 커널 메모리 유출 취약점

## 저장소 구조

```
├── _posts/
│   ├── 25-10-10-ksmbd.md       # KSMBD 소개 및 ZDI-23-979 분석
│   ├── 25-10-15-ksmbd2.md      # ZDI-23-980 OOB Read 취약점 분석
│   ├── 25-10-16-ksmbd3.md      # 리눅스 커널 기초 (메모리 구조, Slab 할당자)
│   └── 25-10-17-ksmbd4.md      # 커널 디버깅 환경 구축 (QEMU, GDB)
├── 시스템보안_기말보고서.pdf
└── 시스템보안_중간보고서_서울여자대학교_정보보호학과_육은서.pdf
```

## 포스트 목록

### 1. KSMBD 취약점 개요 및 ZDI-23-979

SMB 프로토콜과 KSMBD의 기본 개념을 다루고, NULL 포인터 역참조를 이용한 DoS 취약점의 원인과 PoC를 분석합니다.

### 2. ZDI-23-980 OOB Read 분석

Out-of-Bounds Read 취약점을 통해 최대 65KB의 커널 메모리를 유출하는 기법을 분석합니다. `SMB_WRITE`와 `SMB_ECHO` 두 가지 익스플로잇 방식을 다룹니다.

### 3. 리눅스 커널 기초

커널 공간과 유저 공간의 차이, 태스크 구조체, x86-64 메모리 맵(4단계 페이지 테이블), Slab 할당자 등 커널 익스플로잇을 이해하기 위한 기초 지식을 정리합니다.

### 4. 커널 디버깅 환경 구축

커널 이미지 종류(vmlinux, bzImage), 커널 컴파일 방법, QEMU/BusyBox를 이용한 테스트 환경 구성, GDB 원격 디버깅 설정 방법을 안내합니다.

## 환경 구축

분석 환경을 구성하려면 다음 도구들이 필요합니다:

```bash
# 커널 빌드 의존성
sudo apt-get install build-essential libncurses-dev bison flex libssl-dev libelf-dev

# 가상화 및 디버깅
sudo apt-get install qemu-system-x86 gdb

# Python 라이브러리 (PoC 실행용)
pip install impacket pwntools
```

## 참고 자료

- [KSMBD 공식 문서](https://docs.kernel.org/filesystems/smb/ksmbd.html)
- [ZDI-23-979 Advisory](https://www.zerodayinitiative.com/advisories/ZDI-23-979/)
- [ZDI-23-980 Advisory](https://www.zerodayinitiative.com/advisories/ZDI-23-980/)
