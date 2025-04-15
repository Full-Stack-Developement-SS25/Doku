# Anforderungs- und Entwurfsspezifikation ("Pflichtenheft")

# Titelseite

**Produktname:** PromptMaster  
**Autoren:** [Name 1], [Name 2]  
**Link zum Source Code Repository:** Wird nach Projektstart eingetragen

**Inhaltsverzeichnis:**  
* 1 Einführung  
* 2 Anforderungen  
  * 2.1 Stakeholder  
  * 2.2 Funktionale Anforderungen  
  * 2.3 Nicht-funktionale Anforderungen  
  * 2.4 Graphische Benutzerschnittstelle  
  * 2.5 Anforderungen im Detail  
* 3 Technische Beschreibung  
  * 3.1 Systemübersicht  
  * 3.2 Softwarearchitektur  
  * 3.3 Schnittstellen  
  * 3.4 Datenmodell  
  * 3.5 Abläufe  
  * 3.6 Entwurf  
  * 3.7 Fehlerbehandlung  
  * 3.8 Validierung  
* 4 Projektorganisation  
  * 4.1 Annahmen  
  * 4.2 Verantwortlichkeiten  
  * 4.3 Grober Projektplan  
* 5 Anhänge  
  * 5.1 Glossar  
  * 5.2 Referenzen  
  * 5.3 Index  

# 1 Einführung

## 1.1 Beschreibung

"PromptMaster" ist eine mobile iOS-Lernanwendung, die Nutzer:innen Schritt für Schritt das sogenannte Prompt Engineering beibringt. Die App vermittelt den effektiven Umgang mit textbasierten KI-Modellen (Large Language Models, kurz: LLMs), wie sie z. B. in Chatbots oder Schreibassistenten eingesetzt werden. Nutzer:innen erhalten zunehmend komplexere Aufgaben und müssen passende Prompts formulieren, um die KI zu einer Lösung zu führen. Die Qualität der Ergebnisse wird durch eine Bewertung, Feedback und Hinweise zu Verbesserungspotenzialen reflektiert.

Zusätzlich bietet die App ein Gamification-System mit Leveln, Abzeichen und optionalen Challenges. Eine Account-Funktion sowie ein Score-System ermöglichen Nutzer:innen Fortschritte zu speichern und sich mit anderen zu vergleichen. In der Basisversion ist die Nutzung begrenzt – eine Monetarisierung erfolgt über ein Abo-Modell.

Die App richtet sich an ein breites Publikum: Schüler:innen, Studierende, Berufstätige und Bildungseinrichtungen. Durch gezielte Schulung in KI-Kompetenzen wird ein gesellschaftlich zunehmend relevanter Bereich zugänglich gemacht.

# 2 Anforderungen

## 2.1 Stakeholder

| Funktion / Relevanz                         | Name             | Kontakt / Verfügbarkeit                   | Wissen                                      | Interessen / Ziele                               |
|---------------------------------------------|------------------|-------------------------------------------|---------------------------------------------|---------------------------------------------------|
| Nutzer:innen / Zielgruppe                   | Allgemein        | jederzeit erreichbar (App-User)           | Lernwillig, unterschiedliche Vorkenntnisse  | Bessere Prompter werden, Spaß beim Lernen        |
| Bildungseinrichtungen                       | Schulen, Unis    | unterschiedlich                           | möchten moderne Kompetenzen vermitteln      | Motivation & KI-Kompetenz fördern                |
| KI-Dienstleister (z. B. OpenAI, HuggingFace)| Drittanbieter    | abhängig von API-Nutzung                  | Zugriff auf LLMs                            | Integration ihrer Dienste, faire Nutzung         |
| Entwickler:innen (Team)                     | [Name 1, Name 2] | jederzeit                                  | kennen Anforderungen & Architektur          | Projekt erfolgreich umsetzen, Note erhalten      |

## 2.2 Funktionale Anforderungen

- Nutzer:innen können sich registrieren, einloggen und ihr Profil verwalten
- Es gibt aufgabenbasierte Lerneinheiten, die nach Schwierigkeit gestaffelt sind
- Nutzer:innen können Prompts eingeben, um Aufgaben zu lösen
- KI gibt eine Antwort auf den Prompt zurück
- Die Antwort wird auf relevante Schlüsselbegriffe geprüft und bewertet
- Nutzer:innen erhalten Feedback & Verbesserungshinweise
- Punkte/XP werden vergeben; Fortschritt wird gespeichert
- Es gibt Level, Abzeichen, tägliche/wöchentliche Challenges
- Scoreboard vergleicht Nutzer:innen
- Aufgaben sind limitiert, erweiterbar durch Abo-Modell

## 2.3 Nicht-funktionale Anforderungen

### 2.3.1 Rahmenbedingungen

