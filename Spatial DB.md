### 4.2 일괄 업로드 스크립트 실행
데이터가 위치한 디렉토리로 이동하여 아래 쉘 스크립트를 실행합니다. 이 스크립트는 해당 디렉토리의 모든 `.shp` 파일을 찾아 PostGIS에 업로드합니다.

<img width="485" height="314" alt="image" src="https://github.com/user-attachments/assets/a4bb973b-cf45-4ad2-abba-255475fffecb" />

<img width="299" height="464" alt="image" src="https://github.com/user-attachments/assets/670a572b-cafa# PostGIS 공간 DBMS 구축 및 QGIS 연동 가이드

> 참고 강의: [eduOSGeoSeoul - Lecture-PostGIS](https://github.com/kacgung/eduOSGeoSeoul/blob/main/Lecture-PostGIS/Lecture-PostGIS.md)

---

## 1. PostGIS 환경 준비 (pgAdmin)

### 1.1 서버 등록
브라우저에서 `http://localhost:8070` 접속 후 서버를 등록합니다. (ID: `admin@admin.com` / PW: `admin`)

| 분류 | 항목 | 값 |
|:---:|---|---|
| **General** | Name | `postgis` |
| **Connection** | Host name | `localhost` |
| **Connection** | Port | `5432` |
| **Connection** | Username | `postgres` |
| **Connection** | Password | `postgres` |

### 1.2 데이터베이스 생성 및 확장 설치
`osgeo` 데이터베이스를 생성하고 공간 기능을 활성화합니다.

*   **Database 생성 설정 (Definition 탭)**
    *   **Encoding:** `UTF8`
    *   **Template:** `template0`
    *   **Collation / Character type:** `C` (⚠️ 한글 정렬 및 검색 오류 방지)

*   **PostGIS 확장 설치**
    Query Tool에서 아래 명령어를 실행합니다.
    ```sql
    CREATE EXTENSION postgis;
    ```

### 1.3 설치 확인 ✅
`osgeo` 데이터베이스의 Extensions에 postgis가 정상적으로 추가되었는지 확인합니다.

<img width="1119" height="629" alt="image" src="https://github.com/user-attachments/assets/0432e493-f437-4279-9fb6-db32b1230c09" />

---

## 2. QGIS 연동 설정

QGIS 탐색기 패널에서 **PostgreSQL 우클릭 > 새 연결**을 선택하여 정보를 입력합니다.

| 항목 | 값 |
|:---:|---|
| **이름** | `osgeo` |
| **호스트** | `localhost` |
| **포트** | `5432` |
| **데이터베이스** | `osgeo` |
| **사용자/비밀번호** | `postgres` / `postgres` |

---

## 3. 공간 데이터 업로드 (GUI 방식)

### 3.1 DB 관리자 (단일 레이어)
1. `메뉴 > 데이터베이스 > DB 관리자` 접속
2. `제공자 > PostGIS > osgeo > public` 선택
3. **레이어/파일 불러오기** 클릭 후 `.shp` 파일 선택

### 3.2 공간 처리 툴박스 (일괄 처리)
1. `메뉴 > 공간 처리 > 공간 처리 툴박스`
2. **PostgreSQL로 내보내기** 검색 후 **배치 프로세스# PostGIS 공간 DBMS 구축 및 QGIS 연동 가이드

> 참고 강의: [eduOSGeoSeoul - Lecture-PostGIS](https://github.com/kacgung/eduOSGeoSeoul/blob/main/Lecture-PostGIS/Lecture-PostGIS.md)

---

## 1. PostGIS 환경 준비 (pgAdmin)

### 1.1 서버 등록
브라우저에서 `http://localhost:8070` 접속 후 서버를 등록합니다. (ID: `admin@admin.com` / PW: `admin`)

| 분류 | 항목 | 값 |
|:---:|---|---|
| **General** | Name | `postgis` |
| **Connection** | Host name | `localhost` |
| **Connection** | Port | `5432` |
| **Connection** | Username | `postgres` |
| **Connection** | Password | `postgres` |

### 1.2 데이터베이스 생성 및 확장 설치
`osgeo` 데이터베이스를 생성하고 공간 기능을 활성화합니다.

*   **Database 생성 설정 (Definition 탭)**
    *   **Encoding:** `UTF8`
    *   **Template:** `template0`
    *   **Collation / Character type:** `C` (⚠️ 한글 정렬 및 검색 오류 방지)

*   **PostGIS 확장 설치**
    Query Tool에서 아래 명령어를 실행합니다.
    ```sql
    CREATE EXTENSION postgis;
    ```

### 1.3 설치 확인 ✅
`osgeo` 데이터베이스의 Extensions에 postgis가 정상적으로 추가되었는지 확인합니다.

<img width="1119" height="629" alt="image" src="https://github.com/user-attachments/assets/0432e493-f437-4279-9fb6-db32b1230c09" />

---

## 2. QGIS 연동 설정

QGIS 탐색기 패널에서 **PostgreSQL 우클릭 > 새 연결**을 선택하여 정보를 입력합니다.

| 항목 | 값 |
|:---:|---|
| **이름** | `osgeo` |
| **호스트** | `localhost` |
| **포트** | `5432` |
| **데이터베이스** | `osgeo` |
| **사용자/비밀번호** | `postgres` / `postgres` |

---

## 3. 공간 데이터 업로드 (GUI 방식)

### 3.1 DB 관리자 (단일 레이어)
1. `메뉴 > 데이터베이스 > DB 관리자` 접속
2. `제공자 > PostGIS > osgeo > public` 선택
3. **레이어/파일 불러오기** 클릭 후 `.shp` 파일 선택

### 3.2 공간 처리 툴박스 (일괄 처리)
1. `메뉴 > 공간 처리 > 공간 처리 툴박스`
2. **PostgreSQL로 내보내기** 검색 후 **배치 프로세스**로 실행
3. ⚠️ **"입력 속성의 너비 및 정확도 유지"** 옵션은 반드시 **체크 해제**

---

## 4. 대량 데이터 일괄 업로드 (CLI 방식)

`ogr2ogr`을 사용하여 터미널에서 대량의 데이터를 빠르게 업로드하는 방법입니다.

### 4.1 GDAL 설치 및 확인
macOS 사용자는 brew를 이용해 설치합니다. 설치 후 `ogr2ogr --version`으로 정상 설치를 확인합니다.

<img width="567" height="156" alt="image" src="https://github.com/user-attachments/assets/59f0a4bd-2d43-4d61-8ec6-6285c4ee51b1" />
```bash
# 설치 확인
ogr2ogr --version
```

### 4.2 일괄 업로드 스크립트 실행
데이터가 위치한 디렉토리로 이동하여 아래 쉘 스크립트를 실행합니다. 이 스크립트는 해당 디렉토리의 모든 `.shp` 파일을 찾아 PostGIS에 업로드합니다.

<img width="485" height="314" alt="image" src="https://github.com/user-attachments/assets/a4bb973b-cf45-4ad2-abba-255475fffecb" />

<img width="299" height="464" alt="image" src="https://github.com/user-attachments/assets/670a572b-cafa-4deb-961c-39ea14813599" />

```bash
# 설치파일 경로로 이동 (예시)
cd /Users/유저명/Downloads/data

# .shp 파일 전체 PostGIS 업로드
for f in *.shp; do
  echo "현재 업로드 중: $f"
  ogr2ogr -progress \
    --config PG_USE_COPY YES \
    --config SHAPE_ENCODING CP949 \
    -f PostgreSQL "PG:dbname='osgeo' host=localhost port=5432 user='postgres' password='postgres'" \
    -overwrite \
    -nlt PROMOTE_TO_MULTI \
    -lco GEOMETRY_NAME=geom \
    -lco FID=id \
    -lco PRECISION=NO \
    "$f" \
    -nln "public.${f%.shp}"
done
```

---

## 5. 데이터 인코딩 주의사항

데이터를 올린 후 QGIS에서 한글이 깨지는 경우 아래 설정값을 확인합니다.

| 데이터 종류 | 인코딩 | 좌표계 |
|:---:|:---:|:---:|
| 일반적인 국내 SHP 파일 | `CP949` | `EPSG:5181` 또는 `5186` |
| 국가표준 노드링크 (`road_link`) | `UTF-8` | `EPSG:4326` |

> **Tip:** 레이어 속성 > 소스 > 데이터 소스 인코딩을 `CP949`로 변경하면 한글 깨짐 현상이 해결됩니다.
