# Anleitung zur Erstellung einer ToDo-Listen API mit Swagger Editor und Swagger UI

## Aufgabenbeschreibung

Diese Anleitung führt Sie durch die Erstellung einer API-Dokumentation für eine einfache To-Do-Listen-API. Ziel ist es, die erlernten Techniken zur Erstellung und Visualisierung einer API-Dokumentation anzuwenden.

## Beschreibung der ToDo-Listen App

Die ToDo-Listen App ermöglicht das Verwalten von Aufgaben. Ein ToDo Eintrag besteht aus einer Schlüsselnummer zur Identifikation, einem Titel, einer Beschreibung und einem Status.

### Technischer Überblick eines ToDo Eintrags

Ein ToDo Eintrag besteht aus den folgenden Feldern:

-   **id**: Eine eindeutige Identifikationsnummer (Integer) für den ToDo Eintrag.
-   **title**: Der Titel (String) des ToDo Eintrags.
-   **description**: Eine ausführliche Beschreibung (String) des ToDo Eintrags.
-   **status**: Der Status (String) des ToDo Eintrags. Mögliche Werte sind "open", "in progress" und "done".

## Installation des Swagger Editors

Absolut! Hier ist eine detaillierte Anleitung, wie Sie Swagger Editor lokal mit NPM installieren und mit `npx` verwenden, um einen lokalen Webserver unter verschiedenen Betriebssystemen (einschließlich PowerShell) zu starten. Wir gehen auch auf die Portkonfiguration und die Anpassung des Skript-Pfads (URL) ein.

**Wichtiger Hinweis zur Version:** Die Readme erwähnt zwei Hauptversionen von Swagger Editor: SwaggerEditor@4 (Legacy) und SwaggerEditor@5 (unterstützt OpenAPI 3.1.0). Diese Anleitung konzentriert sich auf die Verwendung von `swagger-editor-dist`, da es abhängigkeitsfrei ist und sich gut für die lokale Ausführung mit `npx` eignet. Die Readme gibt an, dass `swagger-editor-dist` alles Notwendige enthält, um Swagger Editor in einem serverseitigen Projekt oder einem Webprojekt zu bedienen, das npm-Modulabhängigkeiten nicht auflösen kann.

**Voraussetzungen:**

