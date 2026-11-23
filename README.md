# Student OTP Minecraft Whitelist Demo

A small prototype for verifying a `@student.edu.vn` email, collecting a
Minecraft username, and tracking a whitelist approval status.

> This is a failed test prototype.

## Features

- Generates 4-digit OTP codes and prints them in the server terminal
- Restricts requests to `@student.edu.vn` email addresses
- Applies a 2-minute resend cooldown, a 5-request hourly limit, and a
  100-request daily limit
- Expires OTP codes after 5 minutes
- Limits verification attempts to 10 per code
- Validates Minecraft usernames as 3–16 characters containing only letters,
  numbers, and underscores
- Prevents duplicate Minecraft usernames
- Stores email addresses as SHA-256 hashes in `users.json`
- Supports `pending`, `verified`, and `banned` account statuses

## How to Use

1. Install Node.js.
2. Open PowerShell in the project folder.
3. Install the server dependencies:

   ```powershell
   npm install express cors
   ```

4. Start the API server:

   ```powershell
   node otp.js
   ```

   The server runs at `http://localhost:3000`.

5. Open `index.html` in a browser.
6. Enter a `@student.edu.vn` email and select **Send OTP**.
7. Copy the 4-digit code printed in the terminal, enter it on the page, and
   verify it.
8. Submit a valid Minecraft username on the setup page.

## Account Status

New registrations are saved in `users.json` with a `pending` status. An
administrator can change that record's `status` to `verified` or `banned`.

```json
"status": "pending"
```

Use `pending` while waiting for review, `verified` after approval, or `banned`
to revoke access.


## Project Structure

```text
.
├── otp.js           # Express API, OTP logic, and account storage
├── index.html       # Student email and OTP verification page
├── setup.html       # Minecraft username registration and account status page
├── users.json       # Registered accounts keyed by hashed email
└── cooldowns.json   # Reserved cooldown storage file
    
```
