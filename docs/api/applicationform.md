---
layout: default
title: Application Form Widget
parent: API Documentation
nav_order: 2
---

# MoneyLoop Application Form Widget <!-- omit in toc -->

## Table of Contents <!-- omit in toc -->

- [Requirements](#requirements)
- [Installation](#installation)
- [Rendering the Application Form](#rendering-the-application-form)
- [Styling](#styling)
- [Example](#example)

---

The MoneyLoop application widget embeds our application form into a `div` element of your choice.
It is easy to install and our default styling can be overwritten.

## Requirements

We ask that you have a [Google Maps](https://developers.google.com/maps/documentation) account first.

## Installation

To install, download the script and css files into your `html` page:

```html
<script src="https://moneyloop.com.au/api/applicationform.js"></script>
```

If you want styling (**recommended**), also download our stylesheet:

```html
<link
  rel="stylesheet"
  type="text/css"
  href="https://moneyloop.com.au/api/applicationform.css"
/>
```

## Rendering the Application Form

Once you have downloaded the script (and stylesheet), you can call `renderMLApplication` to render the application form inside a HTML element of your choice.
You are also able to add optional fields to "pre-populate" the application form.

The arguments `renderMLApplication` takes are provided below.

| Argument       | Description                                                                                         | Required? |
| :------------- | :-------------------------------------------------------------------------------------------------- | :-------- |
| `id`           | The id of the HTML element you want the application form to be inside of.                           | Yes       |
| `googleApiKey` | Your Google Maps API key. If you have already imported the Google Maps script, just enter `'false'` | Yes       |
| `apiKey`       | Your MoneyLoop API Key                                                                              | Yes       |
| `exposure`     | The exposure amount your customer is facing.                                                        | Yes       |
| `firstName`    | Your customer's first name.                                                                         | No        |
| `lastName`     | Your customer's last name.                                                                          | No        |

A basic example of this is:

```javascript
  renderMLApplication({
    id: "MLApp",
    googleApiKey: [REPLACE WITH YOUR GOOGLE API KEY],
    apiKey: [REPLACE WITH YOUR API KEY],
    exposure: "100"
  });
```

## Styling

You can overload our stylesheet with your own by including our stylesheet before yours:

```html
<link
  rel="stylesheet"
  type="text/css"
  href="http://localhost:3001/api/applicationform.css"
/>
<link rel="stylesheet" type="text/css" href="/mystylesheet.css" />
```

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