* **Node.js und npm:** Sie benötigen Node.js (Version >=20.3.0) und npm (Node Package Manager, Version >=9.6.7). Npm wird zusammen mit Node.js installiert.
    * **Download:** [https://nodejs.org/](https://nodejs.org/)
    * **Überprüfung der Installation:**
        * Öffnen Sie Ihr Terminal oder Ihre Eingabeaufforderung.
        * Geben Sie `node -v` ein und drücken Sie Enter.
        * Geben Sie `npm -v` ein und drücken Sie Enter.
        Beide Befehle sollten die installierten Versionen anzeigen.

**Schritt-für-Schritt-Anleitung:**

**1. Öffnen des Terminals/der Eingabeaufforderung/PowerShell**

* **Windows:**
    * **Eingabeaufforderung (CMD):** Drücken Sie `Win + R`, geben Sie `cmd` ein und drücken Sie Enter.
    * **PowerShell:** Drücken Sie `Win + R`, geben Sie `powershell` ein und drücken Sie Enter.
* **macOS:**
    * Öffnen Sie den Finder, gehen Sie zu "Programme" > "Dienstprogramme" und doppelklicken Sie auf "Terminal".
    * Alternativ können Sie Spotlight (Cmd + Leertaste) verwenden, "Terminal" eingeben und Enter drücken.
* **Linux:**
    * Die Methode zum Öffnen eines Terminals variiert je nach Linux-Distribution und Desktop-Umgebung. Üblicherweise finden Sie es im Anwendungsmenü unter "Systemwerkzeuge" oder "Zubehör" oder durch Drücken von `Ctrl + Alt + T`.

**2. Erstellen eines Projektverzeichnisses (Optional, aber empfohlen)**

Es ist eine gute Praxis, für jedes Projekt ein eigenes Verzeichnis anzulegen.

```bash
mkdir mein-swagger-projekt
cd mein-swagger-projekt
```

Ersetzen Sie `mein-swagger-projekt` durch Ihren gewünschten Verzeichnisnamen.

**3. Installieren von `swagger-editor-dist`**

Wir installieren `swagger-editor-dist` lokal in unserem Projektverzeichnis. Dies ist der empfohlene Weg, wenn Sie `npx` verwenden möchten, um es auszuführen.

```bash
npm install swagger-editor-dist
```

Dieser Befehl lädt `swagger-editor-dist` herunter und legt es in einem `node_modules`-Ordner in Ihrem aktuellen Verzeichnis ab.

**4. Installieren eines einfachen HTTP-Servers (optional, aber nützlich für `npx`)**

Um die statischen Dateien von `swagger-editor-dist` einfach über `npx` bereitzustellen, können wir einen einfachen HTTP-Server wie `http-server` verwenden. Wenn Sie diesen nicht global installieren möchten, können Sie ihn auch jedes Mal mit `npx` direkt ausführen. Für die Portkonfiguration und das Angeben des Verzeichnisses ist die Installation (global oder lokal als devDependency) manchmal einfacher in der Handhabung.

* **Option A: `http-server` global installieren (einmalig):**
    ```bash
    npm install -g http-server
    ```
* **Option B: `http-server` als Entwicklungsabhängigkeit im Projekt installieren:**
    ```bash
    npm install --save-dev http-server
    ```
    Wenn Sie es so installieren, müssen Sie `npx http-server` verwenden, um es auszuführen.

**5. Starten des Swagger Editors mit `npx`**

`npx` ist ein Werkzeug, das mit npm (ab Version 5.2+) geliefert wird und es Ihnen ermöglicht, Node.js-Pakete auszuführen, ohne sie global oder lokal explizit installieren zu müssen (oder lokal installierte Pakete einfach aufzurufen).

Der `swagger-editor-dist` enthält die notwendigen Dateien, um den Editor im Browser anzuzeigen. Wir müssen einen Webserver starten, der auf das Verzeichnis zeigt, in dem sich die `index.html` von `swagger-editor-dist` befindet. Dieses Verzeichnis ist `node_modules/swagger-editor-dist/`.

* **Befehl zum Starten (wenn `http-server` global installiert ist oder als devDependency im Projekt):**
    ```bash
    http-server ./node_modules/swagger-editor-dist/
    ```
    Oder wenn Sie `http-server` nicht installiert haben und es direkt mit `npx` ausführen möchten:
    ```bash
    npx http-server ./node_modules/swagger-editor-dist/
    ```

Nachdem Sie diesen Befehl ausgeführt haben, sehen Sie in der Konsolenausgabe, auf welcher Adresse und welchem Port der Server läuft (standardmäßig oft `http://localhost:8080` oder `http://127.0.0.1:8080`). Öffnen Sie diese Adresse in Ihrem Webbrowser.

**PowerShell-spezifischer Hinweis:** Die obigen `npm` und `npx` Befehle funktionieren identisch in PowerShell. Achten Sie lediglich darauf, dass PowerShell im richtigen Verzeichnis ausgeführt wird (verwenden Sie `cd` zum Navigieren).

**6. Konfigurieren des Ports**

Viele HTTP-Server, einschließlich `http-server`, ermöglichen die Konfiguration des Ports über einen Kommandozeilenparameter.

* **Mit `http-server`:**
    Verwenden Sie die Option `-p` gefolgt von der gewünschten Portnummer. Zum Beispiel, um den Server auf Port `8888` zu starten:

    ```bash
    # Wenn http-server global oder als devDependency installiert ist
    http-server ./node_modules/swagger-editor-dist/ -p 8888

    # Oder direkt mit npx
    npx http-server ./node_modules/swagger-editor-dist/ -p 8888
    ```
    Der Editor ist dann unter `http://localhost:8888` erreichbar.

**7. Anpassen des Skript-Pfads (URL der API-Definition)**

Swagger Editor kann beim Start eine API-Definition von einer URL laden. Die Readme beschreibt dies primär im Kontext des Docker-Images (`-e URL="..."`).

Wenn Sie `swagger-editor-dist` lokal mit einem einfachen HTTP-Server wie `http-server` ausführen, gibt es mehrere Ansätze, um eine Standard-URL für Ihre API-Definition festzulegen oder eine Definition zu laden:

* **Manuelles Importieren:**
    Der einfachste Weg ist, den Editor zu starten und dann Ihre OpenAPI-Datei (JSON oder YAML) über das Menü "File" > "Import File" oder "File" > "Import URL" zu laden.

* **Query-Parameter `url`:**
    Viele Swagger-UI/Editor-Installationen (einschließlich der online gehosteten Version) unterstützen einen `url` Query-Parameter in der Adresszeile des Browsers. Nachdem Sie Ihren lokalen Server gestartet haben (z.B. auf `http://localhost:8080`), können Sie versuchen, eine URL zu Ihrer API-Definition anzuhängen:

    ```
    http://localhost:8080/?url=https://petstore3.swagger.io/api/v3/openapi.json
    ```
    Oder wenn Ihre Datei lokal über einen anderen Webserver erreichbar ist (oder Sie sie im `swagger-editor-dist` Verzeichnis platzieren und relativ verlinken):
    ```
    http://localhost:8080/?url=/pfad/zu/deiner/api.yaml
    ```
    **Wichtig:** Damit dies mit lokalen Dateien funktioniert, die Sie neben `index.html` ablegen, muss die Datei über den Webserver erreichbar sein. Legen Sie Ihre `openapi.yaml` z.B. in das Verzeichnis `node_modules/swagger-editor-dist/` und verweisen Sie dann mit `http://localhost:8080/?url=openapi.yaml`.

* **Bearbeiten der `index.html` (Fortgeschritten):**
    Sie könnten die `index.html` Datei innerhalb von `node_modules/swagger-editor-dist/` bearbeiten, um die Standard-URL direkt im SwaggerUIBundle-Aufruf zu ändern. Dies ist jedoch **nicht ideal**, da Ihre Änderungen bei einem Update von `swagger-editor-dist` überschrieben werden.
    Suchen Sie in der `index.html` (oder den zugehörigen JavaScript-Dateien) nach der Initialisierung von `SwaggerUIBundle`. Dort gibt es oft eine `spec` oder `url` Option:

    ```javascript
    // Beispielhafter Code-Ausschnitt (kann je nach Version variieren)
    const ui = SwaggerUIBundle({
      // url: "https://petstore.swagger.io/v2/swagger.json", // Ändern Sie diese Zeile
      url: "deine-lokale-api-definition.yaml", // Oder ein anderer Pfad/URL
      dom_id: '#swagger-editor',
      layout: "EditorLayout",
      presets: [
        SwaggerUIBundle.presets.apis,
        SwaggerUIStandalonePreset
      ],
      // ... andere Optionen
    })
    ```
    **Vorsicht:** Diese Methode ist fehleranfällig und nicht update-sicher. Wenn Sie eine dauerhafte Lösung benötigen, ist es besser, eine eigene HTML-Seite zu erstellen, die `swagger-editor-dist` einbindet und konfiguriert, anstatt die Dateien im `node_modules`-Verzeichnis direkt zu ändern.

* **Verwendung der Docker-Methode (wie in der Readme beschrieben):**
    Wenn Sie Docker verwenden, ist die Konfiguration der Standard-URL sehr einfach über Umgebungsvariablen:
    ```bash
    docker run -d -p 80:8080 -e URL="https://deine-api-url/openapi.json" docker.swagger.io/swaggerapi/swagger-editor
    ```
    Oder mit einer lokalen Datei:
    ```bash
    # Stellen Sie sicher, dass Ihre swagger.json im aktuellen Verzeichnis (pwd) liegt
    docker run -d -p 80:8080 -v $(pwd):/tmp -e SWAGGER_FILE=/tmp/swagger.json docker.swagger.io/swaggerapi/swagger-editor
    ```
    Für Windows PowerShell wäre der `-v` Befehl leicht anders (achten Sie auf die Pfadangabe):
    ```powershell
    docker run -d -p 80:8080 -v "${PWD}:/tmp" -e SWAGGER_FILE=/tmp/swagger.json docker.swagger.io/swaggerapi/swagger-editor
    ```

**Zusammenfassung der Befehle (angenommen, Sie sind im Projektverzeichnis):**

1.  **Installation (einmalig pro Projekt):**
    ```bash
    npm install swagger-editor-dist http-server
    ```
    (oder `npm install -g http-server` für globale Installation von http-server)

2.  **Starten des Editors auf Standardport (oft 8080):**
    ```bash
    npx http-server ./node_modules/swagger-editor-dist/
    ```

3.  **Starten des Editors auf einem spezifischen Port (z.B. 8888):**
    ```bash
    npx http-server ./node_modules/swagger-editor-dist/ -p 8888
    ```

4.  **Laden einer API-Definition über URL-Parameter (im Browser):**
    `http://localhost:PORT/?url=IHRE_API_DEFINITION_URL`

Diese Anleitung sollte Ihnen helfen, Swagger Editor erfolgreich lokal für Ihre API-Entwicklung einzurichten und zu nutzen.

## Ziel der OpenAPI Spezifikation

Das Ziel der OpenAPI Spezifikation ist es, eine standardisierte, sprachunabhängige Schnittstelle für REST APIs zu definieren, die sowohl für Menschen als auch für Maschinen lesbar ist. Sie ermöglicht die Automatisierung von API-Dokumentation, Client-SDK-Generierung und Testfällen.

## Implementierung von CRUD Operationen in OpenAPI

Dieser Abschnitt beschreibt die Implementierung von CRUD (Create, Read, Update, Delete) Operationen in einer OpenAPI Spezifikation.

### Create Operation

Die Create Operation wird verwendet, um neue Ressourcen zu erstellen. In einer OpenAPI Spezifikation wird dies typischerweise mit dem `POST` HTTP-Verb auf einem Pfad abgebildet, der die Sammlung der Ressourcen repräsentiert.

**Komponenten:**

-   **path**: Der Pfad, unter dem die Operation verfügbar ist, z.B. `/todos`.
-   **method**: Das HTTP-Verb `POST`.
-   **requestBody**: Definiert die Struktur der Daten, die der Client senden muss, um eine neue Ressource zu erstellen.
    -   **content**: Der Medientyp des Request Body, z.B. `application/json`.
    -   **schema**: Das Schema, das die Struktur des Request Body beschreibt. Dies kann ein Verweis auf ein Schema im `components/schemas` Abschnitt sein.
-   **responses**: Definiert die möglichen Antworten des Servers.
    -   **'201'**: Der HTTP-Statuscode für eine erfolgreiche Erstellung (Created).
        -   **description**: Eine Beschreibung der Antwort.
        -   **content**: Der Medientyp des Response Body, z.B. `application/json`.
        -   **schema**: Das Schema, das die Struktur des Response Body beschreibt. Dies kann ein Verweis auf ein Schema im `components/schemas` Abschnitt sein.

**Beispiel:**

```yaml
paths:
  /todos:
    post:
      summary: Create a new ToDo item
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ToDo'
      responses:
        '201':
          description: Created
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ToDo'
```

### Read Operation

Die Read Operation wird verwendet, um eine oder mehrere Ressourcen abzurufen. In einer OpenAPI Spezifikation wird dies typischerweise mit dem `GET` HTTP-Verb abgebildet. Es gibt zwei typische Anwendungsfälle:

1.  Abrufen aller Ressourcen einer Sammlung.
2.  Abrufen einer spezifischen Ressource anhand ihrer ID.

**Komponenten (Abrufen aller Ressourcen):**

-   **path**: Der Pfad, unter dem die Operation verfügbar ist, z.B. `/todos`.
-   **method**: Das HTTP-Verb `GET`.
-   **responses**: Definiert die möglichen Antworten des Servers.
    -   **'200'**: Der HTTP-Statuscode für eine erfolgreiche Anfrage (OK).
        -   **description**: Eine Beschreibung der Antwort.
        -   **content**: Der Medientyp des Response Body, z.B. `application/json`.
        -   **schema**: Das Schema, das die Struktur des Response Body beschreibt. In diesem Fall ein Array von Ressourcen.

**Komponenten (Abrufen einer spezifischen Ressource):**

-   **path**: Der Pfad, unter dem die Operation verfügbar ist, z.B. `/todos/{id}`.
-   **method**: Das HTTP-Verb `GET`.
-   **parameters**: Definiert die Parameter, die der Client senden kann.
    -   **in**: Der Ort des Parameters, z.B. `path`.
    -   **name**: Der Name des Parameters, z.B. `id`.
    -   **required**: Gibt an, ob der Parameter erforderlich ist.
    -   **schema**: Das Schema, das den Datentyp des Parameters beschreibt.
    -   **description**: Eine Beschreibung des Parameters.
-   **responses**: Definiert die möglichen Antworten des Servers.
    -   **'200'**: Der HTTP-Statuscode für eine erfolgreiche Anfrage (OK).
        -   **description**: Eine Beschreibung der Antwort.
        -   **content**: Der Medientyp des Response Body, z.B. `application/json`.
        -   **schema**: Das Schema, das die Struktur des Response Body beschreibt. In diesem Fall eine einzelne Ressource.

**Beispiel (Abrufen aller Ressourcen):**

```yaml
paths:
  /todos:
    get:
      summary: Retrieve all ToDo items
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/ToDo'
```

**Beispiel (Abrufen einer spezifischen Ressource):**

```yaml
paths:
  /todos/{id}:
    get:
      summary: Retrieve a specific ToDo item by ID
      parameters:
        - in: path
          name: id
          required: true
          schema:
            type: integer
          description: ID of the ToDo item to retrieve
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ToDo'
```

### Update Operation

Die Update Operation wird verwendet, um bestehende Ressourcen zu aktualisieren. In einer OpenAPI Spezifikation wird dies typischerweise mit dem `PUT` HTTP-Verb auf einem Pfad abgebildet, der die spezifische Ressource repräsentiert.

**Komponenten:**

-   **path**: Der Pfad, unter dem die Operation verfügbar ist, z.B. `/todos/{id}`.
-   **method**: Das HTTP-Verb `PUT`.
-   **parameters**: Definiert die Parameter, die der Client senden kann.
    -   **in**: Der Ort des Parameters, z.B. `path`.
    -   **name**: Der Name des Parameters, z.B. `id`.
    -   **required**: Gibt an, ob der Parameter erforderlich ist.
    -   **schema**: Das Schema, das den Datentyp des Parameters beschreibt.
    -   **description**: Eine Beschreibung des Parameters.
-   **requestBody**: Definiert die Struktur der Daten, die der Client senden muss, um die Ressource zu aktualisieren.
    -   **content**: Der Medientyp des Request Body, z.B. `application/json`.
    -   **schema**: Das Schema, das die Struktur des Request Body beschreibt. Dies kann ein Verweis auf ein Schema im `components/schemas` Abschnitt sein.
-   **responses**: Definiert die möglichen Antworten des Servers.
    -   **'200'**: Der HTTP-Statuscode für eine erfolgreiche Aktualisierung (OK).
        -   **description**: Eine Beschreibung der Antwort.
        -   **content**: Der Medientyp des Response Body, z.B. `application/json`.
        -   **schema**: Das Schema, das die Struktur des Response Body beschreibt. Dies kann ein Verweis auf ein Schema im `components/schemas` Abschnitt sein.

**Beispiel:**

```yaml
paths:
  /todos/{id}:
    put:
      summary: Update an existing ToDo item
      parameters:
        - in: path
          name: id
          required: true
          schema:
            type: integer
          description: ID of the ToDo item to update
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ToDo'
      responses:
        '200':
          description: OK
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ToDo'
```

### Delete Operation

Die Delete Operation wird verwendet, um bestehende Ressourcen zu löschen. In einer OpenAPI Spezifikation wird dies typischerweise mit dem `DELETE` HTTP-Verb auf einem Pfad abgebildet, der die spezifische Ressource repräsentiert.

**Komponenten:**

-   **path**: Der Pfad, unter dem die Operation verfügbar ist, z.B. `/todos/{id}`.
-   **method**: Das HTTP-Verb `DELETE`.
-   **parameters**: Definiert die Parameter, die der Client senden kann.
    -   **in**: Der Ort des Parameters, z.B. `path`.
    -   **name**: Der Name des Parameters, z.B. `id`.
    -   **required**: Gibt an, ob der Parameter erforderlich ist.
    -   **schema**: Das Schema, das den Datentyp des Parameters beschreibt.
    -   **description**: Eine Beschreibung des Parameters.
-   **responses**: Definiert die möglichen Antworten des Servers.
    -   **'204'**: Der HTTP-Statuscode für eine erfolgreiche Löschung (No Content).
        -   **description**: Eine Beschreibung der Antwort.

**Beispiel:**

```yaml
paths:
  /todos/{id}:
    delete:
      summary: Delete a ToDo item
      parameters:
        - in: path
          name: id
          required: true
          schema:
            type: integer
          description: ID of the ToDo item to delete
      responses:
        '204':
          description: No Content
```

## HTTP Error Codes

Es ist wichtig, in einer REST API auch Fehlerfälle sauber zu dokumentieren. Hier sind einige gängige HTTP Error Codes, die in einer OpenAPI Spezifikation definiert werden sollten:

-   **400 Bad Request**: Der Server konnte die Anfrage nicht verstehen oder verarbeiten. Dies kann aufgrund von ungültigen Daten, fehlenden Parametern oder anderen Client-seitigen Fehlern auftreten.
-   **401 Unauthorized**: Der Client ist nicht authentifiziert und muss sich zuerst anmelden, um auf die Ressource zugreifen zu können.
-   **403 Forbidden**: Der Client ist authentifiziert, hat aber keine Berechtigung, auf die Ressource zuzugreifen.
-   **404 Not Found**: Die angeforderte Ressource konnte nicht gefunden werden.
-   **500 Internal Server Error**: Ein generischer Fehler, der auftritt, wenn der Server eine unerwartete Bedingung feststellt.

**Beispiel für die Definition von Error Responses in OpenAPI:**

```yaml
responses:
  '400':
    description: Bad Request
    content:
      application/json:
        schema:
          type: object
          properties:
            message:
              type: string
  '404':
    description: Not Found
    content:
      application/json:
        schema:
          type: object
          properties:
            message:
              type: string
  '500':
    description: Internal Server Error
    content:
      application/json:
        schema:
          type: object
          properties:
            message:
              type: string
```

## Content Types

OpenAPI unterstützt verschiedene Content Types, um die Flexibilität bei der Datenübertragung zu gewährleisten. Die gängigsten sind:

-   `application/json`: Standard für JSON-basierte APIs.
-   `application/xml`: Für APIs, die XML verwenden.

**Beispiel für die Definition von Content Types in OpenAPI:**

```yaml
requestBody:
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/ToDo'
responses:
  '200':
    content:
      application/json:
        schema:
          $ref: '#/components/schemas/ToDo'
```

## API Versioning

Die Versionierung von APIs ist wichtig, um Änderungen zu verwalten und die Abwärtskompatibilität zu gewährleisten. In OpenAPI gibt es verschiedene Möglichkeiten, eine API zu versionieren:

1.  **Über den Pfad**: Die Versionsnummer wird im Pfad angegeben, z.B. `/v1/todos`.
2.  **Über den Header**: Die Versionsnummer wird im Header angegeben, z.B. `X-API-Version: 1.0`.

**Beispiel für die Versionierung über den Pfad in OpenAPI:**

```yaml
paths:
  /v1/todos:
    get:
      summary: Retrieve all ToDo items (Version 1)
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/ToDo'
```
## Installation von Swagger UI

Absolut! Hier ist eine umfassende Anleitung zur lokalen Installation und Verwendung von Swagger UI mit NPM/NPX und Docker auf verschiedenen Betriebssystemen, einschließlich PowerShell-spezifischer Hinweise, wo relevant.

## Anleitung: Swagger UI lokal einrichten

Swagger UI ermöglicht es Ihnen, Ihre OpenAPI-Spezifikationen (früher Swagger-Spezifikationen) interaktiv zu visualisieren und zu testen. Hier sind zwei gängige Methoden, um Swagger UI lokal zu betreiben:

**Voraussetzungen:**

1.  **Node.js und NPM:**
    * Stellen Sie sicher, dass Node.js und NPM (Node Package Manager) installiert sind. Sie können dies überprüfen, indem Sie `node -v` und `npm -v` in Ihrer Kommandozeile/Terminal ausführen.
    * Download: [https://nodejs.org/](https://nodejs.org/)
2.  **Docker (für die Docker-Methode):**
    * Installieren Sie Docker Desktop (für Windows/macOS) oder Docker Engine (für Linux).
    * Download: [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

---

### Methode 1: Verwendung von NPM und NPX

Diese Methode verwendet `swagger-ui-dist`, ein NPM-Paket, das alle notwendigen statischen Dateien enthält, um Swagger UI ohne weitere Abhängigkeiten auszuführen. Wir verwenden dann `npx` mit `http-server`, um diese Dateien lokal bereitzustellen.

**Schritt 1: Projektordner erstellen und `swagger-ui-dist` installieren**

1.  Öffnen Sie Ihr Terminal oder Ihre PowerShell.
    * **Linux/macOS:** Terminal
    * **Windows:** Eingabeaufforderung (cmd) oder PowerShell

2.  Erstellen Sie einen neuen Ordner für Ihr Swagger UI-Projekt und wechseln Sie in diesen Ordner:
    ```bash
    mkdir meine-swagger-ui
    cd meine-swagger-ui
    ```
    In PowerShell wären die Befehle identisch.

3.  Installieren Sie `swagger-ui-dist` lokal in diesem Projekt:
    ```bash
    npm install swagger-ui-dist
    ```
    Dadurch wird ein `node_modules`-Ordner erstellt, der `swagger-ui-dist` enthält. Die relevanten Dateien befinden sich in `node_modules/swagger-ui-dist/`.

**Schritt 2: Swagger UI-Dateien vorbereiten**

Die `swagger-ui-dist` liefert eine `index.html`, die Sie direkt verwenden oder anpassen können.

1.  Kopieren Sie die benötigten Dateien aus `node_modules/swagger-ui-dist` in Ihr Hauptprojektverzeichnis (z.B. `meine-swagger-ui`). Dies ist nicht zwingend notwendig, macht aber die Handhabung einfacher, insbesondere wenn Sie die `index.html` anpassen möchten.
    * **Linux/macOS:**
        ```bash
        cp node_modules/swagger-ui-dist/* .
        # Wenn der obige Befehl aufgrund von Wildcard-Problemen nicht alle Dateien kopiert:
        # cp node_modules/swagger-ui-dist/index.html .
        # cp node_modules/swagger-ui-dist/swagger-ui.css .
        # cp node_modules/swagger-ui-dist/swagger-ui-bundle.js .
        # cp node_modules/swagger-ui-dist/swagger-ui-standalone-preset.js .
        # cp node_modules/swagger-ui-dist/favicon-*.png . # etc.
        # Einfacher ist oft, den gesamten Inhalt zu kopieren:
        # cp -R node_modules/swagger-ui-dist/* .
        ```
    * **Windows (Eingabeaufforderung):**
        ```cmd
        xcopy node_modules\swagger-ui-dist\* . /E /I /Y
        ```
    * **Windows (PowerShell):**
        ```powershell
        Copy-Item -Path node_modules\swagger-ui-dist\* -Destination . -Recurse -Force
        ```
    Wenn Sie die Dateien nicht kopieren, müssen Sie später den Pfad für `npx http-server` entsprechend anpassen (`node_modules/swagger-ui-dist`).

**Schritt 3: OpenAPI-Spezifikationsdatei bereitstellen**

Swagger UI benötigt eine OpenAPI-Spezifikationsdatei (z.B. `openapi.json` oder `openapi.yaml`).

1.  Platzieren Sie Ihre Spezifikationsdatei (z.B. `meine-api.yaml`) im selben Verzeichnis (hier: `meine-swagger-ui`).
2.  **Optional:** Wenn Sie möchten, dass Swagger UI standardmäßig Ihre lokale Datei lädt, müssen Sie die `swagger-initializer.js` (die Sie in Schritt 2 kopiert haben) anpassen. Öffnen Sie die `swagger-initializer.js` in einem Texteditor:
    Suchen Sie nach dem `SwaggerUIBundle`-Konfigurationsblock. Er sieht ungefähr so aus:
    ```javascript
    // ...
    window.onload = function() {
      // Begin Swagger UI call region
      const ui = SwaggerUIBundle({
        url: "https://petstore.swagger.io/v2/swagger.json", // << DIESE ZEILE ÄNDERN
        dom_id: '#swagger-ui',
        deepLinking: true,
        presets: [
          SwaggerUIBundle.presets.apis,
          SwaggerUIStandalonePreset
        ],
        plugins: [
          SwaggerUIBundle.plugins.DownloadUrl
        ],
        layout: "StandaloneLayout"
      });
      // End Swagger UI call region
      window.ui = ui;
    };
    // ...
    ```
    Ändern Sie den Wert von `url` auf den Namen Ihrer lokalen Datei:
    ```javascript
    url: "meine-api.yaml", // oder "meine-api.json"
    ```
    Speichern Sie die `swagger-initializer.js`.

**Schritt 4: Lokalen Webserver mit `npx http-server` starten**

`npx` führt NPM-Paket-Binärdateien aus, ohne sie global installieren zu müssen. Wir verwenden `http-server` um die statischen Dateien bereitzustellen.

1.  Stellen Sie sicher, dass Sie sich im Verzeichnis `meine-swagger-ui` befinden, das die `index.html` und andere Swagger-UI-Dateien (sowie optional Ihre `meine-api.yaml`) enthält.
2.  Starten Sie den Server:
    ```bash
    npx http-server
    ```
    Dies startet den Server normalerweise auf Port `8080`. Sie sehen eine Ausgabe wie:
    ```
    Starting up http-server, serving ./
    Available on:
      http://127.0.0.1:8080
      http://[your-local-ip]:8080
    Hit CTRL-C to stop the server
    ```
3.  Öffnen Sie Ihren Webbrowser und navigieren Sie zu `http://127.0.0.1:8080` (oder dem angezeigten Port).

**Port konfigurieren:**

Um einen anderen Port zu verwenden, nutzen Sie die Option `-p`:
```bash
npx http-server -p DEIN_WUNSCHPORT
# Beispiel für Port 8888:
npx http-server -p 8888
```
Dann wäre Swagger UI unter `http://127.0.0.1:8888` erreichbar.

**Pfad zur OpenAPI-Spezifikation (URL) anpassen:**

Es gibt mehrere Wege, die URL zur Spezifikationsdatei anzugeben:

1.  **Wie in Schritt 3 beschrieben:** Direkt in der `swagger-initializer.js` die `url`-Eigenschaft im `SwaggerUIBundle` ändern. Dies ist die robusteste Methode für eine feste lokale Datei.
2.  **Über einen URL-Parameter:** Wenn Sie die `index.html` nicht ändern möchten, können Sie die URL zur Spezifikation auch als Query-Parameter beim Aufruf im Browser übergeben (vorausgesetzt, Ihre Spezifikationsdatei wird auch vom `http-server` bereitgestellt, d.h. sie liegt im selben Verzeichnis oder einem Unterverzeichnis).
    Wenn Ihre `meine-api.yaml` im Stammverzeichnis des Servers liegt, rufen Sie auf:
    `http://127.0.0.1:8080/?url=meine-api.yaml`
    Wenn sie öffentlich erreichbar ist (z.B. auf GitHub Gist), können Sie auch eine externe URL angeben:
    `http://127.0.0.1:8080/?url=https://example.com/pfad/zu/deiner/api.yaml`
3.  **Eingabefeld in Swagger UI:** Standardmäßig zeigt Swagger UI oben ein Eingabefeld an, in das Sie die URL zu Ihrer Spezifikationsdatei eingeben können, nachdem die Seite geladen wurde.

**Hinweise für PowerShell:**
Die Befehle `mkdir`, `cd`, `npm` und `npx` funktionieren in PowerShell identisch wie in anderen Terminals. Der `Copy-Item`-Befehl wurde oben bereits spezifisch für PowerShell gezeigt.

---

### Methode 2: Verwendung von Docker

Docker ist eine hervorragende Methode, um Swagger UI isoliert und mit minimalem Setup auf Ihrem System auszuführen. Swagger API stellt ein offizielles Docker-Image bereit.

**Schritt 1: Docker-Image herunterladen (optional, passiert automatisch beim ersten `run`)**

```bash
docker pull swaggerapi/swagger-ui
```

**Schritt 2: Docker-Container starten**

Der grundlegende Befehl zum Starten ist:
```bash
docker run -p HOST_PORT:CONTAINER_PORT swaggerapi/swagger-ui
```
Swagger UI im Container lauscht standardmäßig auf Port `8080`.

**Beispiel: Swagger UI auf Port 80 Ihres Host-Systems bereitstellen:**
```bash
docker run -d -p 80:8080 swaggerapi/swagger-ui
```
* `-d`: Startet den Container im "detached" Modus (im Hintergrund).
* `-p 80:8080`: Mappt Port `80` Ihres Host-Systems auf Port `8080` im Container. Sie können Swagger UI dann über `http://localhost` (oder `http://localhost:80`) im Browser aufrufen.

**Port konfigurieren:**

Ändern Sie einfach den `HOST_PORT`-Teil im `-p`-Argument:
```bash
# Swagger UI auf Host-Port 8888 bereitstellen
docker run -d -p 8888:8080 swaggerapi/swagger-ui
```
Dann ist Swagger UI unter `http://localhost:8888` erreichbar.

**Pfad zur OpenAPI-Spezifikation (URL) anpassen mit Docker:**

Es gibt mehrere Möglichkeiten, Ihre API-Spezifikation dem Docker-Container bekannt zu machen:

1.  **Über die Umgebungsvariable `URL` (für eine einzelne Spezifikation):**
    Wenn Ihre Spezifikationsdatei online verfügbar ist:
    ```bash
    docker run -d -p 80:8080 -e URL="https://petstore.swagger.io/v2/swagger.json" swaggerapi/swagger-ui
    ```
    Oder wenn Sie eine lokale Datei haben und diese in den Container mounten:
    Angenommen, Ihre `meine-api.yaml` liegt unter `/pfad/zu/deiner/meine-api.yaml` (Linux/macOS) oder `C:\pfad\zu\deiner\meine-api.yaml` (Windows).

    * **Linux/macOS:**
        ```bash
        docker run -d -p 80:8080 \
            -e URL="/usr/share/nginx/html/meine-api.yaml" \
            -v /pfad/zu/deiner/meine-api.yaml:/usr/share/nginx/html/meine-api.yaml \
            swaggerapi/swagger-ui
        ```
        Beachten Sie: Der Pfad in `-e URL` muss der Pfad *innerhalb des Containers* sein, wohin Sie die Datei gemountet haben. Der Standard-Webroot im `swaggerapi/swagger-ui` Image ist oft `/usr/share/nginx/html/`.

    * **Windows (PowerShell oder CMD):**
        Achten Sie auf die korrekte Pfadsyntax für Docker Volumes unter Windows.
        ```powershell
        # PowerShell (Backticks für Zeilenumbrüche)
        docker run -d -p 80:8080 `
            -e URL="/usr/share/nginx/html/meine-api.yaml" `
            -v C:\pfad\zu\deiner\meine-api.yaml:/usr/share/nginx/html/meine-api.yaml `
            swaggerapi/swagger-ui
        ```
        ```cmd
        REM Eingabeaufforderung (Backslashes für Zeilenumbrüche, falls unterstützt, sonst alles in einer Zeile)
        docker run -d -p 80:8080 ^
            -e URL="/usr/share/nginx/html/meine-api.yaml" ^
            -v C:\pfad\zu\deiner\meine-api.yaml:/usr/share/nginx/html/meine-api.yaml ^
            swaggerapi/swagger-ui
        ```
        **Wichtig:** Stellen Sie sicher, dass das Laufwerk (z.B. `C:`) in den Docker Desktop-Einstellungen für "File Sharing" freigegeben ist.

2.  **Über die Umgebungsvariable `URLS` (für mehrere Spezifikationen mit Dropdown-Auswahl):**
    Sie können eine kommagetrennte Liste von URLs oder Namen für URLs angeben.
    ```bash
    docker run -d -p 80:8080 \
        -e URLS="[ \
            { url: 'https://petstore.swagger.io/v2/swagger.json', name: 'Petstore' }, \
            { url: 'https://petstore3.swagger.io/api/v3/openapi.json', name: 'Petstore v3' } \
        ]" \
        swaggerapi/swagger-ui
    ```
    Wenn Sie lokale Dateien mounten, verwenden Sie die Pfade innerhalb des Containers für die `url`-Eigenschaft.

3.  **Eine eigene `swagger-config.json` oder `index.html` mounten:**
    Sie können eine eigene Konfigurationsdatei oder sogar eine angepasste `index.html` in den Container mounten, um das Standardverhalten zu überschreiben. Dies ist fortgeschrittener und erfordert Kenntnis der Dateistruktur im Docker-Image.
    * **Eigene `index.html` mounten:**
        Angenommen, Sie haben eine `meine-index.html` (die auf Ihre lokale Spezifikationsdatei verweist, die ebenfalls gemountet wird oder bereits in der `index.html` fest codiert ist) unter `/pfad/zu/deiner/meine-index.html`.
        ```bash
        # Linux/macOS
        docker run -d -p 80:8080 \
            -v /pfad/zu/deiner/meine-index.html:/usr/share/nginx/html/index.html \
            # Optional: auch die Spezifikationsdatei mounten, wenn meine-index.html darauf verweist
            -v /pfad/zu/deiner/meine-api.yaml:/usr/share/nginx/html/meine-api.yaml \
            swaggerapi/swagger-ui
        ```
        Dadurch wird die Standard-`index.html` im Container durch Ihre eigene ersetzt.

**Hinweise für PowerShell bei Docker:**
Docker-Befehle sind plattformübergreifend. Die Hauptunterschiede liegen in der Pfadangabe für Volumes (`-v`) und der Verwendung von Escape-Zeichen für Zeilenumbrüche (PowerShell: Backtick ``` ` ```, CMD: Caret `^`).

---

**Zusammenfassung:**

* **NPM/NPX:** Gut für schnelle, unkomplizierte Setups, wenn Sie bereits Node.js verwenden und Flexibilität bei der Anpassung der `index.html` wünschen. Ideal für die Integration in Frontend-Projekte.
* **Docker:** Exzellent für isolierte Umgebungen, einfache Portabilität und wenn Sie Node.js nicht direkt auf Ihrem System installieren möchten oder eine konsistente Umgebung über verschiedene Systeme hinweg benötigen. Die Konfiguration über Umgebungsvariablen ist sehr praktisch.

Wählen Sie die Methode, die am besten zu Ihrem Workflow und Ihren Anforderungen passt!

## Öffnen der OpenAPI Spezifikation in Swagger UI

Unabhängig von der Installationsmethode müssen Sie die OpenAPI Spezifikation in Swagger UI öffnen, um die API-Dokumentation anzuzeigen.

1.  Starten Sie Swagger UI gemäß der Installationsanleitung.
2.  Öffnen Sie Ihren Webbrowser und navigieren Sie zu `http://localhost:8080`.
3.  Geben Sie die URL zu Ihrer OpenAPI Spezifikationsdatei (`openapi.yaml`) in das Textfeld ein und klicken Sie auf "Explore". Alternativ können Sie die Datei auch hochladen.

## Anpassen des Erscheinungsbilds von Swagger UI

Das Erscheinungsbild von Swagger UI kann angepasst werden, um es an Ihre Bedürfnisse anzupassen.

1.  **Konfigurationsoptionen:**

    Swagger UI bietet verschiedene Konfigurationsoptionen, die über die URL-Parameter oder über eine Konfigurationsdatei festgelegt werden können.

    -   `url`: Die URL zur OpenAPI Spezifikationsdatei.
    -   `configUrl`: Die URL zu einer Konfigurationsdatei.
    -   `filter`: Aktiviert die Filterung von Operationen und Tags.
    -   `displayOperationId`: Zeigt die Operation-IDs an.
    -   `defaultModelsExpandDepth`: Setzt die Standardtiefe, bis zu der Models erweitert werden.
    -   `defaultModelExpandDepth`: Setzt die Standardtiefe, bis zu der ein Model erweitert wird.
    -   `docExpansion`: Setzt die Standarderweiterung für die Dokumentation ("none", "list", "full").

2.  **Beispiel:**

    Um Swagger UI mit der OpenAPI Spezifikationsdatei `openapi.yaml` und aktivierter Filterung zu starten, verwenden Sie den folgenden Befehl:

    ```bash
    swagger-ui-dist --url openapi.yaml --filter
    ```

## Testen der API Endpunkte mit Swagger UI

Swagger UI ermöglicht es, die API Endpunkte direkt im Browser zu testen.

1.  **Auswählen eines Endpunkts:**

    Klicken Sie auf einen Endpunkt, um die Details anzuzeigen.

2.  **Eingabe von Parametern:**

    Geben Sie die erforderlichen Parameter ein.

3.  **Ausführen der Anfrage:**

    Klicken Sie auf "Try it out!" und dann auf "Execute", um die Anfrage auszuführen.

4.  **Anzeigen der Antwort:**

    Die Antwort wird unterhalb des "Execute"-Buttons angezeigt.