- iOS-kompatibel (aktuelle Versionen)
- Flutter als Framework
- Backend basiert auf Node.js mit REST API
- Datenbank: PostgreSQL

### 2.3.2 Betriebsbedingungen

- Internetzugang nötig für LLM-Funktionalität
- Lokaler Cache für Aufgaben möglich
- Eingeschränkte Offline-Funktion

### 2.3.3 Qualitätsmerkmale

Qualitätsmerkmal     | sehr gut | gut | normal | nicht relevant
---------------------|----------|-----|--------|----------------
Zuverlässigkeit      |    X     |     |        |       
Fehlertoleranz       |    X     |     |        |       
Wiederherstellbarkeit|    X     |     |        |       
Ordnungsmäßigkeit    |    X     |     |        |       
Richtigkeit          |    X     |     |        |       
Konformität          |          |  X  |        |       
Benutzerfreundlichkeit|         |     |        |       
Installierbarkeit    |          |     |   X    |       
Verständlichkeit     |    X     |     |        |       
Erlernbarkeit        |          |  X  |        |       
Bedienbarkeit        |          |  X  |        |       
Zeitverhalten        |          |     |   X    |       
Effizienz            |          |     |        |   X    
Analysierbarkeit     |    X     |     |        |       
Modifizierbarkeit    |          |     |        |   X    
Stabilität           |    X     |     |        |       
Prüfbarkeit          |    X     |     |        |       

## 2.4 Graphische Benutzerschnittstelle

Die graphische Benutzerschnittstelle wird mit Flutter realisiert und ist für iOS optimiert. Die Screens orientieren sich am typischen Flow einer Lern-App.

### Screens

#### Startscreen
- Optionen: Einloggen, Registrieren
- Weiterleitung zum Dashboard nach erfolgreicher Anmeldung
- Verknüpfte User Story:
  - | Als | möchte ich | so dass | Akzeptanz |
    |-----|------------|---------|------------|
    | Nutzer | mich einloggen | ich auf meine persönlichen Lernfortschritte zugreifen kann | Login funktioniert bei gültigen Zugangsdaten |

#### Dashboard / Übersicht
- Anzeige von Level, XP, Fortschritt
- Verfügbare Aufgaben des Tages/Woche
- Zugang zu bisherigen Ergebnissen und Profil
- Verknüpfte User Stories:
  - Zugriff auf Aufgaben
  - Überblick über Lernstand

#### Aufgaben-Screen
- Aufgabenstellung wird angezeigt
- Prompt-Eingabefeld
- „Senden“-Button zur Bewertung
- KI-Antwort erscheint unterhalb
- Bewertung + Feedback erscheint nach KI-Antwort
- Verknüpfte User Stories:
  - Prompteingabe und Feedback
  - Bewertung auf Basis von Keywords

#### Scoreboard / Vergleich
- Anzeige von Highscores (global oder Freunde)
- Optionaler Filter: Zeitraum, Level
- Verknüpfte User Story:
  - Motivation durch Vergleich mit anderen

#### Profil / Einstellungen
- Account-Details, Fortschritt, Statistiken
- Abo-Modell / Limitanzeige / Upgrade-Möglichkeit

### Navigation
Die Navigation erfolgt über ein tab-basiertes Bottom-Navigation-Menü:
- Dashboard | Aufgaben | Scoreboard | Profil

Ein Zustandsdiagramm zur Navigation folgt in Kapitel 3.5 Abläufe.

---

## 2.5 Anforderungen im Detail

### Strukturierte User Stories

| **Als** | **möchte ich** | **so dass** | **Akzeptanz** |
|--------|----------------|-------------|----------------|
| Nutzer | mich registrieren und einloggen | ich meinen Lernfortschritt speichern kann | Konto wird erfolgreich erstellt oder angemeldet |
| Nutzer | eine Aufgabe sehen und bearbeiten | ich üben kann, Prompts zu schreiben | Aufgabe wird angezeigt und KI-Antwort erscheint |
| Nutzer | Feedback zu meiner Eingabe erhalten | ich daraus lernen kann | Bewertung und Hinweise erscheinen nach KI-Antwort |
| Nutzer | Punkte und Level aufsteigen | ich motiviert bleibe | Fortschrittsanzeige funktioniert |
| Nutzer | mich mit anderen vergleichen | ich sehen kann, wie gut ich bin | Scoreboard ist sichtbar |
| Nutzer | Aufgaben auch später erneut ansehen können | ich mein Lernen reflektieren kann | Verlauf und Historie ist zugänglich |
| Nutzer | täglich neue Aufgaben erhalten | ich regelmäßig übe | Aufgaben rotieren täglich |
| Nutzer | eine Upgrade-Option sehen | ich entscheiden kann, ob ich mehr Funktionen nutze | Upgrade-Möglichkeit klar angezeigt |
| Nutzer | bei zu schlechten Prompts einen Hinweis erhalten | ich gezielter verbessern kann | Verbesserungshinweise erscheinen bei <50 % Score |

