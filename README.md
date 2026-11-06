# Saffron & Smoke - Staff Panel

The private orders panel for restaurant staff. Orders placed on the restaurant site appear here live, and staff can update their status.

## Folder structure

    saffron-smoke-staff/
    ├── index.html
    ├── css/style.css
    └── js/
        ├── app.js               (sign-in, live orders, filters, status updates, sound alert)
        └── firebase-config.js   (your Firebase keys go here)

## Features

- Staff sign-in with email and password (Firebase Authentication)
- Live orders list: new orders appear without refreshing the page
- A beep plays when a new order arrives (Sound on/off button at the top)
- Summary counts: Total, New, Preparing, Ready and Delivered
- Filter by status and by order type (Dine-in, Home Delivery, Takeaway)
- Search by order ID, customer name, mobile or table number
- Order details: customer name, mobile, address, notes, table number, items, delivery fee, COD fee and total
- Payment method and transaction ID (for Easypaisa and JazzCash orders)
- Status updates: New, Preparing, Ready, Delivered, Cancelled
- Dark and light theme, mobile friendly

## How it connects

1. A customer places an order on the restaurant site with Order Now.
2. The order is saved in the Firestore collection `restaurantOrders`.
3. This panel reads the same collection and shows the order instantly.
4. When staff change a status here, the order is updated in Firestore.

Both sites must use the same Firebase config.

## Setup

1. Paste your Firebase config into `js/firebase-config.js` (same config as the restaurant site):

        window.FIREBASE_CONFIG = {
          apiKey: "...",
          authDomain: "...",
          projectId: "...",
          storageBucket: "...",
          messagingSenderId: "...",
          appId: "..."
        };

2. In Firebase go to Authentication > Users > Add user and create the staff account with a strong password. If the restaurant staff use a different email from the Hasan Mart staff, create that user too.
3. In Firestore Database > Rules make sure the `restaurantOrders` block is there and contains the staff email (see the restaurant site README). To allow two staff emails, use:
   `request.auth.token.email in ['staff1@gmail.com', 'staff2@gmail.com']`
4. Authorized domains already include `syedhasanshahqadri-ops.github.io`.

## Publishing on GitHub Pages

1. Create a repository named `saffron-smoke-staff`.
2. Upload the contents of this folder to the root of the repository.
3. Go to Settings > Pages, choose the `main` branch and the root folder, then save.
4. Your link: `https://syedhasanshahqadri-ops.github.io/saffron-smoke-staff/`

## Using the panel

1. Open the link and sign in. Keep the page open during opening hours so the sound alert works.
2. New orders appear at the top with the status **New** and a highlighted edge.
3. Click an order to see the details, items and payment information.
4. For Easypaisa and JazzCash orders, check the transaction ID in your payment app before confirming.
5. Update the status as the order moves: Preparing, Ready, then Delivered.
6. Use Sign out when you finish, especially on a shared device.

## Troubleshooting

- **"Setup needed":** `js/firebase-config.js` is still empty.
- **"Sign-in failed":** wrong email or password, or the user was not created in Authentication.
- **"Missing or insufficient permissions":** the email in the rules does not match the signed-in account, or the rules were not published.
- **No beep:** the browser blocks sound until you interact with the page. Sign in on that device first and check that Sound is on.
- **No orders appear:** the restaurant site may still be in demo mode. Check that it has the same Firebase config.

## Security notes

- Never write the staff password in the code.
- Use a strong password and change it if it is ever shared in a chat or message.
- Do not link to this panel from the restaurant site, and share its link only with staff.# saffron-smoke-staff
