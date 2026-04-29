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
| Connection | Host name/address | `postgis` |
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

### ② Functions 수가 700개 이상

```
osgeo
  > Schemas
  > public
  > Functions  ← 700개 이상이면 정상
```

### ③ spatial_ref_sys 테이블 생성됨

```
osgeo
  > Schemas
  > public
  > Tables
  > spatial_ref_sys  ← 확인
```

> `spatial_ref_sys` 는 **좌표계 정보를 담고 있는 매우 중요한 테이블**입니다.  
> EPSG 코드, proj4text 등 좌표계 관련 정보가 담겨 있습니다.

---
