---
layout: default
title: MoneyLoop Application Form
parent: Components
nav_order: 1
permalink: /components/api_and_quote
---

# API and Quote <!-- omit in toc -->

The MoneyLoop API allows your software to interface with the MoneyLoop application.

## Table of Contents <!-- omit in toc -->

- [Environments](#environments)
- [Login](#login)
- [Quote](#quote)


## Environments

Use the following host for the environment you wish to utilise.

Testing: https://demonstration.moneyloop.com.au
Production: https://moneyloop.com.au

All requests
headers['Content-Type'] = 'application/json'
headers['Accept']       = 'application/json'
headers['USER_API_TOKEN'] = [Your Token]


## Login

Obtain your username and password from MoneyLoop.

HTTP Post request (USER_API_TOKEN is not required)

```
path = "/api/login"
body = {
  username: @username,
  password: @password
}
```

This will return a json object

```
{ token: [your token]}
```

Note: the token will expire if not used for a period of time.

On expiry a new token will need to be obtained.

## Quote

### Standard Payment Plan Quote

payment_cycle: 0: Fortnightly, 1:Monthly, 3: Weekly

The below will return a payment plan quote for

exposure: $1000.00  # note amount in cents
payment_cycle: Fortnightly
periods: 5          # First payment will be made on day of quote
plan_detail_type:   must always be 1


```
path = "api/quote";
body = {
  exposure: 100000
  payment_cycle: 0
  periods: 5
  plan_detail_type: 1
  payment_cycle: 0
}
```

This will return a json object with two equal arrays

```
 { dates: [array_of_dates], amounts: [array_of_amounts]}

```

### Financial Hardship Payment Plan Quote

In this instance, the customer is able to set a maximum repayment amount per repayment cycle.

A quote will be returned that allows for payment of the exposure, within the customers ability to pay.

```
path = "api/quote";
body = {
  exposure: 100000
  plan_detail_type: 1,
  managed_repayment: 5000,
  payment_cycle: @payment_cycle
}
```

This will return a json object with date and amounts arrays of 20 repayments

```
 { dates: [array_of_dates], amounts: [array_of_amounts]}

```
