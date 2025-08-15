# Week 34 – CI/CD Intro

## 🔨 Praktiska övningar

### 🟢 Lätt – Skapa en enkel CI-pipeline
1. Skapa eller klona ett JavaScript/React-projekt.
2. Skapa mappen `.github/workflows/` i projektets rot.
3. Lägg till en fil `ci.yml` med följande innehåll:
    ```yaml
    name: CI

    on:
      push:
        branches: [ "main" ]
      pull_request:
        branches: [ "main" ]

    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v3
          - name: Use Node.js
            uses: actions/setup-node@v3
            with:
              node-version: '18'
          - run: npm install
          - run: npm test
    ```
4. Committa och pusha till GitHub.
5. Kontrollera pipelinen under fliken **Actions**.

---

### 🟠 Medel – Lägg till kodgranskning i flödet
1. Skapa en ny branch `feature/my-change`.
2. Gör en kodändring.
3. Skicka en Pull Request mot `main`.
4. Kontrollera att pipelinen körs automatiskt på PR:en.

---

### 🔴 Svår – Utöka pipelinen med fler steg
1. Lägg till ett steg för att köra `npm run build` efter testerna.
2. Lägg till ett steg som kör `eslint .` för att linta koden.
3. Gör en commit och pusha.
4. Kontrollera att alla steg körs och att pipelinen blir grön.
