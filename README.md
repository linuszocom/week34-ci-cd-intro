# Week 34 – CI/CD Intro (Wednesday)

## 🔨 Praktiska övningar

### 🟢 Lätt – Skapa en minimal CI-pipeline
1. Skapa eller klona ett JavaScript/React-projekt.
2. Skapa mappen `.github/workflows/` i projektets rot.
3. Lägg till en fil `ci.yml` med följande innehåll:
    ```yaml
    name: CI

    on:
      push:
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

### 🟠 Medel – Lägg till branch-triggers och manuellt flöde
1. Ändra `on:`-delen i pipelinen så att den även körs på `develop`-branch.
2. Lägg till ett manuellt körningsalternativ med:
    ```yaml
    workflow_dispatch:
    ```
3. Pusha ändringen och testa att köra pipelinen manuellt från GitHub.

---

### 🔴 Svår – Utöka pipelinen med fler bygg- och teststeg
1. Lägg till ett steg som kör `npm run build` efter testerna.
2. Lägg till ett steg som kör `eslint .` för att linta koden.
3. Se till att pipelinen misslyckas om linter hittar fel.
4. Pusha ändringarna och kontrollera att alla steg körs.
