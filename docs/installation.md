---
layout: default
title: Installation
nav_order: 2
permalink: /installation
---

# Installation <!-- omit in toc -->

## Table of Contents <!-- omit in toc -->

- [Requirements](#requirements)
- [Installation - Application Form](#installation_application_form)
- [Installation - Callback Notifications](#installation_callback_notifications)

## Requirements

As a minimum, you will need a MoneyLoop API Key.

To obtain your API Key, browse to http://dashboard.moneyloop.com.au/pages/edit_account or https://demonstration-dashboard.moneyloop.com.au/pages_edit_account for production or demonstration environments.

Select the company you wish to manage, then scroll down the page to the developers section.

There you will see your API Key and your Callback Key.

You will also need a Google Map API Key.

For more information on component-specific requirements, see [components](/components).

## Installation Application Form

Below we show how to integrate the MoneyLoop Application Form into a standard `html` page.

```html

<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>

    <!-- Title and Favicon -->
    <title>MoneyLoop Application Form</title>

    <!-- Meta Tags -->
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />

    <!-- MoneyLoop Components -->
    <script src="https://moneyloop.com.au/api/applicationform.js"></script>

    <!-- MoneyLoop Components - (**recommended**) CSS -->
    <link rel="stylesheet" type="text/css" href="https://moneyloop.com.au/api/applicationform.css"
    />

    <!-- Overide MoneyLoop stylesheet by including your own -->
    <link rel="stylesheet" type="text/css" href="your-stylesheet.css" />

    <!-- Load and Run MoneyLoop Javascript Component -->
    <script>
      document.addEventListener("DOMContentLoaded", () => {

        renderApplyForm();

        async function renderApplyForm() {

          // Select your environment
          const environment = "production";
          //
          let host      = null;
          let dashboard = null

          if (environment == "production") {
            host      = "https://www.moneyloop.com.au";
            dashboard = "https://dashboard.moneyloop.com.au";
          } else {
            host      = "https://demonstration.moneyloop.com.au";
            dashboard = "https://demonstration-dashboard.moneyloop.com.au";
          }

          const api_key   = "XX";  // Your API Key

          // Declare all fields
          let exposure_type = null;
          let exposure      = null;
          let payment_cycle = null;
          let repayment     = null;
          let periods       = null;
          let discount_options = null;
          let dates         = null;
          let amounts       = null;
          let managed       = false;

          /*
            The api_identifier allows you to provide a unique identifier for
            each Application Form request.

            This is used to identify the result of the application from process and to
            continue to provide updates on the lifecycle of the application.

          */
          const api_identifier = "123456789";


          /***************************************************************************/
          /*

          Note: Uncomment examples

          Standard Example: with exposure, payment_cycle & period

          Notes:
          - exposure = $2000
          - payment_cycle = fortnightly
          - First payment made today, then 4 more each fortnightly (plan length of approx 2 months)
          */

          // exposure_type = "dollars"; // 0: dollars, 1: cents
          // exposure      = 2000;      // $2000
          // payment_cycle = 0;         // 0: fortnight, 1: monthly, 2: custom, 3: weekly
          // periods       = 5;

          /***************************************************************************/
          /* Financial Hardship Example: with exposure, payment_cycle & maximum repayment */

          // exposure_type = "dollars"; // 0: dollars, 1: cents
          // exposure      = 2000;      // $2000
          // payment_cycle = 0;         // 0: fortnight, 1: monthly, 2: custom, 3: weekly
          // plan_detail_type: 1,
          // managed   = true;
          // repayment = 50; // $50

          /***************************************************************************/
          /* Custom Example: with Payment schedule and individual payment amounts specified */

          // payment_cycle = 2;        // 0: fortnight, 1: monthly, 2: custom, 3: weekly
          // exposure_type = "cents";  // 0: dollars, 1: cents
          // exposure      = 60025;    // $600.25
          // managed       = true;
          //
          // // Payment Plan schedule
          // dates   = ["2020-11-01", "2020-11-15"];
          // amounts = [30000, 30025]; // must in in cents

          // Set discount options
          // TBD


          // Initialise MLApp
          document.getElementById("MLApp").innerHTML = createMLLoader();

          return await renderMLApplication({

            // *** Required Fields
            url: `${host}/api/applicationform/`,
            host:   host,
            dashboard: dashboard,
            id:     "MLApp",
            method: "api",
            apiKey: api_key,
            api_identifier: api_identifier,
            googleApiKey: "XXXXXXXXXXXXXXXXXX", // Use your Google Map's API Key
            exposure_type: exposure_type,
            exposure: exposure,

            managed: managed,
            repayment: repayment,
            paymentCycle: payment_cycle,
            periods: periods,
            dates: dates,
            amounts: amounts,
            discountOptions: discount_options,

            // Specify Application Form required fields          
            requiredFields: [
              'Full Name',
              'Date of Birth',
              'Country',
              'Mobile Phone Number',
              'Email',
              'Address',
              'Job Title'
            ],

            // Optional - pre-populate data
            firstName: "test firstname",
            lastName:  "test lastname",
            mobileNumber: "0432212713",
            // homeNumber: "0299775976",
            dobDay:   "05",
            dobMonth: "04",
            dobYear:  "2001",
            address: "320 Harris Street, Pyrmont NSW, Australia",
            email:    Date.now() + "@test.com",
            employer: "MoneyLoop",
            salary:   "3",
            residencyStatus: "Yes"
          });
        }
      });
    </script>


  </head>
  <body class="container-fluid page__container">

    <!-- Application form -->
    <div class="w-100 pt-3" id="MLAppContainer">
        <div id="MLApp"></div>
    </div>

  </body>
</html>

```

## Installation Callback Notifications

Callbacks are api notifications that provide updates on the status of Application Form requests.

To enable callbacks, provide a callback url in the MoneyLoop Dashboard, then provide an api_identifier with each Application Form request.

A callback API Notification will be a JSON HTTP Post request, with the body containing a JSON object.

The JSON object contains the api_identifier, the status of the Application and an array of repayments history (if any).

### Example Callback Notification

```
 {"api_identifier"=>"test_api_identifier",
 "status"=>"1",
 "repayments"=>[{"id"=>1349, "status"=>"Approved", "date"=>"2019-12-15T17:38:10.656+11:00", "amount"=>7600}, {"id"=>1360, "status"=>"Dishonoured", "date"=>"2019-12-29T20:15:00.000+11:00", "amount"=>7600}, {"id"=>2340, "status"=>"Dishonoured", "date"=>"2020-01-12T09:15:00.000+11:00", "amount"=>7600}, {"id"=>2341, "status"=>"Dishonoured", "date"=>"2020-01-26T09:15:00.000+11:00", "amount"=>7600}, {"id"=>2637, "status"=>"Approved", "date"=>"2020-02-05T09:15:00.000+11:00", "amount"=>7600}, {"id"=>2641, "status"=>"Approved", "date"=>"2020-02-12T09:15:00.000+11:00", "amount"=>7600}, {"id"=>2642, "status"=>"Dishonoured", "date"=>"2020-02-26T09:15:00.000+11:00", "amount"=>7600}, {"id"=>2643, "status"=>"Approved", "date"=>"2020-03-11T09:15:00.000+11:00", "amount"=>7600}, {"id"=>3152, "status"=>"Dishonoured", "date"=>"2020-03-25T09:15:00.000+11:00", "amount"=>7600}, {"id"=>3330, "status"=>"Approved", "date"=>"2020-03-27T10:39:58.461+11:00", "amount"=>7600}]}
```

### Callback Status Key
- 1 = active
- 2 = paid in full
- 3 = refunded
- 4 = cancelled
- 5 = default
- 6 = suspended
- 10 = Awaiting Customer Acceptance
- 11 = Awaiting Payment Acceptance

### Callback Failure

If a callback fails for any reason, it will be retried on the following schedule.

- 5 minutes from first failure
- 15 minutes from previous failure
- 2 hours from previous failure
- 12 hours from previous failure
- 1 day from previous failure
- 2 days from previous failure
- 7 days from previous failure
- flagged as failed and will no longer be attempted
