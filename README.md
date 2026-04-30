# 🏢 INNOCEAN France — Attendance Tracking System
### Suivi des présences / 출퇴근 분석 시스템

> **Automated employee attendance analysis tool** built for internal HR management.  
> **Outil d'analyse des entrées/sorties** développé pour la gestion RH interne.  
> 직원 출입 로데이터를 기반으로 출퇴근 현황을 자동 분석하는 웹 애플리케이션입니다.

🌐 **Trilingual interface** — 🇰🇷 한국어 / 🇬🇧 English / 🇫🇷 Français  
🔒 **100% client-side** — no server, no database, no data ever leaves the browser

---

## ✨ Features / Fonctionnalités / 주요 기능

### 📊 Global Dashboard / Tableau de bord / 전체 대시보드
- Employee count, late rate, avg net hours, hour deficit days, match rate
- Nombre d'employés, taux de retards, heures nettes moyennes
- 직원 수, 지각 비율, 평균 실근무시간, 근무부족일, 매칭률

### 📋 Daily Attendance Log / Journal quotidien / 일별 출퇴근
- Auto-calculates arrival (first badge) and departure (last badge) per day
- Detects late arrivals, early departures, **working hour deficits**
- Calcul automatique arrivée/départ, détection retards et **déficits horaires**
- 출근(첫 기록)/퇴근(마지막 기록) 자동 계산, 지각·조기퇴근·**★ 실근무 부족분** 감지

### 👤 Individual Dashboard / Fiche individuelle / 직원별 상세
- Daily arrival/departure **timeline chart** with colour-coded anomalies
- **Calendar view** — colour per day (on time / late / early out / deficit)
- Monthly trend chart (late days, early outs, deficits)
- Arrival time **distribution histogram**
- Per-employee **PDF report** (print-ready, in selected language)
- Chronologie quotidienne, calendrier mensuel, PDF par employé
- 일별 타임라인, 월별 캘린더, 출근 분포, PDF 리포트

### 📈 Global Statistics / Statistiques / 전체 통계
- Daily headcount (weekdays only), average by day of week
- **Top 20 avg late minutes** per employee
- **Top 20 cumulative hour deficit** per employee ← identifies underperformers
- Top 20 retards / Top 20 déficits cumulés ← détecte les "tire-au-flanc"
- 지각 Top 20 / 근무부족 Top 20 ← 월급루팡 탐지

### 🖨️ Export / 내보내기
- Per-employee **PDF** report — fully translated in active language
- **CSV** export with all columns (name, badge, date, times, deficit, status)
- PDF par employé traduit, export CSV complet

---

## 📐 Calculation Rules / Règles de calcul / 계산 기준

| Item | Rule |
|------|------|
| Start threshold | 09:30 (all days) |
| End threshold | 18:30 Mon–Thu / **18:00 Friday** |
| Lunch break | 12:30 – 14:00 (excluded from net hours) |
| Required hours | Mon–Thu **7h30** / Fri **7h00** |
| Hour deficit | Required − Actual (positive values only) |

---

## 🚀 How to Use / Utilisation / 사용 방법

**No installation required** — open the HTML file directly in any modern browser.

1. Open `innocean_attendance_v5_deficit.html` in Chrome, Firefox, or Safari
2. Upload the **badge file** (`Badges_Innocean_Final.xlsx`) — drag & drop or click
3. Upload one or more **access log files** — multiple files supported simultaneously
4. Data is analysed and displayed instantly ✅
5. Switch language with the 🇰🇷 / 🇬🇧 / 🇫🇷 buttons at the top right

---

## 📁 Input File Format / Format fichiers / 입력 파일 형식

### Badge file / Fichier badges / 배지 파일
Required columns: `NOM`, `PRÉNOM`, `CODE DECIMAL`, `MATRICULE RH`

### Access log / Données d'accès brutes / 출입 로데이터
Required columns: `Date heure`, `Utilisateur`, `Identifiant`  
→ Extra columns are automatically ignored

---

## 🛠️ Tech Stack / Stack technique / 기술 스택

| Item | Details |
|------|---------|
| Language | HTML5 + Vanilla JavaScript + CSS (single file, no build step) |
| Charts | [Chart.js 4.4](https://www.chartjs.org/) via cdnjs CDN |
| Excel parsing | [SheetJS (xlsx) 0.18](https://sheetjs.com/) via cdnjs CDN |
| Server / DB | **None** — 100% client-side |
| i18n | Built-in translation system — KO / EN / FR |
| Installation | **Not required** — open and go |

---

## 💡 Technical Highlights / Points techniques / 기술적 특징

- **Badge matching** — `Identifiant` (access log) ↔ `CODE DECIMAL` (badge file), with IFR number fallback
- **Net hours** — lunch overlap subtracted dynamically based on actual arrival/departure
- **Friday rule** — different end threshold (18:00 vs 18:30) per day of week
- **Multi-status** — a single day can be simultaneously "late + hour deficit"
- **Variable columns** — auto-adapts to changing column layouts from the security provider
- **XSS protection** — all Excel-sourced data escaped via `esc()` before HTML injection
- **Modular JS** — shared helpers: `renderTags()`, `mkBarChart()`, `initTabs()`, `chartColors()`
- **Trilingual** — `T(key)` translation system, language switch re-renders all UI + charts + PDF

---

## 🔒 Security / Sécurité / 보안

- ✅ No API keys or secrets hardcoded
- ✅ No external data transmission — employee data never leaves the browser
- ✅ No localStorage, cookies, or tracking pixels
- ✅ XSS protection: all user-sourced data sanitised before rendering
- ✅ CDN scripts loaded with `crossorigin` + `referrerpolicy` attributes
- ✅ No `eval()` usage

---

## 👩‍💼 Background / Contexte / 개발 배경

Developed by **Jiyoung PARK**, Junior Office Manager at INNOCEAN France,  
to replace a monthly manual pivot-table workflow and give the HR team  
a complete, actionable, multilingual attendance overview.

Développé par **Jiyoung PARK**, Junior Office Manager chez INNOCEAN France,  
pour automatiser le traitement mensuel des données d'accès (pivot Excel)  
et fournir au service RH un tableau de bord complet et multilingue.

INNOCEAN France의 Junior Office Manager **박지영**이 개발.  
매월 수동으로 진행하던 피벗 테이블 작업을 자동화하고,  
HR 담당자에게 즉시 활용 가능한 3개 국어 출퇴근 분석 도구를 제공하기 위해 제작.

---

## 📸 Overview / Aperçu / 미리보기

```
[Upload badge file + access log(s)]   ← drag & drop, multiple files OK
              ↓
    [Auto badge matching + calculation]
              ↓
┌─────────────────────────────────────────┐
│ 63 employees │ 740 records │ Late: 45%  │
│ Hour deficits: 416 │ Match rate: 97%   │
└─────────────────────────────────────────┘
              ↓
[Daily Log] [Employee Summary] [Statistics] [Unmatched Badges]
              ↓
     [Click employee name → individual dashboard]
  📈 Timeline │ 📅 Calendar │ 📊 Monthly │ 🕘 Distribution │ 📋 Log
              ↓
    [🖨️ PDF report in current language │ 📥 CSV export]
```

---

*Built with ❤️ and [Claude AI](https://claude.ai) — April 2026*
