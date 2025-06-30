# Softwarespezifikation

**Projektname:** PromptMaster  
**Team:** Marvin Petschulat, Mattis Wellenbüscher  


---

## 1. Einleitung

- **Ziel:** Entwicklung einer App zur KI-gestützten Generierung und Bewertung von Prompts  
- **Plattformen:** Flutter-App (Frontend), Node.js-Backend (Express), Supabase (PostgreSQL), Firebase (Login)

---

## 2. Backend: Technischer Überblick

**Architektur:**  
Das Backend basiert auf **Node.js mit Express**.  
Die zentrale Datei ist `src/index.js`, von dort aus werden Routen wie `authRoutes.js` uvm. geladen.

**Wichtige Komponenten:**
- **PostgreSQL (Supabase gehostet):** Datenbankzugriff über `pg`, Verbindung via `SUPABASE_CONNECTION_STRING`
- **JWT-basierte Authentifizierung**
- **Social Logins:** GitHub und Google via Firebase SDK und GitHub OAuth
- **E-Mail-Funktion:** SMTP-Versand über `nodemailer`
- **Externe LLM-API:** Anbindung an OpenRouter mittels `axios`
- **Gamification:** XP, Level, Badges – inkl. eigener Logik zur Vergabe und Abfrage

**Verwendete Technologien:**
- Node.js 20, Express
- PostgreSQL über Supabase
- JWT, Firebase Admin SDK, GitHub OAuth
- Nodemailer, Axios
- ESLint für Codequalität
- OpenRouter API für KI-gestützte Bewertungen


**Entscheidungen:**
- Supabase wird **nur** als PostgreSQL-Host genutzt
- Authentifizierung und Mail-Logik **selbst implementiert**, nicht über Supabase-Features
- Firebase für Google und GitHub Login, da einfacher zu integrieren. Eigene Logik via Email und Passwort mit JWT-Token-Handling integriert.

---

## 3. Frontend: Technischer Überblick

**Architektur:**  
Flutter-Projekt mit logischer Trennung in Screens, Services, Widgets

**Besonderheiten:**
- **Firebase-Login** (Google, GitHub)
- **Backend-Kommunikation:** HTTP zu `localhost:3000/api`, definiert in `lib/services/config.dart`
- **Serviceklassen:** z. B. `UserService`, `AIService` für API-Kommunikation
- **Datenhaltung:** SharedPreferences bzw. Web Storage
- **UI:** Login, Dashboard, Aufgabenliste, Profilansicht

**Deployment:**  
- Firebase Hosting (`firebase.json`)
- Kein direkter Supabase-Zugriff vom Frontend (auch nicht im Code referenziert)


---

## 4. Abweichungen vom Pflichtenheft (falls zutreffend)

| Bereich             | Vorgabe im Pflichtenheft     | Implementierter Stand                          | Abweichung |
|---------------------|-------------------------------|--------------------------------------------------|------------|
| Authentifizierung   | Supabase-Auth                 | Eigene Implementierung + Firebase (Google, Github) + Custom JWT                           | Ja         |
| Datenbank           | PostgreSQL                    | PostgreSQL über Supabase                        | Nein       |
| E-Mail-Verifizierung| Supabase optional             | Eigene Lösung via Nodemailer                    | Ja         |
| Bewertung           | LLM-gestützt (OpenAI etc.)    | Via OpenRouter API                              | Nein       |
| Gamification        | XP, Level, Badges             | Vollständig implementiert                       | Nein       |

---

## 5. Wer hat was umgesetzt?

| Name                | GitHub-Username | Martikelnummer | Verantwortliche Module / Features                                                                                                                  |
|---------------------|------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Mattis Wellenbüscher | Venneqz          | 1326693             | XP/Level-System, Bewertungs-API, OpenRouter-Anbindung, UI-Elemente (Dashboard, Fortschritt), Flutter CI-Optimierung, Badge-System, Prompt-Historie, Premium-Routen, Level-Logik, Frontend-Initialisierung |
| Marvin Petschulat    | MVBeats          | 1326680              | Auth-Services, Firebase-Google/GitHub-Login, Passwort-Reset, Mail-Logik, Flutter-Login-Screens, Backend-Initialisierung und Struktur, Datenbank-Einrichtung, Dokumentation |



---