# 3 Technische Beschreibung

## 3.1 Systemübersicht

Das System folgt einem klassischen Client-Server-Modell und nutzt eine 3-Schichten-Architektur.

### Box-and-Arrow-Diagramm (textuell beschrieben):

- **Flutter App (Client)**  
  ↓ HTTP/HTTPS (REST, JSON)  
- **Backend (Node.js / Express.js)**  
  ↓ PostgreSQL (SQL)  
- **Datenbank (PostgreSQL via Supabase oder eigene Instanz)**

Datenformate: JSON für Client-Server-Kommunikation  
Protokolle: HTTPS / REST-API

## 3.2 Softwarearchitektur

### Server (Backend)

- **Web-Schicht:** REST API via Express.js
- **Logik-Schicht:** Bewertung, Keyword-Analyse, Benutzerlogik
- **Persistenz-Schicht:** Datenbank-Anbindung via ORM (z. B. Prisma)

### Client (Frontend – Flutter App)

- **View-Schicht:** UI-Screens (Dart / Flutter Widgets)
- **Logik-Schicht:** State Management (Provider / Riverpod)
- **Kommunikation-Schicht:** HTTP-Client für API-Calls

### 3.2.1 Technologieauswahl

| Komponente | Technologie |
|------------|-------------|
| Frontend | Flutter (Dart) |
| Backend | Node.js, Express.js |
| API | REST, JSON |
| Datenbank | PostgreSQL |
| Auth | Supabase Auth oder eigener JWT-Service |
| Hosting | Render, Railway oder Supabase |
| DevOps | GitHub + GitHub Actions |
| Testing | Jest (Backend), Flutter-Test (Frontend) |

## 3.3 Schnittstellen

### Externe Schnittstellen

| Ziel | Methode | Pfad | Beschreibung |
|------|---------|------|--------------|
| Aufgaben abrufen | GET | /api/tasks | Gibt zufällige/niveauabhängige Aufgaben zurück |
| Prompt senden | POST | /api/prompt | Bewertet einen Prompt auf Basis der Aufgabenstellung |
| Authentifizierung | POST | /api/auth/login | Login via Email & Passwort |
| Benutzerinfo | GET | /api/user/me | Gibt Nutzerdaten & Fortschritt zurück |
| Scoreboard | GET | /api/scores | Top-Listen für Level & XP |

### Interne Schnittstellen

- Bewertungsmodul <-> Promptanalysemodul
- DB-Layer <-> ORM-Schicht

## 3.3.1 Ereignisse

Nicht Event-gesteuert im engeren Sinne, aber intern:
- Prompt gesendet → Bewertung → Feedback generiert
- Neue Aufgabe gestartet → Fortschritt gespeichert

## 3.4 Datenmodell

### Analyseklassendiagramm (textuell beschrieben)

- **User**
  - id, email, password_hash, level, xp, created_at
- **Task**
  - id, title, description, difficulty
- **Prompt**
  - id, user_id, task_id, content, score, feedback, timestamp
- **ScoreboardEntry**
  - user_id, level, total_score

(Diagramm als ER-Diagramm optional visualisierbar)

## 3.5 Abläufe

### Beispiel-Aktivitätsdiagramm (vereinfacht, textuell)

**Use Case: Aufgabe bearbeiten**
1. Aufgabe wird angezeigt
2. Nutzer gibt Prompt ein
3. Prompt wird an Backend gesendet
4. Backend gibt Bewertung + KI-Antwort + Feedback zurück
5. Fortschritt wird gespeichert
6. Feedback und Score werden angezeigt

**Use Case: Login**
1. Nutzer öffnet App
2. Gibt Zugangsdaten ein
3. App schickt Daten an /api/auth/login
4. Token wird gespeichert
5. Weiterleitung zum Dashboard

## 3.6 Entwurf

UML-Diagramme zu Modulen (optional) – empfohlen:
- TaskController
- PromptEvaluator
- AuthService

## 3.7 Fehlerbehandlung

| Fehler | Beschreibung | Lösung |
|--------|--------------|--------|
| 401 Unauthorized | Ungültiger Token / Login | Login erneut durchführen |
| 500 Internal Server Error | z. B. Bewertungsmodul nicht erreichbar | Retry mit Hinweis |
| Invalid Prompt | Kein Inhalt oder zu kurz | Fehlerhinweis anzeigen |
| DB Down | PostgreSQL nicht erreichbar | Infoanzeige + Retry-Versuch |

## 3.8 Validierung

### Integrationstestfälle

