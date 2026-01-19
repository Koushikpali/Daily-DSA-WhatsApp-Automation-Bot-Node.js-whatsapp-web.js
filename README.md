# Daily DSA WhatsApp Automation Bot
A lightweight Node.js bot that uses whatsapp-web.js to send daily Data Structures & Algorithms (DSA) problems (or other curated messages) to a WhatsApp user or group automatically.

This project automates sending daily DSA problems via WhatsApp using an automated (web) WhatsApp session. It is ideal for study groups, coding clubs, or anyone who wants daily practice delivered to their phone.

## Features
- Send daily or scheduled messages (DSA problems, links, tips).
- Works with whatsapp-web.js (web-based WhatsApp session).
- Configurable recipient (individual or group) and schedule.
- Supports message templates and optional attachments/links.
- Simple JSON configuration and extensible codebase.

## Prerequisites
- Node.js 16+ (or the version supported by whatsapp-web.js used in this repo).
- npm or yarn.
- A computer that can run an active browser session (the bot uses whatsapp-web.js and requires scanning a QR code to log in).
- (Optional) PM2, Docker, or a systemd service for persistent running.

## Quick Start

1. Clone the repository
```bash
git clone https://github.com/Koushikpali/Daily-DSA-WhatsApp-Automation-Bot-Node.js-whatsapp-web.js.git
cd Daily-DSA-WhatsApp-Automation-Bot-Node.js-whatsapp-web.js
```

2. Install dependencies
```bash
npm install
```

3. Configuration
Create a `config.json` (or set environment variables depending on the project code) with the following example structure:

```json
{
  "recipient": "123456789@s.whatsapp.net",
  "isGroup": false,
  "schedule": "0 9 * * *",
  "timezone": "Asia/Kolkata",
  "messageTemplate": "Today's DSA problem:\n\nTitle: {{title}}\nLink: {{link}}\n\nDifficulty: {{difficulty}}\n\nGood luck!",
  "problemSource": "data/problems.json"
}
```

- `recipient`: WhatsApp ID for an individual or group (e.g. `123456789@s.whatsapp.net` or `12345-67890@g.us`).
- `isGroup`: set to `true` when sending to a group.
- `schedule`: cron expression (this example sends daily at 09:00).
- `timezone`: timezone for the schedule.
- `messageTemplate`: template used to format a problem message.
- `problemSource`: path to your problem list or generator module.

4. Start the bot
```bash
node index.js
```
On first run, the bot will display a QR code in the terminal (or open a browser) for you to scan with WhatsApp to authenticate the web session. Once authenticated, the session may be saved (if implemented) so you don't need to scan every start.

## Example messages and screenshot

Below is the exact example message text shown by the bot in the screenshot you provided. To display the screenshot in this README, save your image from the chat as `assets/whatsapp-example.png` and commit it to the repository. The README references that file:
![Example automated message screenshot](WhatsApp%20Image%202026-01-20%20at%202.27.51%20AM.jpeg)


Example automated message (plain text version — copy this into your message template if you want the same wording and emojis):

this is an automated bot msg. Testing is on. If you receive this msg at 10:00 IST, it's working fine 🚀📌  
Today's DSA problem: https://leetcode.com/problems/valid-parentheses/

Another example (shown in the screenshot):

this is an automated bot msg. Testing is on. If you receive this msg at 10:00 IST, it's working fine 🚀📌  
Today's DSA problem: https://leetcode.com/problems/maximum-subarray/

Suggested messageTemplate that reproduces the style (in config.json):
```text
this is an automated bot msg. Testing is on. If you receive this msg at 10:00 IST, it's working fine 🚀📌
Today's DSA problem: {{link}}
```

Tips:
- Keep the link on its own line so WhatsApp previews the link with a card (as in the screenshot).
- Include emojis and short testing text for quick verification when you start the bot.
- If you want the bot to send the problem title as well, use a template like:
  "Today's DSA problem: {{title}}\n{{link}}"

## Configuration and Customization
- Problems can be provided in a JSON file (array of problems with title/link/difficulty) or via an API.
- Customize scheduling by editing the cron expression (common values: daily at 9am → `0 9 * * *`).
- Message templates support simple placeholders like `{{title}}`, `{{link}}`, and `{{difficulty}}` — adapt the code to use any templating engine you prefer.

Example `problems.json` structure:
```json
[
  {
    "title": "Two Sum",
    "link": "https://leetcode.com/problems/two-sum/",
    "difficulty": "Easy"
  },
  {
    "title": "Longest Substring Without Repeating Characters",
    "link": "https://leetcode.com/problems/longest-substring-without-repeating-characters/",
    "difficulty": "Medium"
  }
]
```

## Running in Production
- Use PM2 to keep the bot running:
```bash
pm2 start index.js --name daily-dsa-bot
pm2 save
```
- Or containerize with Docker (if you add a Dockerfile) and run in a reliable environment.
- Ensure session persistence: persist the whatsapp-web.js session data so reboots don't require rescanning.

## Troubleshooting
- QR Code not showing: ensure terminal supports QR display or the code opens a browser window (whatsapp-web.js options).
- Session lost frequently: enable and persist session storage (file or database) so you don't need to rescan every run.
- Messages not delivered: verify `recipient` ID is correct and the bot account has permission to message the group/user.
- Rate limits: do not send spammy volumes; respect WhatsApp usage policies to avoid being blocked.

## Security & Privacy
- The bot uses your WhatsApp account — use a dedicated account if you prefer separation from your personal account.
- Keep any saved session files private and secure.
- Do not hard-code sensitive data in files tracked by git; use environment variables or a secure vault for secrets.

## Contributing
Contributions, issues, and feature requests are welcome. Please open issues for bugs or enhancement ideas. Feel free to add support for:
- OAuth/remote problem sources (LeetCode, GeeksforGeeks APIs),
- Improved templating and scheduling UI,
- Dockerfile and example systemd/PM2 configs.

## License
Specify your license here (e.g., MIT). If you want to add a license, include a LICENSE file.

---
Instructions:
- To make the screenshot appear in the README, save and commit the image under `assets/whatsapp-example.png`.
- If you'd like, I can add the image file to the repository for you — tell me to proceed and provide permission to write the file, or upload the image here and I'll include it.
