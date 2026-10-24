# Portfolio with login, signup and live admin updates

Visitors see only a sign-in page. After they sign in they see the portfolio.
The admin edits the phone number and services, and everyone who is signed in sees the change immediately.

## Run it on your own computer
1. Install Node.js (version 18 or newer) from https://nodejs.org
2. Open a terminal in this folder and run:  `node server.js`
3. Open http://localhost:3000
4. Click **Create account**. **The first account you create is the admin**, so do this before anyone else.
5. As admin, click **Edit site** (top right) to change your phone number, email and services, or to remove members.

No `npm install` is needed. The app uses only what comes with Node.

## Put it online so other people can use it
Your computer can't be reached by other people, so you need a host that runs Node (Render, Railway, Fly.io or a VPS).
Use `node server.js` as the start command, then set these settings on the host:

| Setting | Value | Why |
|---|---|---|
| `ADMIN_EMAIL` | your email | Only this email can ever become admin (safer than "first account wins") |
| `TRUST_PROXY` | `1` | Lets the app see the real visitor address behind the host |
| `COOKIE_SECURE` | `1` | Sends the login cookie only over HTTPS |
| `DATA_DIR` | a folder on a **persistent disk** | Accounts and content are saved in `data.json`. On hosts without a persistent disk they are lost on every restart |

Always use an HTTPS address (most hosts give you one for free).

## What is protected
- Passwords are hashed with scrypt and never stored in plain text.
- Login uses an HttpOnly cookie. Sign-in and sign-up attempts are rate limited.
- The portfolio page itself is only sent to signed-in people.
- Only the admin can change content or remove members, and the server checks this on every request.

## Not included yet
Password reset by email, email verification, and two-factor login. All three need an email service. Back up `data/data.json` regularly.
