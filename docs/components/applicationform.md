---
layout: default
title: MoneyLoop Application Form
parent: Components
nav_order: 1
permalink: /components/applicationform
---

# MoneyLoop Application Form <!-- omit in toc -->

The MoneyLoop application widget embeds our application form into a `HTML` element of your choice.
It is easy to install and our default styling can be overwritten.

---

## Table of Contents <!-- omit in toc -->

- [Requirements](#requirements)
- [Rendering the Application Form](#rendering-the-application-form)
  - [Rendering in an `<iframe>` element](#rendering-in-an-iframe-element)
- [Styling](#styling)
- [Example](#example)

---

## Requirements

We ask that you have a [Google Maps](https://developers.google.com/maps/documentation) account first.

---

## Rendering the Application Form

Once you have downloaded the script (and stylesheet), you can call `renderMLApplication` to render the application form inside a HTML element of your choice.
You are also able to add optional fields to "pre-populate" the application form.

The arguments `renderMLApplication` takes are provided below.

| Argument       | Description                                                                                         | Required? |
| :------------- | :-------------------------------------------------------------------------------------------------- | :-------: |
| `id`           | The id of the HTML element you want the application form to be inside of.                           |    ✅     |
| `googleApiKey` | Your Google Maps API key. If you have already imported the Google Maps script, just enter `'false'` |    ✅     |
| `apiKey`       | Your MoneyLoop API Key.                                                                             |    ✅     |
| `exposure`     | The exposure amount your customer is facing.                                                        |    ✅     |
| `firstName`    | Your customer's first name.                                                                         |    ❌     |
| `lastName`     | Your customer's last name.                                                                          |    ❌     |
| `mobileNumber` | Your customer's mobile number.                                                                      |    ❌     |
| `homeNumber`   | Your customer's home number.                                                                        |    ❌     |
| `email`        | Your customer's email.                                                                              |    ❌     |
| `employer`     | Your customer's employer.                                                                           |    ❌     |

A basic example of this is:

```javascript
  renderMLApplication({
    id: "MLApp",
    googleApiKey: [REPLACE WITH YOUR GOOGLE API KEY],
    apiKey: [REPLACE WITH YOUR API KEY],
    exposure: "100"
  });
```

### Rendering in an `<iframe>` element

Rendering the application form inside an iframe is not available, but we are developing a solution for this.
If you want to be one of the first people to know when it will be ready, please [contact us](mailto:hello@moneyloop.com.au)

---

## Styling

You can overload our stylesheet with your own by including our stylesheet before yours:

```html
<link
  rel="stylesheet"
  type="text/css"
  href="http://localhost:3001/api/applicationform.css"
/>
<link rel="stylesheet" type="text/css" href="stylesheet.css" />
```

---

## Example

The form will render in the div

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Application Test</title>

    <!-- Stylesheet -->
    <link
      rel="stylesheet"
      type="text/css"
      href="http://localhost:3001/api/applicationform.css"
    />
  </head>
  <body>
    <div id="MLApp"></div>

    <!-- Application form script -->
    <script src="http://localhost:3001/api/applicationform.js"></script>

    <!-- Render the Application Form -->
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

---
