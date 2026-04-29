# PostGIS 공간 DBMS 준비하기

> 참고 강의: [eduOSGeoSeoul - Lecture-PostGIS](https://github.com/kacgung/eduOSGeoSeoul/blob/main/Lecture-PostGIS/Lecture-PostGIS.md)

---

## 1. pgAdmin 접속

브라우저에서 접속:

```
http://localhost:8070
```

로그인 정보:
- Email: `admin@admin.com`
- Password: `admin`

---

## 2. 서버 등록

```
좌측 Object Explorer
  > Servers (우클릭)
  > Register
  > Server
```

| 탭 | 항목 | 값 |
|----|------|----|
| General | Name | `postgis` |
| Connection | Host name/address | `localhost` |
| Connection | Port | `5432` |
| Connection | Username | `postgres` |
| Connection | Password | `postgres` |

> **Save** 클릭

---

## 3. 데이터베이스 생성

```
Servers > postgis
  > Databases (우클릭)
  > Create
  > Database...
```

### General 탭

| 항목 | 값 |
|------|----|
| Name | `osgeo` |

### Definition 탭

| 항목 | 값 |
|------|----|
| Encoding | `UTF8` |
| Template | `template0` |
| Collation | `C` |
| Character type | `C` |

> ⚠️ Collation, Character type에 `C` 가 아닌 다른 값을 선택하면  
> 한글 정렬과 검색에서 문제가 생길 수 있으니 주의!

> **Save** 클릭

---

## 4. PostGIS Extension 설치

```
Databases > osgeo 선택
  > 상단 [SQL] 버튼 클릭 (Query 창 열기)
```

Query 창에 입력 후 **F5** 또는 ▶ Run 버튼으로 실행:

```sql
create extension postgis;
```

---

## 5. 설치 확인 ✅

아래 3가지가 확인되면 **공간정보를 담을 준비 완료!**

### ① Extensions에 postgis 추가됨

```
osgeo
  > Extensions
  > postgis  ← 확인
```
<img width="1119" height="629" alt="image" src="https://github.com/user-attachments/assets/0432e493-f437-4279-9fb6-db32b1230c09" />


# QGIS + PostgreSQL(PostGIS) 연동하기


## 1. QGIS에서 PostgreSQL 연결 설정

QGIS 실행 후 탐색기에서 연결 추가:

```
탐색기
  > PostgreSQL (우클릭)
  > 새 연결
```

연결 정보 입력:

| 항목 | 값 |
|------|----|
| 이름 | `osgeo` |
| 호스트 | `localhost` |
| 포트 | `5432` |
| 데이터베이스 | `osgeo` |
| 사용자 | `postgres` |
| 비밀번호 | `postgres` |

> **연결 테스트** 클릭 후 확인 → **확인** 클릭

---

## 2. 공간정보 1개 올리기 (DB 관리자)

```
메뉴 > 데이터베이스 > DB 관리자
  > 제공자 > PostGIS > osgeo > public 선택
  > 레이어/파일 불러오기
```

| 항목 | 값 |
|------|----|
| 입력 (가져올 파일) | `/data/admin_emd.shp` |

> **확인** 클릭

---

## 3. 공간정보 여러 개 올리기 (공간 처리 툴박스)

```
메뉴 > 공간 처리 > 공간 처리 툴박스
  > 검색창에 "PostgreSQL" 입력
  > "PostgreSQL로 내보내기" 선택
  > 배치 프로세스로 실행
```

설정값:

| 항목 | 값 |
|------|----|
| 데이터베이스 (연결 이름) | `osgeo` |
| 입력 레이어 | `/data/admin_sgg.shp`, `/data/admin_sid.shp` |
| 형태 인코딩 | `CP949` |
| 스키마 | `public` |
| 입력 속성의 너비 및 정확도 유지 | ❌ 체크 해제 |

> ⚠️ **"입력 속성의 너비 및 정확도 유지"는 반드시 체크 해제!**

---

## 4. 업로드한 레이어 삭제 (필요시)

```
탐색기 > PostgreSQL > osgeo > public
  > 삭제할 레이어 (우클릭)
  > 관리 > 삭제
```

---

## 5. 데이터 인코딩 확인 주의사항

| 레이어 | 인코딩 | 좌표계 |
|--------|--------|--------|
| 대부분의 shp 파일 | `CP949` (Windows 한글) | `EPSG:5186` |
| `road_link_geographic` | `UTF-8` | `EPSG:4326` |

> QGIS에서 레이어를 열었을 때 한글이 깨지면  
> 레이어 속성 > 소스 > 데이터 소스 인코딩을 `CP949` 로 변경

