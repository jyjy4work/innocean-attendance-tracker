# 🏢 INNOCEAN France — Attendance Tracking System
# Suivi des présences / 출퇴근 분석 시스템

> **Automated employee attendance analysis tool** built for internal HR management.  
> **Outil d'analyse des entrées/sorties des employés** développé pour la gestion RH interne.  
> 직원 출입 로데이터를 기반으로 출퇴근 현황을 자동 분석하는 웹 애플리케이션입니다.

---

## ✨ Features / Fonctionnalités / 주요 기능

### 📊 Global Dashboard / Tableau de bord global / 전체 대시보드
- Employee count, late arrival rate, average working hours
- Nombre d'employés, taux de retards, heures travaillées moyennes
- 직원 수, 지각 비율, 평균 실근무시간 요약 카드

### 📋 Daily Attendance Log / Suivi quotidien / 일별 출퇴근
- Automatic calculation of arrival (first badge) and departure (last badge)
- Detection of late arrivals, early departures, and **working hour deficits**
- Calcul automatique de l'heure d'arrivée (1er badge) et de départ (dernier badge)
- Détection des retards, départs anticipés, **déficit d'heures travaillées**
- 출근(첫 기록) / 퇴근(마지막 기록) 자동 계산
- 지각, 조기퇴근, **★ 실근무 부족분** 자동 감지

### 👤 Individual Employee Dashboard / Fiche individuelle / 직원별 상세 분석
- Daily arrival/departure timeline chart
- Monthly calendar view (color-coded by status)
- Monthly trend chart for late arrivals and hour deficits
- Arrival time distribution histogram
- Timeline quotidien entrée/sortie (graphique)
- Vue calendrier mensuel (couleurs par statut)
- 일별 출퇴근 타임라인 차트
- 월별 캘린더 뷰 (색상으로 상태 표시)
- 월별 지각/근무부족 추이 차트
- 출근 시간대 분포 히스토그램

### 📈 Global Statistics / Statistiques globales / 전체 통계
- Daily attendance count (weekdays only)
- Average attendance by day of week
- Arrival time distribution
- **Top 20 employees by average late minutes**
- **Top 20 employees by cumulative hour deficit** ← identifies underperformers
- Présence par date (jours ouvrés uniquement)
- **Top 20 retards moyens / Top 20 déficits horaires cumulés** ← détecte les "tire-au-flanc"
- 날짜별/요일별 출근 인원
- **지각 Top 20 / 근무부족 Top 20** ← 월급루팡 탐지

### 🖨️ Export / 내보내기
- Per-employee PDF report (built-in print button)
- Full CSV export with all columns
- PDF / impression par employé (bouton intégré)
- 직원별 PDF 인쇄 / 전체 CSV 다운로드

---

## 📐 Calculation Rules / Règles de calcul / 계산 기준

| Item | Rule |
|------|------|
| Start time threshold | 09:30 |
| End time threshold | 18:30 (Mon–Thu) / **18:00 (Friday)** |
| Lunch break | 12:30 – 14:00 (excluded from net hours) |
| Required hours | Mon–Thu **7h30** / Fri **7h00** |
| Hour deficit | Required hours − Actual hours (only when positive) |

---

## 🚀 How to Use / Utilisation / 사용 방법

**No installation required** — runs directly in the browser.  
**Aucune installation requise** — fonctionne directement dans le navigateur.  
**설치 불필요** — 브라우저에서 바로 실행.

1. Open `innocean_attendance_v5_deficit.html` in Chrome, Firefox, or Safari  
   Ouvrir le fichier dans Chrome, Firefox ou Safari  
   브라우저에서 HTML 파일 열기

2. Upload the **badge information file** (`Badges_Innocean_Final.xlsx`) — drag & drop or click  
   Glisser-déposer le fichier badges  
   배지 정보 파일 업로드 (드래그 또는 클릭)

3. Upload one or more **raw access log files** — multiple files supported  
   Glisser-déposer les fichiers de données d'accès brutes (plusieurs fichiers possibles)  
   출입 로데이터 파일 업로드 (여러 개 동시 가능)

4. Data is analyzed and displayed automatically ✅  
   Les données s'affichent automatiquement ✅  
   데이터 자동 분석 완료 ✅

---

## 📁 Input File Format / Format des fichiers d'entrée / 입력 파일 형식

