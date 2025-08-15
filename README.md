# Week 34 – CI/CD Intro (Wednesday)

## 🔨 Praktiska övningar

### 🟢 Lätt – Skapa din första CI-pipeline
Mål: Förstå grunderna i hur GitHub Actions fungerar.

1. Skapa eller klona ett JavaScript/React-projekt (kan vara ett enkelt "Hello World").
2. Skapa en mapp i projektets rot:  
   `.github/workflows/`
3. Inuti den mappen, skapa en fil som heter `ci.yml` och klistra in följande kod:
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
4. Gör en commit och pusha till GitHub.
5. Gå till fliken **Actions** i ditt repo och se om pipelinen körs.
6. Kontrollera att stegen blir **grönmarkerade** och inte visar några fel.

---

### 🟠 Medel – Lägg till fler sätt att starta pipelinen
Mål: Lära hur man styr när pipelinen ska köras.

💡 **Förberedelse:**  
Om du inte redan har en `dev`-branch i ditt repo så skapa en och pusha upp den till ditt repo. 

1. Öppna din `ci.yml` igen.
2. Under `on:`, lägg till att pipelinen även ska köras när kod pushas till `dev`-branchen:
    ```yaml
    on:
      push:
        branches: [ "main", "dev" ]
    ```
3. Lägg även till möjlighet att starta pipelinen manuellt från GitHub-gränssnittet genom att lägga till:
    ```yaml
      workflow_dispatch:
    ```
   Resultatet ska se ut så här:
    ```yaml
    on:
      push:
        branches: [ "main", "dev" ]
      workflow_dispatch:
    ```
4. Committa och pusha ändringarna.
5. Gå till **Actions** → välj din pipeline → klicka på **Run workflow** för att starta manuellt.
6. Bekräfta att pipelinen körs även om du inte pushar ny kod.

---

### 🔴 Svår – Lägg till fler steg och skapa ett "bygg-test-flöde"
Mål: Se hur en pipeline kan bestå av flera steg som körs i ordning.

1. I din `ci.yml`, lägg till ett steg som bygger projektet efter att testerna körts:
    ```yaml
    - run: npm run build
    ```
2. Lägg till ett steg för att kolla kodkvalitet med ESLint:
    ```yaml
    - run: npx eslint .
    ```
3. Om ESLint hittar fel, ska pipelinen misslyckas.
4. Gör en medveten ESLint-varning (t.ex. lägg till en oanvänd variabel) och pusha — bekräfta att pipelinen blir **röd**.
5. Rätta felet och pusha igen — kontrollera att pipelinen blir **grön**.
