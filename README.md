# 🏢 Attendance Reporting Tool — INNOCEAN France
### Rapport mensuel de présence / 월간 출퇴근 리포트 자동화 도구

> A single-file web app that turns the monthly badge-access export into a ready-to-use working-time report.  
> Une application web (un seul fichier) qui transforme l'export mensuel des badges en rapport de temps de travail.  
> 출입 시스템의 월간 원본 데이터를 바로 쓸 수 있는 근무시간 리포트로 바꿔 주는 단일 파일 웹 앱입니다.

🌐 **Trilingual interface** — 🇰🇷 한국어 / 🇬🇧 English / 🇫🇷 Français  
🔒 **100% client-side** — no server, no database, no data ever leaves the browser

---

## 🎯 What · Why · Result / Quoi · Pourquoi · Résultat / 무엇 · 왜 · 결과

| | |
|---|---|
| **What** | Reads the existing access-control export and the badge list, matches them, and produces a monthly working-time report (dashboard, PDF, CSV). It collects **no new data**. |
| **Why** | The monthly report was built by hand in Excel pivot tables — slow, repetitive and error-prone. |
| **Result** | Adopted by the team for monthly reporting: preparation time went from **~10 minutes to ~10 seconds**. |

- **Quoi** — Exploite l'export existant du contrôle d'accès ; aucune nouvelle donnée collectée.  
- **Pourquoi** — Le rapport mensuel était fait à la main (tableaux croisés dynamiques).  
- **Résultat** — Utilisé par l'équipe pour le reporting mensuel : de ~10 minutes à ~10 secondes.

- **무엇** — 기존 출입 기록 파일을 그대로 읽어 월간 근무시간 리포트를 만듦(새로운 데이터 수집 없음)  
- **왜** — 매월 엑셀 피벗 테이블로 수작업하던 보고 업무를 자동화하기 위해  
- **결과** — 팀이 월간 보고에 실제 채택, 작업 시간 약 10분 → 약 10초

---

## ✨ Features / Fonctionnalités / 주요 기능

### 📊 Overview / Vue d'ensemble / 전체 현황
- Headcount, average net hours, days below the required schedule, badge match rate
- Effectif, heures nettes moyennes, jours sous l'horaire requis, taux de correspondance
- 인원 수, 평균 실근무시간, 기준 시간 미달일, 배지 매칭률

### 📋 Daily log / Journal quotidien / 일별 기록
- Arrival = first badge, departure = last badge, lunch break deducted automatically
- Flags late arrivals, early departures and hours below the required schedule
- 첫 출입 = 출근, 마지막 출입 = 퇴근, 점심시간 자동 차감 / 지각·조기퇴근·기준 시간 미달 표시

### 👤 Individual view / Fiche individuelle / 개인별 화면
- Timeline, monthly calendar, arrival-time distribution
- Individual **PDF report** in the selected language
- 타임라인, 월별 캘린더, 출근 시간 분포, 언어별 PDF 리포트

### 📈 Team statistics / Statistiques d'équipe / 팀 통계
- Daily headcount (weekdays), average by day of week, monthly trends
- Summaries by employee for HR follow-up
- 일별 인원, 요일별 평균, 월별 추이, HR 확인용 직원별 요약

### 🖨️ Export / 내보내기
- PDF report per employee (translated) · full CSV export

---

## 📐 Calculation rules / Règles de calcul / 계산 기준

| Item | Rule |
|------|------|
| Start threshold | 09:30 (all days) |
| End threshold | 18:30 Mon–Thu / **18:00 Friday** |
| Lunch break | 12:30 – 14:00 (excluded from net hours) |
| Required hours | Mon–Thu **7h30** / Fri **7h00** |
| Hours below schedule | Required − Actual (positive values only) |

---

## 🚀 How to use / Utilisation / 사용 방법

**No installation required** — open the HTML file in any modern browser.

1. Open `innocean_attendance_v5_deficit.html` in Chrome, Firefox or Safari
2. Upload the **badge list** (`.xlsx`) — drag & drop or click
3. Upload one or more **access-log exports**
4. The report is generated instantly ✅
5. Switch language with 🇰🇷 / 🇬🇧 / 🇫🇷 (top right)

### Input files / Fichiers d'entrée / 입력 파일
- Badge list — columns `NOM`, `PRÉNOM`, `CODE DECIMAL`, `MATRICULE RH`
- Access log — columns `Date heure`, `Utilisateur`, `Identifiant` (extra columns ignored)

---

## 🛠️ Tech stack / Stack technique / 기술 스택

| Item | Details |
|------|---------|
| Language | HTML5 + Vanilla JavaScript + CSS (single file, no build step) |
| Charts | [Chart.js 4.4](https://www.chartjs.org/) via cdnjs |
| Excel parsing | [SheetJS (xlsx) 0.18](https://sheetjs.com/) via cdnjs |
| Server / DB | **None** — 100% client-side |
| i18n | Built-in `T(key)` system — KO / EN / FR |

### Technical highlights
- **Badge matching** — access-log `Identifiant` ↔ badge `CODE DECIMAL`, with fallback
- **Net hours** — lunch overlap subtracted from actual arrival/departure
- **Friday rule** — different end threshold per day of week
- **Variable columns** — adapts to layout changes in the security provider's export
- **Trilingual** — language switch re-renders UI, charts and PDF

---

## 🔒 Privacy & security / Confidentialité / 개인정보·보안

- ✅ Everything runs locally in the browser — no upload, no storage, no cookies, no tracking
- ✅ No API keys or secrets in the code
- ✅ XSS protection: all Excel-sourced data escaped before rendering
- ✅ No `eval()`; CDN scripts loaded with `crossorigin` + `referrerpolicy`
- ✅ **No real employee data in this repository**

---

## 👩‍💼 Background / Contexte / 개발 배경

Built by **Jiyoung PARK** (Corporate Services, INNOCEAN France) to automate a recurring monthly reporting task.  
Développé par **Jiyoung PARK** (Corporate Services, INNOCEAN France) pour automatiser un reporting mensuel récurrent.  
INNOCEAN France 경영지원(Corporate Services) 소속 **박지영**이 반복되는 월간 보고 업무를 자동화하기 위해 개발.

---

*Built with [Claude AI](https://claude.ai) — April 2026*
