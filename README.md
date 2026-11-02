# Autojobication: downloads

Autojobication is a Windows desktop app that finds LinkedIn jobs that match
your profile and applies to them for you, at a human pace, from your own computer.

## ⬇️ Download

**[Download Autojobication for Windows](https://github.com/OneAndOnlyWahidHassani/Autojobication-releases/releases/latest/download/Autojobication-setup.exe)** (always the latest version)

Older versions and release notes are under [Releases](https://github.com/OneAndOnlyWahidHassani/Autojobication-releases/releases).

**Requirements:** Windows 10 or 11, 64-bit (Intel/AMD; ARM PCs are not
supported), about 1 GB of free disk space, and an internet connection.

---

## 1. Install

1. Run `Autojobication-setup.exe`.
2. Windows may show **"Windows protected your PC"**. That happens because the
   installer isn't code-signed yet, not because something is wrong. Click
   **More info → Run anyway**.
3. Follow the installer. It installs just for your user account, so no admin
   password is needed.

## 2. First launch: finish setup in the app

When you open Autojobication, a **Finish setup** card appears if something is missing.

| Item | What to do |
| --- | --- |
| **Google Chrome** (required) | If Chrome is already installed, this shows **Installed** and there's nothing to do. Otherwise click **Install**. Windows may ask for permission. If the automatic install doesn't work, your browser opens the Chrome download page. Install it, then click **Check again**. |
| **Chromium for external sites** (optional, ~150 MB) | Only needed if you turn on applying on company career sites (see step 5). Click **Install** and the app downloads it by itself. |

The app re-checks this every time it starts. After some updates it may ask you to
install Chromium again, because each version needs its matching Chromium.

## 3. Create your profile

1. Open the **Profile** tab and click **Create my profile**.
2. The profile starts from an **example (Jane Doe)**. Replace **everything** with
   your own details: name, email, phone, location, CV summary, skills, the path
   to your résumé PDF, target job titles and so on.
3. Click **Save changes**.

Runs are blocked while the example name or email is still in the profile, so it
can never apply as Jane Doe.

## 4. Add your Claude API key

The app uses Anthropic's Claude to read and fill in application forms.

1. Create an account at [console.anthropic.com](https://console.anthropic.com/) and add billing credits.
2. Go to **API Keys → Create Key** and copy the key (it starts with `sk-ant-`).
3. In Autojobication, open **Settings → Anthropic API key**, paste it, and click **Save**.

The key is stored in **Windows Credential Manager**, not in a file. Spending is
capped at **$5/day** by default. Change it in **Profile → Max $/day**. The
dashboard shows today's cost.

## 5. Log in to LinkedIn

Autojobication uses **its own Chrome profile**, separate from your everyday
Chrome, so it isn't logged in at first.

1. On the **Dashboard**, click **Look for jobs**.
2. A Chrome window opens. If LinkedIn asks you to sign in, log in by hand in that
   window. Two-factor authentication and CAPTCHAs are fine.
3. Back in the app, click **I resolved it — resume**.

You only need to do this once. The login is remembered. If LinkedIn signs you out
later, the app pauses and asks you to log in again.

**Applying on company sites (optional):** many jobs send you to the company's own
career site (Workday, Greenhouse, …). This is off by default. To turn it on, set
**Profile → External ATS strategy** to `attempt`. Chromium from step 2 is needed for this.

## 6. Optional: a free local model with Ollama

By default, job matching uses Claude Haiku, which is cheap and needs no setup. To match jobs
on your own PC for free instead:

1. Install [Ollama](https://ollama.com/download) and open it once.
2. In a terminal, run: `ollama pull llama3.2`
3. In Autojobication: **Profile → Match model → `ollama`**, then **Save changes**.
   If you use another model or port, change `llm.ollama_model` / `llm.ollama_url` in **Raw JSON**.

Ollama must be running whenever Autojobication matches jobs.

---

## Updates

Autojobication checks for new versions when it starts. When one is available, the
sidebar shows **Update available → Install & restart**. Your profile, history
and settings are kept. You can't update during a run; stop the run or let it finish first.

## Where your data lives

| What | Where |
| --- | --- |
| Profile, job history (`applications.db`), logs, app Chrome profile | `%APPDATA%\job-agent` |
| API key and external-site logins | Windows Credential Manager |
| Chromium (optional) | `%LOCALAPPDATA%\ms-playwright` |
| The app itself | `%LOCALAPPDATA%\Autojobication` |

To move to a new PC, copy `%APPDATA%\job-agent`, then add your API key again on the new PC.

**Uninstall:** Windows Settings → Apps → Autojobication → Uninstall. Your data
folder is left in place. Delete `%APPDATA%\job-agent` too if you want everything gone.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| Installer or Chrome install fails with "operation not permitted" | Windows Security's **Controlled folder access** may be blocking it. Check **Windows Security → Virus & threat protection → Protection history**, then allow the blocked app. |
| "Your profile still has the example details" | Replace the example name and email in **Profile**, then save. |
| "anthropic_api_key not set" | See step 4. |
| Chrome opens but LinkedIn shows a login page | See step 5, then click **I resolved it — resume**. |
| Matching fails with an Ollama error | Make sure the Ollama app is running and the model is pulled, or switch **Match model** back to `haiku`. |
