# MyHospital Zambia

*Bridging the gap between Zambia’s hospitals and the people through digital healthcare.*

MyHospital Zambia is a single-file patient web app that simulates a modern digital healthcare platform for hospitals across Zambia. It is built with plain HTML, CSS and JavaScript (no frameworks, no build step, no external dependencies) and is designed for patients and guardians.

> **This is a demo.** All patient data, hospital details, phone numbers, payments and results are fictional. Nothing is sent to a server, and the “end-to-end encryption” shown in the app is a simulated notice only.

## Quick start

1. Open `myhospital-zambia.html` in any modern browser.
2. Log in with the demo credentials:

   | Field    | Value     |
   |----------|-----------|
   | Username | `patient` |
   | Password | `12345`   |

3. Alternatively, use the **NRC / Passport + OTP** tab: enter any NRC or passport number, press *Send OTP*, and type the 4-digit demo code shown on screen.

The telemedicine camera feature needs a secure context. It works when the page is served over HTTPS or from `localhost`. Opening the file directly from disk may block camera access in some browsers; in that case the app falls back to a simulated consultation.

## Features

**Navigation:** Home · Meds · Appointments · Billing · Profile, plus login and logout.

**Home**
- Guided “care journey” simulation: referral uploaded → appointment confirmed → fee paid via mobile money → navigate the hospital → lab results received.
- Campus map simulation: tap a department to see where it is.
- Department directory with contact numbers, visiting hours and ward listings.

**Meds (digital health card)**
- Diagnosis and treatment history (mock data).
- Lab and radiology results with a *Download PDF* button (simulated, see Limitations).
- Prescription history with medication reminders saved on the device.
- Telemedicine: *Start consultation* shows “Connecting to Dr. Banda…” and requests the real camera and microphone through WebRTC `getUserMedia`.
- Pharmacist chat: ask “What are the side effects of Atorvastatin?” (or type your own question) and get an automated reply.

**Appointments**
- OPD booking for Cardiology, Orthopedics, Pediatrics and General OPD.
- Referral letter upload field (file picker only; the file is not uploaded anywhere).
- Confirmation output, e.g. *Orthopedics Appointment – 20 Nov 2025 – Confirmed*.
- Live queue tracker that counts your position down over time.

**Billing**
- Mobile money payment simulation: Airtel Money, MTN MoMo, Zamtel Kwacha.
- On success: *Payment Successful* and a downloadable digital receipt.

**Profile**
- Patient details, offline mode toggle, security notice and logout.

**Other**
- Language toggle: English, Nyanja and Bemba.
- Offline mode caches your data in LocalStorage.
- Responsive layout for mobile, tablet and desktop, with automatic light and dark themes.

## How data is stored

Everything lives in the browser’s LocalStorage, so it is private to your device and browser and survives a refresh.

| Key                 | Contents                                    |
|---------------------|---------------------------------------------|
| `mh_logged_in`      | Whether you are logged in                   |
| `mh_lang`           | Selected language (`en`, `ny`, `be`)        |
| `mh_appts`          | Booked appointments                         |
| `mh_reminders`      | Medication reminder times                   |
| `mh_offline`        | Offline mode on or off                      |
| `mh_cache_snapshot` | Offline cache of appointments and reminders |

To reset the demo, clear the site’s LocalStorage in your browser’s developer tools.

## Project structure

```
myhospital-zambia.html   # the whole app: markup, styles and scripts
README.md
```

Inside the HTML file, the sections are labelled by view (`view-home`, `view-meds`, `view-appointments`, `view-billing`, `view-profile`), and the script is organised by feature: login, routing, journey, map, appointments, meds, telemedicine, chat, billing, offline mode.

## Customising

- **Demo credentials:** edit the check in `loginDemo()`.
- **Departments and map:** edit the `DEPTS` array and the directory table in the Home view.
- **Prescriptions:** edit the `RX` array.
- **Pharmacist replies:** add keyword and answer pairs to `PHARM_REPLIES`.
- **Translations:** edit the `I18N` object. Add a `data-i18n="key"` attribute to any element you want translated.
- **Colours:** change the CSS variables at the top of the `<style>` block.

## Limitations

- All data is mock data. There is no backend, real authentication, or real payment processing.
- “PDF” downloads are plain-text files saved with a `.pdf` extension, to simulate the flow.
- The referral upload only shows the chosen file name.
- Translations currently cover headings, navigation and key labels. The Nyanja and Bemba text should be reviewed by native speakers before real use.
- The default booking date (20 Nov 2025) matches the demo scenario and may now be in the past; pick any date in the date field.
- Medication reminders are stored but do not trigger notifications.
- The pharmacist chat is a keyword lookup, not medical advice.

## Credits

All Rights Reserved – Designed by Chembe mulila
