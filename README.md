📰 Hacker News — Angular + .NET Backend

A full-stack solution that displays the newest Hacker News stories with:
✅ Pagination
✅ Search
✅ Backend caching
✅ Automated tests (FE + BE)
✅ Swagger API
✅ Angular SPA UI

✅ Tech Stack
Layer	Technology
Front-end	Angular 17+, TypeScript
Back-end	ASP.NET Core (.NET 8/9)
Tests (UI)	Karma / Jasmine
Tests (API)	xUnit
API Source	HackerNews Firebase API
✅ Prerequisites
Tool	Version
Node.js	≥ 20.19 (or 22.x recommended)
.NET SDK	≥ .NET 8 / 9
Angular CLI	Installed via npx
PowerShell	For helper scripts
Git	Latest
Chrome	For FE test runner

If Node is outdated, install via NVM

nvm install 22.12.0
nvm use 22.12.0

✅ Project Structure
hn-challenge/
│
├── Hn.Api/               → .NET Backend API
│   ├── Controllers/
│   ├── Services/
│   ├── Tests/
│   ├── Program.cs
│
├── hn-web/               → Angular App
│   ├── src/
│   ├── tests/
│
└── README.md

✅ 1) Clone the repository
git clone <repo-url>
cd hn-challenge

✅ 2) Install & Test Back-end (API)
📦 Restore + Test
dotnet restore
dotnet test


You should see:

TOTAL: X SUCCESS

✅ 3) Run the Back-end API
dotnet run --project Hn.Api


Runs at:

➡ http://localhost:5129

➡ Swagger: http://localhost:5129/swagger

➡ Sample: http://localhost:5129/api/stories?page=1&pageSize=20

✅ 4) Install & Test Front-end (Angular)
📦 Install dependencies
cd hn-web
npm ci

✅ Run FE test suite
npx @angular/cli@latest test --watch=false


You should see:

TOTAL: 5 SUCCESS

✅ 5) Run Front-end UI
npx @angular/cli@latest serve --port 4200 -o


UI will open at:

➡ http://localhost:4200

✅ Shows newest stories
✅ Search (client-side)
✅ Pagination

NOTE: Angular expects API URL to be configured in
hn-web/src/environments/environment.ts

Default:

export const environment = {
  apiBase: "http://localhost:5129/api"
};

✅ 6) One-shot Script (Run both)
.\run-all.ps1


This:
✅ Starts API
✅ Starts Angular

(If file not present, ask — I can provide it)

✅ 7) Deployment Summary

Two options:

✅ Single App Service (Recommended)

→ Angular bundled into API via wwwroot
→ No CORS needed

OR

✅ Split Deployment

API → Azure App Service

FE → Azure Static Web App

Build Angular production:

cd hn-web
npx @angular/cli@latest build --configuration production


Publish API:

dotnet publish Hn.Api -c Release -o publish


Full deploy script available — ask if needed.

✅ 8) Caching Details
Cached	TTL
ID List	2 min
Each Story	10 min

Backend ensures:
✅ Faster loads
✅ Fewer calls to HN API

✅ 9) API Endpoints
Verb	Endpoint	Description
GET	/api/stories?page=1&pageSize=20&query=text	Get newest stories

Supports:
✅ pagination
✅ search (server-side)

Example:

GET /api/stories?page=2&pageSize=30&query=Google

✅ 10) Automated Tests
✅ Backend
dotnet test

✅ Frontend
cd hn-web
npx @angular/cli@latest test --watch=false

✅ 11) Troubleshooting
Issue	Fix
Node error	nvm use 22.12.0
Timeout retrieving HN stories	Retry; HN API often slow
FE cannot reach BE	Check environment.ts -> apiBase
Swagger not loading	Restart API
✅ 12) Known Constraints
Item	Note
No DB	Uses only public HN API
Slow upstream API	Cached to improve
Story URLs sometimes empty	Handled → falls back to discussion link
✅ 13) Architecture

Angular SPA → consumes backend

.NET API → fetches + caches HN data

DI used for HttpClient + services

Unit tests included for both layers

Simplified flow:

Angular → API → HackerNews
                ↓ cache

✅ 14) Component Diagram / ERD

See /docs/ folder (if included)
or ask and I will regenerate.

✅ 15) License

MIT

✅ DONE ✅

Your project is now ready to run locally & test on new developer machines.

If you’d like
✅ Docker Compose
✅ Auto-deploy GitHub Action
✅ Azure ARM/Bicep
✅ Editable architecture PDF

Just ask!
