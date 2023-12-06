``` mermaid
sequenceDiagram
  participant b as Browser
  participant s as Server

  b ->>+ s: GET https://studies.cs.helsinki.fi/exampleapp/spa
  s -->>- b: Send `spa.html` document
  Note right of b: The CSS & JS files are linked in HTML's header, enabling their retrieval & integration into the webpage

  b ->>+ s: GET https://studies.cs.helsinki.fi/exampleapp/main.css
  s -->>- b: Send `main.css` file

  b ->>+ s: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
  s -->>- b: Send `spa.js` file
  Note right of b: The browser executes `spa.js`, fetches `data.json` from the server

  b ->>+ s: GET https://studies.cs.helsinki.fi/exampleapp/data.json
  s -->>- b: Send `data.json` file
  Note right of b: The browser executes the callback function by `xhttp.onreadystatechange`

  b ->> b: Parse data from `data.json` to `notes` array in client-side
  b ->> b: Execute `redrawNotes()`, replace old `ul` with new `ul` containing new data from `notes` array in client-side
  Note right of b: The browser renders updates during callback execution
```
