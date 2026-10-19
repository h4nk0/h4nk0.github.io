# Capture × Todoist sign-in files

Todoist lets Capture sign in without a client secret or a server, as long as a few small files
are served over HTTPS from a site you control. A free GitHub Pages site does it.

| File | What it is |
|---|---|
| `oauth/todoist-client.json` | Capture's OAuth client description. Its own URL is the client id. |
| `oauth/todoist/index.html` | The page Todoist returns to after sign-in ("Returning to Capture…"). |
| `.well-known/apple-app-site-association` | Lets iOS hand that return trip straight back to Capture. |
| `.nojekyll` | Tells GitHub Pages to publish the `.well-known` folder. |

Nothing here sees your Todoist password or tokens: sign-in happens on Todoist's own page, and the
tokens go straight from Todoist to your iPhone's Keychain.

> **Status: published 2026-10-19** at https://github.com/h4nk0/h4nk0.github.io (Pages from `main`, root).
> To change a file, edit it here, copy it into that repository and push.

## Steps (already done)

1. **Create the repository.** On GitHub, create a new **public** repository named exactly
   `h4nk0.github.io`.
2. **Copy the files.** Copy everything in this folder into the root of that repository, including
   the hidden `.nojekyll` file and the `.well-known` folder. Commit and push.
3. **Turn on Pages.** In the repository, open Settings › Pages and set Source to
   "Deploy from a branch", branch `main`, folder `/ (root)`. Wait a minute, then check that
   `https://h4nk0.github.io/oauth/todoist-client.json` shows the JSON.
4. **Already done in the app.** `TodoistConfig.host` is `h4nk0.github.io` and the app's Associated
   Domains include `webcredentials:h4nk0.github.io`.
5. **Done.** Build Capture to your iPhone and tap Connect Todoist.

Until step 5, Settings › To-dos in Capture has "Use an API token instead" (Todoist › Settings ›
Integrations › Developer), so nothing else is blocked.

**If sign-in opens Todoist but never comes back:** Apple caches the
`apple-app-site-association` file, so allow up to a day after step 3, then delete and reinstall Capture.
The file must be reachable at `https://h4nk0.github.io/.well-known/apple-app-site-association`
with no redirect.
