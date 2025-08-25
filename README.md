# OWASP

🔹 1. Pre-Setup (You, as Instructor)

👉 Do this before class so students can jump directly to labs:

On your Kali/Linux machine, run once:

sudo apt update && sudo apt install -y docker.io
sudo systemctl enable docker --now
docker pull bkimminich/juice-shop

Verify Juice Shop works:

docker run --rm -p 3000:3000 bkimminich/juice-shop

A01: Broken Access Control

Login with your account on http://localhost:3000.

Click the Basket (cart icon) on the top right.

Example URL: http://localhost:3000/#/basket/3

In the URL, change the number (e.g., /basket/3 → /basket/1).

Press Enter.


A02: Cryptographic Failures
In your browser, go to:

http://localhost:3000/ftp


You’ll see an exposed directory with files.

Download the file package.json.bak.

Right-click → Save Link As…

Or click it → save to Downloads.

Open the file with a text editor in Kali:

 mousepad ~/Downloads/package.json.bak

View the contents (developer backup file).


🛡️ A03: Injection

Click: Login.

Type: ' OR 1=1-- in Email field, leave password blank.

Click: Login.
In the Password field, type anything (example: 123).

Output: Bypass Authentication
A04: A04 – Insecure Design (Business Logic Flaw)

Login to Juice Shop.

Go to Products → Add the Best Juice Shop Salesman Artwork (₳5000) to basket.

Open DevTools → Network → XHR tab.

In Basket, click “+” once to change quantity → observe the request:

PUT /api/BasketItems/<id>


Right-click that request → Copy as cURL (bash).

Paste in Kali terminal → change body to:

{"BasketId":<id>, "ProductId":<id>, "quantity":-100}


Run command.

Refresh Basket page → Total price becomes negative.

Proceed to Checkout:

Add dummy shipping info.

Add test card (e.g. 4111111111111111 / 12/2099 / 123).

Place order.

🛡️ A05: Security Misconfiguration

In URL bar: Type /ftp or /administration.

Output: Access to sensitive page.

Scoreboard: “Security Misconfiguration” → ✅ Green.

🛡️ A06: Vulnerable & Outdated Components

Click: Scoreboard → notice hint about outdated components.

Optional Demo: Run npm audit if time permits.

Output: Shows vulnerable packages.

Scoreboard: “Vulnerable Components” → ✅ Green.

🛡️ A07: Auth Failures

Click: Login.

Try: admin@juice-sh.op / admin123.

If not working: Just explain brute force concept (Hydra demo optional).

Output: Weak password access.

Scoreboard: “Authentication Failures” → ✅ Green.

🛡️ A08: Integrity Failures

Click: Checkout → Apply Coupon.

Intercept with Burp: Change "discount":90.

Output: 90% discount applied.

Scoreboard: “Integrity Failures” → ✅ Green.

🛡️ A09: Logging & Monitoring Failures

Click: Login → try 10 wrong passwords.

Observe: No lockout, no alert.

Output: Unlimited attempts allowed.

Scoreboard: “Logging & Monitoring” → ✅ Green.

🛡️ A10: SSRF

Click: Submit Product.

Enter Image URL: http://localhost:3000/admin.

Click: Submit.

Output: Internal admin page loaded.

Scoreboard: “SSRF” → ✅ Green.
