# The New You Movement Calorie Calculator

A 7-step calorie and macro calculator for Kim Weston's The New You Movement. It's a single self-contained file (`index.html`), so it can be hosted anywhere static, or pasted into a Custom HTML element.

## Flow

1. **Quiz:** name, age, height, weight (sliders with ft/in, st/lb, cm and kg), activity, goal, then email and phone.
2. **Loading screen:** ticks through the calculation steps.
3. **Results:** daily calorie target, resting rate, maintenance, macros, personalised notes and a CTA.

## Settings

The settings are at the top of the `<script>` block in `index.html`.

- **`DASHBOARD_URL` / `DASHBOARD_CLIENT`:** every submission is posted to the REPS dashboard (`/api/forms`) and lands in Kim Weston's Leads as a Quiz lead called "Calorie calculator", with the results attached.
- **`WEBHOOK_URL`:** optional GHL Inbound Webhook URL to also send each lead to. Leave it empty to skip it.
- **`REQUIRE_PHONE`:** Set to `false` to make phone optional.
- **`LOGO_URL`:** Logo image URL. Leave it empty to show a text version of the logo.
- **`BRAND.bookingUrl` / `bookingId`:** the GHL booking calendar shown at the bottom of the results (15-minute triage call), with the name, email and phone passed in.
- **`BRAND`:** CTA copy, disclaimer and webhook source label.

## Webhook payload

The form-encoded payload is sent with `sendBeacon` on submit:

`first_name, email, phone, age, sex, height_cm, weight_kg, activity, activity_multiplier, goal, bmr_kcal, maintenance_kcal, target_kcal, protein_g, carbs_g, fat_g, fibre_g, source`

## Calculation

- **Resting rate:** Mifflin-St Jeor, calculated as female.
- **Activity multipliers:** 1.2 to 1.725.
- **Goals:** lose weight (-20%), maintain, or gradual gain (+10%).
- **Calorie floor:** 1,200 kcal.
- **Protein:** 2.2 g/kg (1g per lb) up to 80kg, then 1 g/kg above that.
- **Fat:** 30% of calories, never under 0.8 g/kg.
- **Carbs:** fill the rest of the target, never under 50g.
- **Fibre:** 14g per 1,000 kcal, never under 25g.
