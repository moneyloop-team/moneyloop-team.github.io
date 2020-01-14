---
layout: default
title: Application Form Widget
nav_order: 2
---

# MoneyLoop Application Form Widget

## Installation

## Example

The form will render in the div

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Application Test</title>

    <!-- Stylesheets -->
    <link
      rel="stylesheet"
      type="text/css"
      href="http://localhost:3001/api/applicationform.css"
      media="screen"
    />
  </head>
  <body>
    <h1>Your Application Form</h1>

    <div id="MLApp"></div>

    <!-- Application form scripts -->
    <script src="http://localhost:3001/api/applicationform.js"></script>

    <!-- Initialise the Application Form -->
    <script>
      renderMLApplication({
        id: "MLApp",
        googleApiKey: [REPLACE WITH YOUR GOOGLE API KEY],
        apiKey: [REPLACE WITH YOUR API KEY],
        exposure: "100"
      });
    </script>
  </body>
</html>
```