### Badge file / Fichier badges / 배지 정보 파일
Required columns: `NOM`, `PRÉNOM`, `CODE DECIMAL`, `MATRICULE RH`  
Colonnes requises : `NOM`, `PRÉNOM`, `CODE DECIMAL`, `MATRICULE RH`  
필수 컬럼 : `NOM`, `PRÉNOM`, `CODE DECIMAL`, `MATRICULE RH`

### Raw access log / Données d'accès brutes / 출입 로데이터
Required columns: `Date heure`, `Utilisateur`, `Identifiant`  
Colonnes requises : `Date heure`, `Utilisateur`, `Identifiant`  
필수 컬럼 : `Date heure`, `Utilisateur`, `Identifiant`  
→ Extra columns are automatically ignored / Les colonnes supplémentaires sont ignorées / 나머지 컬럼은 자동 무시

---

## 🛠️ Tech Stack / Stack technique / 기술 스택

| Item | Details |
|------|---------|
| Language | HTML5 + Vanilla JavaScript (CSS included) |
| Charts | [Chart.js 4.4](https://www.chartjs.org/) |
| Excel parsing | [SheetJS (xlsx) 0.18](https://sheetjs.com/) |
| Server / DB | **None** — 100% client-side, no data ever leaves the browser |
| Installation | **Not required** — open the HTML file and go |

---

## 💡 Technical Highlights / Points techniques notables / 기술적 특징

- **Badge matching**: links `Identifiant` (access log) ↔ `CODE DECIMAL` (badge file) with IFR number fallback
- **Net hours calculation**: automatically subtracts lunch break based on actual overlap
- **Friday rule**: different departure threshold (18:00 vs 18:30) applied per day of week
- **Multi-status detection**: a single day can be flagged as both "late" and "hour deficit" simultaneously
- **Variable column formats**: auto-adapts to changing column layouts from the security provider
- **XSS protection**: all Excel-sourced data is escaped before HTML rendering
- **Liaison `Identifiant` ↔ `CODE DECIMAL`** avec fallback IFR
- **Déduction automatique** de la pause déjeuner selon le chevauchement réel
- **Protection XSS** : toutes les données lues depuis Excel sont échappées avant insertion HTML
- 배지 매칭: `Identifiant` ↔ `CODE DECIMAL` 연결, IFR 번호 폴백 처리
- 실근무 계산: 점심시간 실제 겹침 구간 자동 차감
- XSS 보안 처리: 엑셀 데이터 HTML 삽입 전 특수문자 이스케이프

---

## 👩‍💼 Background / Contexte / 개발 배경

Developed by **Jiyoung PARK**, Junior Office Manager at INNOCEAN France,  
to automate a manual monthly process (Excel pivot tables)  
and provide the HR team with a complete, actionable attendance overview.

Développé par **Jiyoung PARK**, Junior Office Manager chez INNOCEAN France,  
pour automatiser un processus manuel (tableau croisé dynamique Excel mensuel)  
et fournir au service RH une vue complète et actionnable des présences.

INNOCEAN France의 Junior Office Manager **박지영**이 개발.  
매월 수동으로 진행하던 피벗 테이블 작업을 자동화하고,  
HR 담당자에게 즉시 활용 가능한 출퇴근 분석 도구를 제공하기 위해 제작.

---

## 📸 Overview / Aperçu / 미리보기

```

[Upload badge file + access log files]
↓
[Auto badge matching & calculation]
↓
┌──────────────────────────────────────┐
│ 63 employees | 740 records | 45% late│
│ 333 hour deficits | 97% matched      │
└──────────────────────────────────────┘
↓
[Daily Log] [Employee Summary] [Statistics] [Unmatched Badges]
↓
[Click employee name → Individual dashboard]
📈 Timeline | 📅 Calendar | 📊 Monthly trend | 🕘 Distribution | 📋 Log
↓
[🖨️ Print PDF report / CSV download]

```
[배지 파일 + 로데이터 업로드]
        ↓
[자동 매칭 & 계산]
        ↓
┌─────────────────────────────────┐
│ 직원 63명 | 출근 740건 | 지각 45% │
│ 근무부족 333건 | 매칭률 97%      │
└─────────────────────────────────┘
        ↓
[일별 출퇴근] [직원 요약] [전체 통계] [미매칭 배지]
        ↓
[직원 이름 클릭 → 개인 상세 대시보드]
  📈 타임라인 | 📅 캘린더 | 📊 월별 추이 | 🕘 분포 | 📋 기록
        ↓
[🖨️ PDF 리포트 출력 / CSV 다운로드]
```

---

*Built with ❤️ and Claude AI — April 2026*
