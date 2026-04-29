# 🗺️ OSGeo 공간정보 개발환경 (Apple Silicon Mac)

PostGIS + pgAdmin + GeoServer를 Podman Pod로 구성하는 로컬 공간정보 개발환경입니다.  
[eduOSGeoSeoul](https://github.com/kacgung/eduOSGeoSeoul) 교육과정을 기반으로 Apple Silicon Mac 환경에 맞게 구성했습니다.

---

## 구성 요소

| 도구 | 역할 | 접속 주소 | 계정 |
|---|---|---|---|
| **PostGIS** | 공간 데이터베이스 | `localhost:5432` | postgres / postgres |
| **pgAdmin 4** | DB 관리 GUI | http://localhost:8070 | admin@admin.com / admin |
| **GeoServer** | 웹 지도 서비스 발행 | http://localhost:8080/geoserver | admin / geoserver |
| **QGIS** | 데스크탑 GIS (맥 네이티브) | — | — |

---
## 목차
- [개발환경구축](#개발환경구축)
  - [구성 요소](#구성-요소)
  - [사전 준비](#사전-준비)
  - [설치 방법](#설치-방법)
  - [사용 방법](#사용-방법)
  - [연결 구조](#연결-구조)
  - [참고](#참고)

## 사전 준비

- Apple Silicon Mac (M1/M2/M3/M4)
- [Homebrew](https://brew.sh) 설치 완료
- QGIS 설치: [qgis.org](https://qgis.org/downloads/macos/) 에서 직접 다운로드

---

## 설치 방법

### 1. Podman 설치 및 머신 시작

```bash
brew install podman
podman machine init
podman machine start
```
<img width="1124" height="178" alt="image" src="https://github.com/user-attachments/assets/f0d3b7a2-da40-4096-ad8e-b7f8b114e489" />

### 2. Pod 생성

```bash
podman pod create --name osgeo-pod -p 5432:5432 -p 8070:8070 -p 8080:8080
```

### 3. PostGIS 실행

> Apple Silicon에서는 `--platform linux/amd64` 옵션이 필요합니다.

```bash
podman run -d --pod osgeo-pod --name postgis \
  --platform linux/amd64 \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=postgres \
  -e POSTGRES_DB=gisdb \
  -v postgis_db:/var/lib/postgresql/data \
  postgis/postgis:17-3.5
```

### 4. pgAdmin 실행

```bash
podman run -d --pod osgeo-pod --name pgadmin \
  -e PGADMIN_DEFAULT_EMAIL=admin@admin.com \
  -e PGADMIN_DEFAULT_PASSWORD=admin \
  -e PGADMIN_LISTEN_PORT=8070 \
  dpage/pgadmin4:8.14
```

### 5. GeoServer 실행

```bash
podman run -d --pod osgeo-pod --name geoserver \
  -e GEOSERVER_DATA_DIR=/opt/geoserver_data \
  -v geoserver_data:/opt/geoserver_data \
  docker.osgeo.org/geoserver:2.28.0
```

### 6. 상태 확인

```bash
podman stats --no-stream --format "table {{.Name}} {{.CPUPerc}} {{.MemPerc}}"
```
<img width="900" height="240" alt="image" src="https://github.com/user-attachments/assets/8dac2cde-3dd6-4231-9674-473b1b8db880" />

---

## 사용 방법

### 재부팅 후 시작

```bash
podman machine start
podman pod start osgeo-pod
```

### Pod 관리

```bash
podman pod stop osgeo-pod      # 중지
podman pod start osgeo-pod     # 시작
podman ps --pod                # 상태 확인
podman pod rm -f osgeo-pod     # 완전 삭제 (데이터 볼륨은 유지됨)
```

---

## 연결 구조

```
공공데이터 (SHP, GeoJSON 등)
        ↓
    PostGIS          ← 데이터 저장 / 공간 SQL 분석
        ↑↓
    pgAdmin          ← DB 내용 확인 / 쿼리 실행
        ↓
    GeoServer        ← WMS / WFS로 웹 지도 서비스 발행
        ↓
    QGIS             ← 데이터 시각화 / 편집
```

---

## 참고

- pgAdmin에서 PostGIS 연결 시 Host: `localhost`
- GeoServer에서 PostGIS 저장소 등록 시 Host: `localhost`
- 윈도우 교안의 백틱(`` ` ``) 줄바꿈 → 맥에서는 백슬래시(`\`) 사용
- 윈도우 교안의 `:Z` 볼륨 옵션 → 맥에서는 제거 (SELinux 전용)
