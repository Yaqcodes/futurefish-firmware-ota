# Future Fish Firmware OTA Manifest

This repo contains the OTA update manifest for the Future Fish IoT firmware. Devices fetch `check.json` at startup to see if a newer firmware version is available.

## Contents

- **check.json** – JSON with `version` (semver string) and `url` (absolute URL to the `.bin` file). Update this file when you release new firmware.

## GitHub Pages setup

1. **Create the repo on GitHub** (e.g. `futurefish-firmware-ota`). Keep it **public** so GitHub Pages can serve it.

2. **Push this folder** as the repo contents:
   ```bash
   cd futurefish-firmware-ota
   git init
   git add .
   git commit -m "Initial: check.json and CNAME for GitHub Pages"
   git branch -M main
   git remote add origin https://github.com/Yaqcodes/futurefish-firmware-ota.git
   git push -u origin main
   ```

3. **Enable GitHub Pages**
   - Repo → **Settings** → **Pages**
   - **Source**: Deploy from a branch
   - **Branch**: `main` / **(root)**
   - Save. After a minute, the site will be at `https://yaqcodes.github.io/futurefish-firmware-ota/`.

4. **Custom domain (firmware.futurefishagro.com)**
   - In **Settings** → **Pages**, under **Custom domain**, enter: `firmware.futurefishagro.com`
   - Save. The **CNAME** file in this repo already matches that.
   - In your DNS (e.g. Cloudflare, your registrar), add:
     - **CNAME**: `firmware` → `yaqcodes.github.io` (or the value GitHub shows in the Pages settings).
   - After DNS propagates, HTTPS will work and devices can use `https://firmware.futurefishagro.com/check.json`.

## Updating firmware

1. Build and attach the new `.bin` to a **GitHub Release** in your firmware repo (or host it elsewhere).
2. Edit **check.json** in this repo: set `version` to the new release (e.g. `1.0.1`) and `url` to the new `.bin` URL.
3. Commit and push. GitHub Pages will update within a few minutes; devices will see the new version on next boot or check.
