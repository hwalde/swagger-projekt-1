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

Es gibt zwei Möglichkeiten, den Swagger Editor lokal zu installieren:

### Docker

1.  **Linux / Mac:**

    Öffnen Sie ein Terminal und führen Sie den folgenden Befehl aus:

    ```bash
    docker pull swaggerapi/swagger-editor
    docker run -d -p 80:8080 swaggerapi/swagger-editor
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost`.

2.  **CMD (Windows):**

    Öffnen Sie die Eingabeaufforderung und führen Sie die folgenden Befehle aus:

    ```cmd
    docker pull swaggerapi/swagger-editor
    docker run -d -p 80:8080 swaggerapi/swagger-editor
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost`.

3.  **PowerShell (Windows):**

    Öffnen Sie PowerShell und führen Sie die folgenden Befehle aus:

    ```powershell
    docker pull swaggerapi/swagger-editor
    docker run -d -p 80:8080 swaggerapi/swagger-editor
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost`.

### npm

1.  **Linux / Mac:**

    Öffnen Sie ein Terminal und führen Sie die folgenden Befehle aus:

    ```bash
    npm install -g swagger-editor
    swagger-editor
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost:8080`.

2.  **CMD (Windows):**

    Öffnen Sie die Eingabeaufforderung und führen Sie die folgenden Befehle aus:

    ```cmd
    npm install -g swagger-editor
    swagger-editor
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost:8080`.

3.  **PowerShell (Windows):**

    Öffnen Sie PowerShell und führen Sie die folgenden Befehle aus:

    ```powershell
    npm install -g swagger-editor
    swagger-editor
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost:8080`.

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

Swagger UI kann auf zwei Arten installiert werden: Docker und npm.

### Docker

Docker ist eine Containerisierungsplattform, die es ermöglicht, Anwendungen in isolierten Umgebungen auszuführen. Dies ist die empfohlene Methode, um Swagger UI zu installieren, da sie einfach und plattformunabhängig ist.

1.  **Linux / Mac:**

    Öffnen Sie ein Terminal und führen Sie den folgenden Befehl aus:

    ```bash
    docker pull swaggerapi/swagger-ui
    docker run -d -p 8080:8080 swaggerapi/swagger-ui
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost:8080`.

2.  **CMD (Windows):**

    Öffnen Sie die Eingabeaufforderung und führen Sie die folgenden Befehle aus:

    ```cmd
    docker pull swaggerapi/swagger-ui
    docker run -d -p 8080:8080 swaggerapi/swagger-ui
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost:8080`.

3.  **PowerShell (Windows):**

    Öffnen Sie PowerShell und führen Sie die folgenden Befehle aus:

    ```powershell
    docker pull swaggerapi/swagger-ui
    docker run -d -p 8080:8080 swaggerapi/swagger-ui
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost:8080`.

### npm

npm ist ein Paketmanager für JavaScript, der es ermöglicht, JavaScript-Bibliotheken und -Tools zu installieren.

1.  **Linux / Mac:**

    Öffnen Sie ein Terminal und führen Sie die folgenden Befehle aus:

    ```bash
    npm install -g swagger-ui-dist
    ```

    Erstellen Sie ein Verzeichnis, in dem Sie Ihre OpenAPI-Spezifikationsdatei (`openapi.yaml`) speichern möchten. Navigieren Sie zu diesem Verzeichnis im Terminal.

    Führen Sie dann den folgenden Befehl aus:

    ```bash
    swagger-ui-dist --url openapi.yaml
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost:8080`.

2.  **CMD (Windows):**

    Öffnen Sie die Eingabeaufforderung und führen Sie die folgenden Befehle aus:

    ```cmd
    npm install -g swagger-ui-dist
    ```

    Erstellen Sie ein Verzeichnis, in dem Sie Ihre OpenAPI-Spezifikationsdatei (`openapi.yaml`) speichern möchten. Navigieren Sie zu diesem Verzeichnis in der Eingabeaufforderung.

    Führen Sie dann den folgenden Befehl aus:

    ```cmd
    swagger-ui-dist --url openapi.yaml
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost:8080`.

3.  **PowerShell (Windows):**

    Öffnen Sie PowerShell und führen Sie die folgenden Befehle aus:

    ```powershell
    npm install -g swagger-ui-dist
    ```

    Erstellen Sie ein Verzeichnis, in dem Sie Ihre OpenAPI-Spezifikationsdatei (`openapi.yaml`) speichern möchten. Navigieren Sie zu diesem Verzeichnis in PowerShell.

    Führen Sie dann den folgenden Befehl aus:

    ```powershell
    swagger-ui-dist --url openapi.yaml
    ```

    Öffnen Sie dann Ihren Webbrowser und navigieren Sie zu `http://localhost:8080`.

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