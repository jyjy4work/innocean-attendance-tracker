# 🏢 INNOCEAN France — Suivi des présences / 출퇴근 분석 시스템

> **Outil d'analyse des entrées/sorties des employés** développé pour la gestion RH interne.  
> 직원 출입 로데이터를 기반으로 출퇴근 현황을 자동 분석하는 웹 애플리케이션입니다.

---

## ✨ Fonctionnalités / 주요 기능

### 📊 Tableau de bord global / 전체 대시보드
- Nombre d'employés, taux de retards, heures travaillées moyennes
- 직원 수, 지각 비율, 평균 실근무시간 요약 카드

### 📋 Suivi quotidien / 일별 출퇴근
- Calcul automatique de l'heure d'arrivée (1er badge) et de départ (dernier badge)
- Détection des retards, départs anticipés, **déficit d'heures travaillées**
- 출근(첫 기록) / 퇴근(마지막 기록) 자동 계산
- 지각, 조기퇴근, **★ 실근무 부족분** 자동 감지

### 👤 Fiche individuelle / 직원별 상세 분석
- Timeline quotidien entrée/sortie (graphique)
- Vue calendrier mensuel (couleurs par statut)
- Évolution mensuelle des retards et déficits
- Distribution des heures d'arrivée
- 일별 출퇴근 타임라인 차트
- 월별 캘린더 뷰 (색상으로 상태 표시)
- 월별 지각/근무부족 추이 차트
- 출근 시간대 분포 히스토그램

### 📈 Statistiques globales / 전체 통계
- Présence par date (jours ouvrés uniquement)
- Moyenne de présence par jour de semaine
- Distribution des horaires d'arrivée
- **Top 20 retards moyens par employé**
- **Top 20 déficits horaires cumulés** ← détecte les "tire-au-flanc"
- 날짜별/요일별 출근 인원
- **지각 Top 20 / 근무부족 Top 20** ← 월급루팡 탐지

### 🖨️ Export / 내보내기
- PDF / impression par employé (bouton intégré)
- Export CSV avec toutes les colonnes
- 직원별 PDF 인쇄 / 전체 CSV 다운로드

---

## 📐 Règles de calcul / 계산 기준

| 항목 | 기준 |
|------|------|
| 출근 기준 | 09:30 |
| 퇴근 기준 | 18:30 (월~목) / **18:00 (금요일)** |
| 점심시간 | 12:30 – 14:00 (실근무에서 제외) |
| 소정근무 | 월~목 **7h30** / 금 **7h00** |
| 실근무 부족분 | 소정근무 − 실근무 (양수일 때만) |

---

## 🚀 Utilisation / 사용 방법

**Aucune installation requise / 설치 불필요** — fonctionne directement dans le navigateur.

1. Ouvrir `innocean_attendance_v5_deficit.html` dans Chrome, Firefox ou Safari  
   `innocean_attendance_v5_deficit.html` 파일을 브라우저에서 열기

2. Glisser-déposer (ou cliquer) le fichier **배지 정보** (`Badges_Innocean_Final.xlsx`)  
   배지 정보 파일 업로드 (드래그 또는 클릭)

3. Glisser-déposer les fichiers de **données d'accès brutes** (plusieurs fichiers possibles)  
   출입 로데이터 파일 업로드 (여러 개 동시 가능)

4. Les données s'affichent automatiquement / 데이터 자동 분석 완료 ✅

---

## 📁 Format des fichiers d'entrée / 입력 파일 형식

### Fichier badges / 배지 정보 파일
Colonnes requises : `NOM`, `PRÉNOM`, `CODE DECIMAL`, `MATRICULE RH`  
필수 컬럼 : `NOM`, `PRÉNOM`, `CODE DECIMAL`, `MATRICULE RH`

### Données d'accès brutes / 출입 로데이터
Colonnes requises : `Date heure`, `Utilisateur`, `Identifiant`  
필수 컬럼 : `Date heure`, `Utilisateur`, `Identifiant`  
→ Les colonnes supplémentaires sont ignorées / 나머지 컬럼은 자동 무시

---

## 🛠️ Stack technique / 기술 스택

| 항목 | 내용 |
|------|------|
| 언어 | HTML5 + Vanilla JavaScript (CSS 포함) |
| 차트 | [Chart.js 4.4](https://www.chartjs.org/) |
| 엑셀 파싱 | [SheetJS (xlsx) 0.18](https://sheetjs.com/) |
| 서버/DB | **없음** — 100% 클라이언트 사이드 |
| 설치 | **불필요** — 브라우저에서 바로 실행 |

---

## 💡 Points techniques notables / 기술적 특징

- **Badge matching** : liaison `Identifiant` (log) ↔ `CODE DECIMAL` (badge) avec fallback IFR
- **Calcul net** : déduction automatique de la pause déjeuner selon le chevauchement réel
- **Règle vendredi** : seuil de départ différent (18:00 vs 18:30) selon le jour de semaine
- **Détection multi-statut** : un jour peut être simultanément "지각 + 근무부족"
- **Formats variables** : le système s'adapte automatiquement aux variations de colonnes du prestataire de sécurité

---

## 👩‍💼 Contexte / 개발 배경

Développé par **Jiyoung PARK**, Junior Office Manager chez INNOCEAN France,  
pour automatiser un processus manuel (tableau croisé dynamique Excel mensuel)  
et fournir au service RH une vue complète et actionnable des présences.

INNOCEAN France의 Junior Office Manager **박지영**이 개발.  
매월 수동으로 진행하던 피벗 테이블 작업을 자동화하고,  
HR 담당자에게 즉시 활용 가능한 출퇴근 분석 도구를 제공하기 위해 제작.

---

## 📸 Aperçu / 미리보기

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