| Komponente | Testziel |
|------------|----------|
| API /prompt | Bewertung erfolgt korrekt bei Keyword-Erkennung |
| API /tasks | Gibt Aufgabe abhängig vom Level zurück |
| UI | Scoreanzeige reagiert auf Fortschritt |
| Auth | Registrierung & Login mit Token funktioniert |

Verknüpfung mit User Story IDs optional ergänzbar.

# 4 Projektorganisation

## 4.1 Annahmen

- Das Produkt wird ausschließlich für iOS-Geräte entwickelt (iPhone/iPad)
- Flutter wird verwendet, da es Cross-Platform-fähig ist (für spätere Erweiterungen)
- Das Backend wird mit Node.js und Express implementiert
- PostgreSQL wird als relationale Datenbank verwendet
- Supabase wird für Hosting, Auth und ggf. Datenbank genutzt
- Keine kostenpflichtigen APIs werden verwendet (z. B. OpenAI nur bei Free-Tier)
- Bewertung der Prompts erfolgt lokal über Keyword-Logik
- Entwicklung erfolgt auf Mac mit Xcode und Flutter SDK

### Interne Qualitätsanforderungen

- Sauberer, gut dokumentierter Code
- Erweiterbarkeit und Wartbarkeit der Module
- Gute Trennung von Logik, UI und Datenzugriff
- Automatisierte Tests für kritische Pfade

## 4.2 Verantwortlichkeiten

| Softwarebaustein | Person(en) |
|------------------|------------|
| Flutter Frontend | [Name A] |
| Node.js Backend  | [Name B] |
| Datenbankmodell  | [Name B] |
| GUI-Design / Mockups | [Name A] |
| Testing / Dokumentation | beide gemeinsam |

### Rollen

| Name | Rolle |
|------|-------|
| [Name A] | Frontend-Entwickler, GUI, Mockups |
| [Name B] | Backend-Entwickler, Datenmodell |
| beide | Tester, Dokumentation |

## 4.3 Grober Projektplan

### Meilensteine

| KW | Aufgabe |
|----|---------|
| KW 16 | Abschluss Softwarespezifikation (Pflichtenheft) |
| KW 17 | Projektsetup + Repo-Struktur |
| KW 18 | Grundgerüst Frontend & Backend, erste API-Calls |
| KW 19 | Aufgabenverwaltung, Promptbewertung, Login |
| KW 20 | Bewertung + Feedback, Score-System |
| KW 21 | Gamification (Levels, Abzeichen, Leaderboard) |
| KW 22 | Tests & Fehlerbehandlung, Code Freeze |
| KW 23 | Präsentation & Demo, Abgabe |

# 5 Anhänge

## 5.1 Glossar

| Begriff | Bedeutung |
|--------|-----------|
| LLM | Large Language Model – ein KI-Modell, das natürliche Sprache versteht und erzeugt |
| Prompt | Texteingabe an ein LLM, um eine gewünschte Antwort zu erhalten |
| Flutter | Framework zur plattformübergreifenden App-Entwicklung (Google, Sprache: Dart) |
| REST | Architekturstil für APIs, bei dem Ressourcen über HTTP-Methoden angesprochen werden |
| API | Application Programming Interface – Schnittstelle zur Kommunikation zwischen Systemen |
| Supabase | Backend-as-a-Service-Plattform mit PostgreSQL, Authentifizierung und Hosting |
| Gamification | Motivationsstrategie durch spieltypische Elemente (Level, XP, Abzeichen) |
| Scoreboard | Anzeige von Nutzer:innen-Rankings auf Basis ihrer Leistungen in der App |

## 5.2 Referenzen

- Datenschutzgrundverordnung (DSGVO), abrufbar unter: https://eur-lex.europa.eu/legal-content/DE/TXT/?uri=CELEX%3A32016R0679
- Flutter: https://flutter.dev
- Node.js: https://nodejs.org
- Supabase: https://supabase.com
- PostgreSQL: https://www.postgresql.org
- Prompt Engineering Guide: https://github.com/dair-ai/Prompt-Engineering-Guide

## 5.3 Index

- Abo-Modell → Kapitel 1.1, 2.2, 4.1  
- Authentifizierung → Kapitel 2.2, 3.3  
- Backend → Kapitel 3.2, 4.2  
- Bewertungssystem → Kapitel 2.2, 3.4  
- Flutter → Kapitel 3.2.1, 4.1  
- Gamification → Kapitel 1.1, 2.2, 3.5  
- GUI-Mockups → Kapitel 2.4  
- Keyword-Analyse → Kapitel 2.2, 3.2  
- Prompt → Kapitel 1.1, 2.2, 3.3  
- Scoreboard → Kapitel 2.2, 2.4, 3.3  
- User Story → Kapitel 2.5  

