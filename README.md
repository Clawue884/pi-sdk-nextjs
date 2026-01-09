pi-sdk-nextjs

> Developer SDK for integrating Pi Network authentication into Next.js applications

This repository provides a JavaScript/TypeScript SDK and CLI to simplify secure Pi authentication flows in modern Next.js projects.




---

🧠 Overview

pi-sdk-nextjs is designed for developers who want to integrate Pi Network authentication into Next.js applications with minimal boilerplate and clear security boundaries.

The SDK focuses on:

Generating Pi authentication URLs

Verifying Pi callback requests securely on the server

Supporting Next.js App Router conventions


This repository exposes a small, explicit API intended to be composed into your own application logic.


---

✨ Features

🔐 Server-side verification of Pi authentication callbacks

⚡ Minimal API surface

🧩 Works naturally with Next.js App Router

🖥️ Includes CLI support for setup and testing



---

📦 Installation

npm install pi-sdk-nextjs

or

yarn add pi-sdk-nextjs


---

⚙️ Environment Variables

Create a .env.local file in your Next.js project:

PI_API_KEY=your_pi_api_key
PI_APP_ID=your_app_id
PI_CALLBACK_URL=http://localhost:3000/api/pi/callback

> ⚠️ Never expose PI_API_KEY to the client.




---

🚀 Basic Usage (Next.js App Router)

1️⃣ Initialize Pi Client

// lib/pi.ts
import { PiClient } from "pi-sdk-nextjs";

export const piClient = new PiClient({
  apiKey: process.env.PI_API_KEY!,
  appId: process.env.PI_APP_ID!,
  callbackUrl: process.env.PI_CALLBACK_URL!,
});


---

2️⃣ Redirect User to Pi Login

// app/api/pi/auth/route.ts
import { NextResponse } from 'next/server';
import { piClient } from '@/lib/pi';

export async function GET() {
  const authUrl = piClient.getAuthUrl();
  return NextResponse.redirect(authUrl);
}


---

3️⃣ Handle Pi Callback

// app/api/pi/callback/route.ts
import { NextRequest, NextResponse } from 'next/server';
import { piClient } from '@/lib/pi';

export async function GET(req: NextRequest) {
  const payload = await piClient.verifyCallback(req);

  // payload contains verified Pi user information
  console.log(payload);

  return NextResponse.redirect('/dashboard');
}


---

🔐 Security Model

All Pi verification must occur server-side

Client input must never be trusted for authentication

Treat Pi callbacks as authentication events

Log and monitor failed verification attempts



---

🧩 Design Principles

Explicit over implicit authentication flow

Server-first security

Framework-native integration

Composable SDK usage



---

📚 Examples

A complete working Next.js example is provided separately under:

examples/nextjs-basic


---

🤝 Contributions

Contributions are welcome, especially:

Documentation improvements

Example applications

Non-breaking helper utilities


Please avoid modifying core authentication logic without prior discussion.


---

📄 License

This project is licensed under the same terms as the upstream repository.

All credits belong to the original maintainers.
