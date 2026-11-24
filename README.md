# Brigade Airsoft Games — Scenario Hub

The site served at **airsoft.munkys.dev**. The **current game** is featured on the main page, and an **Archive** button (top-left) opens past scenarios.

a US task force races to rescue the sole surviving VIP).

## Structure
```
/                      -> current game (featured)        -> index.html
/archive/              -> archive index (list of games)  -> archive/index.html
/archive/<game>/       -> an archived game               -> archive/<game>/index.html
```

Archived games:
- **Getting High on Your Own Supply** (Colombia 1984) — `archive/getting-high-on-your-own-supply/`

## Features
- **Single `index.html` per game** — pure HTML/CSS/JS, no build step, no dependencies.
- **Bilingual HE/EN toggle** — one button flips `dir`/`lang` and swaps all content (RTL/LTR).
- **Faction theme** — North Korea red vs. USA blue over a dark tactical base (CSS custom properties, easy to re-skin).
- **Print-friendly** — dedicated `@media print` styles for paper briefs.
- **Archive hub** — featured current game + a card-based archive of past games.

## Add the next game later
1. Move the current `index.html` (+ its assets) into `archive/<old-game-slug>/`.
2. Add a card for it in `archive/index.html`.
3. Drop the new game's `index.html` (+ assets) at the repo root.
4. Commit & push, then deploy (below).

## Local preview
Open `index.html` in a browser. For correct relative `/archive/` links, serve the folder:
```powershell
python -m http.server 8080
# then visit http://localhost:8080/
```

## Deploy to airsoft.munkys.dev (Lightsail + Nginx)
```bash
# one-time: clone into the web root
sudo rm -rf /var/www/airsoft && sudo git clone https://github.com/BarakHoo/airsoft-scenario-korea.git /var/www/airsoft

# on each update
cd /var/www/airsoft && sudo git pull
```
Use the provided `nginx/airsoft.conf` as `/etc/nginx/sites-available/airsoft`, then:
```bash
sudo ln -sf /etc/nginx/sites-available/airsoft /etc/nginx/sites-enabled/airsoft
sudo nginx -t && sudo systemctl reload nginx
sudo certbot --nginx -d airsoft.munkys.dev   # HTTPS
```

> You can also host on **GitHub Pages** (Settings → Pages → `main` / root):
> https://barakhoo.github.io/airsoft-scenario-korea/
