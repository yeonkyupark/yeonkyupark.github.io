---
title: UV 기반 파이썬 프로젝트 관리
date: 2026-03-24
categories: [interest]
tags: [python, uv]
image: /assets/images/logo_python.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

## UV 개요
`uv`는 Astral에서 만든 차세대 Python 패키지 및 환경 관리 도구다. 기존의 pip, venv, poetry 등을 통합한 형태라고 보면 된다.

### 핵심 특징

- 매우 빠른 패키지 설치 (Rust 기반)  
- 가상환경 자동 관리  
- 의존성 lock 파일 지원  
- pip 호환 (기존 프로젝트 전환 쉬움)  

### 장점과 단점

#### 장점

- 압도적인 속도, pip 대비 수십 배 빠른 설치 속도  
- 통합 관리, 가상환경 + 패키지 관리 + 실행까지 한번에  
- 간결한 명령어, 복잡한 poetry/conda보다 직관적이고 단순  
- 재현형 보장, lock 파일 기반 동일 환경 유지  

#### 단점

- 신규 도구, 생태계/레퍼런스가 적음  
- 고급 기능 제한, poetry 대비 일부 기능 부족  
- 팀 적응 필요, 기존 pip/conda 사용자에게 러닝커브 존재  

## UV 설치

Python 설치 환경에선 `pip` 명령어로 `uv`를 설치한다.

```
pip install uv
```

설치가 완료되면 아래와 같이 설치된 버전을 확인하면서 이상 유무를 점검한다.

```
uv --version
```

## 프로젝트 관리

### 프로젝트 생성 및 초기화

`uv init` 명령어로 프로젝트를 생성 및 초기화 한다.

```
uv init my-project
cd my-project
```

프로젝트가 생성 및 초기화되면 프로젝트 이름으로 폴더가 생성되고 아래와 같은 구조를 갖게 된다.

```
D:\my-project
├── .gitignore
├── .python-version
├── main.py
├── pyproject.toml
└── README.md
```

### 가상환경 생성

`uv add`나 `uv run` 시 가상환경이 자동으로 생성된다. 명시적으로 가상환경을 생성하려면 `uv venv` 명령을 사용하다.

```
uv venv
```

프로젝트 폴더 내 *.venv* 하위 폴더가 생성된다.

## 의존성 관리

### 패키지 설치

`uv add` 명령어로 패키지를 설치한다.

```
uv add requests                         # 패키지 하나 설치
uv add numpy pandas matplotlib seaborn  # 패키지 여러 개 설치
```

### 패키지 제거

`uv remove` 명령어로 설치된 패키지를 제거한다.

```
uv remove requests
```

### requirements.txt 변환

기존 `pip` 관리 형태 호환성을 위해 필요한 경우 *requirements.txt* 파일을 다음과 같이 생성할 수 있다.

```
uv pip compile requirements.in -o requirements.txt
```

또는

```
uv pip install -r requirements.txt
```

### 의존성 고정(Lock)

`uv lock` 명령어로 설치된 패키지 간 의존성을 고정한다. 의존성이 고정되면 *uv.lock* 파일이 생성된다.

#### lock 기반 설치

`uv sync` 명령어로 고정된 의존성에 맞춰 패키지를 설치한다.

```
uv sync
```

위 코드는 `pip` 환경에서 다음과 가까운 형태로 동작한다.

```
pip install -r requirements.txt
```

`uv sync` 특징

- 없는 패키지 설치
- 필요없는 패키지 제거
- 버전까지 완전히 일치

*requirements.txt*이 추가 설치 개념이라면 *uv.lock*은 완전 동기화를 하는 개념이다.

## 실행 관리

### 스크립트 실행

```
uv run python main.py
```

### 모듈 실행

```
uv run -m app.main
```


## 참고자료

- uv 공식 사이트: https://docs.astral.sh/uv/ 
