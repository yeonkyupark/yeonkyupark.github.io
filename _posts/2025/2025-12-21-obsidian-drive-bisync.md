---
title: 옵시디언과 구글 드리이브 연동
date: 2025-12-21 
categories: [hobby]
tags: [obsidian, drive]
image: /assets/images/logo_obsidian.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

옵시디언(https://obsidian.md/)과 구글 드라이브(https://drive.google.com) 연동하는 방법은 여러 가지가 있다. 윈도우즈에서는 데스트톱용 Drive(https://dl.google.com/drive-file-stream/GoogleDriveSetup.exe)를 설치하고 옵시디언에서 Vault를 Drive로 직접 설정하면 된다. 리눅스 경우 데스크톱용 Drive를 제공하지 않는다. 따라서 Drive와 연동해서 사용하려면 몇 가지 설정을 해야 한다.

구글 Drive와 옵시디언 연동
- Drive mount + 직접 연결
- 옵시디언 유료 버전이 관련 유료 어플 이용
- 로컬 Vault + rclone sync

일반적으로 가장 추천하는 방식인 로컬 Vault +clone sync를 이용하는 절차를 알아본다.

## Google Drive 저장소 준비

구글 드라이브에 Vault용 폴더를 생성한다. 이 폴더는 데이터 백업과 동기화 허브 역할을 하게 된다.

```
Obsidian
```

## 로컬 Vault 생성

개인 PC에 데이터를 저장할 Vault용 폴더를 생성한다.

```
~/ObsidianVault
```

## rclone 설정

구글 드라이브와 로컬 Vault를 연결하기 위한 rclone을 생성한다.

```
rclone config
```

이름은 `gdrive`, Storage는 `18 Google Drive`를 선택한다. 이후 설정 요청에 따라 적절하게 옵션을 선택 및 설정한다.

## 최초 동기화

```
rclone bisync ~/ObsidianVault gdrive:ObsidianVault \
  --checksum \
  --resync
```

`--resync` 옵션은 최초 1회만 수행한다. 따라서 위 명령은 터미널에서 1회만 수동으로 수행하고 이후 자동 동기화 시에는 해당 옵션을 제거한다.

## 자동 동기화 

먼저 서비스를 생성하고 생성된 서비스가 주기적으로 실행되도록 타이머를 설정한다.

### 서비스 등록

```
~$ nano .config/systemd/user/obsidian-bisync.service
```

`obsidian-bisync.service` 파일에는 아래 내용을 작성한다.

```
[Unit]
Description=Obsidian Vault rclone bisync
After=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/bin/rclone bisync %h/ObsidianVaults/Personal "gdrive:Obsidian/Personal Vault" \
    --checksum 
    --drive-skip-gdocs 
    --log-file=%h/.cache/rclone-obsidian.log 
    --log-level=INFO
```

내용을 작성한 후 서비스를 실행한다.

```
systemctl --user daemon-reload
systemctl --user start obsidian-bisync.service
```

### 타이머 생성

타이머 파일을 생성한다.

```
nano ~/.config/systemd/user/obsidian-bisync.timer
```

해당 파일에는 아래 내용을 작성한다.

```
[Unit]
Description=Run Obsidian bisync every 15 minutes

[Timer]
OnBootSec=2m
OnUnitActiveSec=15m
Persistent=true

[Install]
WantedBy=timers.target
```

`OnUnitActiveSec` 옵션을 통해 동기화 주기를 설정한다.

마지막으로 타이머를 `systemd`에 등록 및 실행한다.

```
systemctl --user daemon-reload
systemctl --user enable obsidian-bisync.timer
systemctl --user start obsidian-bisync.timer
```

정상적으로 동작하지 않는 경우 다음 사항을 점검해 본다.
- 폴더 및 파일명이 정확한가? 공백이 있는 경우 쌍따옴표(“)를 이용하여 묶어 준다.
- 옵션 설정이 제대로 되어 있는가? `.service` 파일에서는 `~` 경로를 인식하지 않으므로 절대 경로 또는 `%h`을 이용하여 설정한다.
- rclone 접근 승인은 완료되었는가? 충돌이나 알 수 없는 경우로 접근 권한이 사라진다면 기존 설정을 삭제한 후 새로 만드는 것을 추천한다.

**추가**

아래와 같이 `resync` 요청이 있는 경우 다음 순서에 따라 작업을 진행한다.

```
ERROR : Bisync critical error: cannot find prior Path1 or Path2 listings
ERROR : Bisync aborted. Must run --resync to recover.
```

위 내용은 비정상 종료에 의해 발생하며 터미널에서 `--resync` 동작을 통해 해결한다.  

우선 타이머와 서비스를 종료한다.

```
systemctl --user stop obsidian-bisync.timer
systemctl --user stop obsidian-bisync.service
```

`bisync` 관련 파일을 정리한다.

```
rm -rf ~/.cache/rclone/bisync*
rm -rf ~/.config/rclone/bisync*
```

터미널에서 `--resync` 동작을 수행한다.

```
/usr/bin/rclone bisync ~/PC경로 "gdrive:구글드라이브경로" --resync
```

서비스와 타이머를 실행 시킨다.

```
systemctl --user start obsidian-bisync.service
```

```
systemctl --user enable --now obsidian-bisync.timer
```

마지막으로 상태를 확인한다.

```
systemctl --user status obsidian-bisync.service
systemctl --user status obsidian-bisync.timer
```



