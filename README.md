# Jeopardy Game App (standalone)

A self-contained multiplayer Jeopardy game. No dependencies — just Node.js.

## Run locally
```
node server.js          # then open http://localhost:3000
```
Set `PORT` to change the port. Game data persists to `data.json` next to server.js.

## Deploy on Render (free tier)
1. Put this folder's files in a GitHub repository (keep the structure: server.js,
   package.json, render.yaml, public/index.html, public/qrcode.min.js).
2. On render.com: **New → Blueprint**, connect the repository, **Apply**.
   (Or: New → Web Service → connect repo → Runtime: Node, Build Command: *(empty)*,
   Start Command: `node server.js`, Instance Type: Free.)
3. Render gives you a URL like `https://jeopardy-game-app-xxxx.onrender.com`.
   That is the public address: the host opens it to run the game; players scan the
   QR code on the host lobby screen (it encodes `<your-url>/?code=XXXX`) and join
   from any browser.

Free-tier notes: the service sleeps after ~15 min idle (first visit then takes
~1 minute to wake — open it a few minutes before your event). The free instance's
disk is ephemeral, so templates saved in the app may reset if the service
restarts; re-creating a template takes a couple of minutes, and a paid instance
($7/mo) removes both limits.

## Preset admin accounts
- admin1 / admin123
- admin2 / admin123
- host1 / host123

(Change them in `ADMINS` at the top of server.js before deploying, if you like.)

## How a game flows
Admin signs in → builds or picks a template → Start Game → lobby shows a 4-letter
code + QR code → players join on phones (create a team = captain, join a team, or
audience if enabled) → host starts → board → open a question → 5-4-3-2-1 → captains
buzz → answer on phone (auto-judged) or orally (host judges) → wrong answers deduct
per template rules and, for choice questions, other teams may re-buzz after a 3-2-1 →
Final Jeopardy for host-set points → champion screen.
