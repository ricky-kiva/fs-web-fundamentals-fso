``` mermaid
sequenceDiagram
  participant browser as Browser 
  participant server as Server

  browser ->>+ server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
  server ->> server: Push data {form's payload & current time} to `notes` array within the server
  server -->>- browser: Redirect to /exampleapp/notes (in Response Header `location`)
  Note left of server: Status Code: 302 Found

  browser ->>+ server: GET https://studies.cs.helsinki.fi/exampleapp/notes
  server -->>- browser: Send `notes.html` document
  Note right of browser: The CSS & JS files are linked in HTML's header, enabling their retrieval & integration into the webpage

  browser ->>+ server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
  server -->>- browser: Send `main.css` file

  browser ->>+ server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
  server -->>- browser: Send `main.js` file
  Note right of browser: The browser executes `main.js`, fetches `data.json` from the server

  browser ->>+ server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
  server -->>- browser: Send `data.json` file
  Note right of browser: The browser executes the callback function by `xhttp.onreadystatechange`

  browser ->> browser: Parse & log data from `data.json`
  browser ->> browser: Create an `ul` element, set its class to "notes"
  browser ->> browser: Iterate over parsed data, create `li` elements and append to `ul`
  browser ->> browser: Append `ul` to the element with ID "notes"
  Note right of browser: The browser renders updates during callback execution
```
