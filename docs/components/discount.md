Discounts provide incentives for early payment of payment plans.

Discounts can be set in two ways:

1. Company wide the dashboard
2. On a Payment Plan basis - via the javascript object.

Note: Discounts set on a Payment Plan basis override any company wide settings.

There are two types of discounts

1. Encourage early payment of balance
2. Encourage early payment of periodic payment

Set discounts

JSON

discountOptions.key =

{
  discount_allow_paid_in_full: true/false,
  discount_allow_pay_repayment_early: true/false  


}

Discount JSON Options

discountOptions.key = {};
discountOptions.key.discount_allow_paid_in_full =
  company.discount_allow_paid_in_full;
discountOptions.key.discount_allow_pay_repayment_early =
  company.discount_allow_pay_repayment_early;

if (company.discount_options.discount_allow_paid_in_full != false) {
  const allow_switch = document.getElementById(
    "customDiscountAllowPaidInFull_switch"
  );

  if (allow_switch == null || allow_switch.checked == false) {
    discountOptions.discount_allow_paid_in_full.allow_per_plan_customisation = false;
    // remove custom_discount_percent key
    if (
      discountOptions.discount_allow_paid_in_full.custom_discount_percent
    ) {
      delete discountOptions.discount_allow_paid_in_full
        .custom_discount_percent;
    }
  } else {
    // set custom discount var and percentat
    discountOptions.discount_allow_paid_in_full.allow_per_plan_customisation = true;
    discountOptions.discount_allow_paid_in_full.custom_discount_percent = document.getElementById(
      "discount_allow_paid_in_full_custom"
    ).value;
  }
}

// discount_allow_pay_repayment_early
if (company.discount_options.discount_allow_pay_repayment_early != false) {
  const allow_switch = document.getElementById(
    "customDiscountAllowEarlyRepayments_switch"
  );

  if (allow_switch == null || allow_switch.checked == false) {
    discountOptions.discount_allow_pay_repayment_early.allow_per_plan_customisation = false;
    // remove custom_discount_percent key
    if (
      discountOptions.discount_allow_pay_repayment_early
        .custom_discount_percent
    ) {
      delete discountOptions.discount_allow_pay_repayment_early
        .custom_discount_percent;
    }
  } else {
    // set custom discount var and percentat
    discountOptions.discount_allow_pay_repayment_early.allow_per_plan_customisation = true;
    discountOptions.discount_allow_pay_repayment_early.custom_discount_percent = document.getElementById(
      "discount_allow_early_repayments"
    ).value;
  }
}

return discountOptions;
