``` mermaid
sequenceDiagram
  participant b as Browser
  participant s as Server

  b ->> b: Prevent form's `onsubmit` default behavior
  b ->> b: Create `note` variable with {form's value & current time}
  b ->> b: Push `note` to `notes` array within the client-side
  b ->> b: Set form's first field value to empty string ("")
  b ->> b: Execute `redrawNotes()`, replace old `ul` with new `ul` containing new data from `notes` array in client-side
  Note right of b: The browser renders updates during callback execution

  b ->>+ s: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
  Note right of b: Request Header's "content type" sets to `application/json`. Payload is `note` converted to JSON string
  s ->> s: Push payload data to `notes` array within the server
  s -->>- b: {message: "note created"}
  Note left of s: Status Code: 201 Created

  b ->> b: Log response text (this.responseText)
```
