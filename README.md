# fundamentals of web apps

## notes
- images are fetched as they are met by the browser while rendering the document received as `Response` from the server.
  - other assets-stylesheets, scripts--are fetched in the same way.
- requests are typed: `document`, `script`, `stylesheet`, `xhr`


## new note diagram

```mermaid
sequenceDiagram

participant user

participant browser

participant server



user->>browser: create note: "hello note app"

browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note body="note='hello note app'"

activate server

Note left of server: /new_note creates a new note and adds it to the list of notes

server->>browser: 302 redirect to https://studies.cs.helsinki.fi/exampleapp/notes

deactivate server



browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes

activate server

server-->>browser: HTML document

deactivate server



browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css

activate server

server-->>browser: stylesheet

deactivate server



browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js

activate server

server-->>browser: script

deactivate server



Note right of browser: execution of the JavaScript code begins to fetch notes from the server



browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json

activate server

server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]

deactivate server



Note right of browser: The browser calls the callback function to render the notes

browser->>user: formatted list of notes with new note appended
```

## spa diagram

```mermaid
sequenceDiagram

participant browser
participant server


browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa

activate server

server-->>browser: HTML document

deactivate server



browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css

activate server

server-->>browser: stylesheet

deactivate server



browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js

activate server

server-->>browser: SPA Javascript file

deactivate server


Note right of browser: execution of the JavaScript code begins to fetch notes from the server



browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json

activate server

server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]

deactivate server



Note right of browser: The browser calls the callback function to render the notes

```


## new note with spa diagram

```mermaid
sequenceDiagram

participant user

participant browser

participant server



user->>browser: create note: "hello note app"

Note left of browser: Browser calls onsubmit callback of form

browser->>user: formatted list of notes with new note appended

browser->>server: POST /new_note {"content":"hello note app", "date":"some date"}

activate server

Note left of server: /new_note creates a new note and adds it to the server's list of notes

server->>browser: 201 Created

deactivate server
```
