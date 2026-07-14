# 🏎️ F1 Apex — Course 3D

Jeu de course de Formule 1 en 3D, jouable directement dans le navigateur. 10 écuries réelles, 11 circuits mythiques, aucune installation requise.

**[▶ Jouer en ligne](https://llorenzoliverfouchet-gif.github.io/Formula-Apex-online/)**

## Fonctionnalités

- **10 écuries et pilotes réels**, **11 circuits** (Monaco, Bahreïn, et d'autres tracés emblématiques, de jour comme de nuit)
- **Plusieurs modes de jeu** :
  - 🏎 Solo contre des IA
  - 👥 2 joueurs en écran partagé (même clavier)
  - 🌐 En ligne en duel, pair-à-pair (WebRTC, sans serveur)
  - 🛰️ En ligne via serveur relais (marche même sur réseaux restrictifs type 4G)
- Difficulté réglable, gestion de l'essence et des arrêts au stand, plusieurs vues caméra (poursuite, cockpit, caméra TV, aérienne)
- 🌊 **Caméra douce** (option dans le menu) — adoucit fortement tous les mouvements de caméra (tremblement, zoom, à-coups) pour les personnes sensibles au mal des transports
- Manette, clavier (ZQSD/flèches), volant tactile ou flèches tactiles selon l'appareil
- Chat texte et vocal en multijoueur en ligne
- **PWA installable** — fonctionne hors ligne une fois chargé une première fois
- 🎬 **Mode « Cinématique » (caché)** — un mode réalisateur pensé pour filmer des vidéos : zéro voiture jouable, les 10 écuries se disputent la course entre elles, et la caméra suit celle de ton choix. Débloque-le en tapant 7 fois sur le badge de version (coin haut droit du menu) pour faire apparaître le chip correspondant dans les modes de jeu. Pendant la course : ⏮/⏭ (ou les flèches ←/→) pour changer de voiture suivie, C/V pour changer d'angle de caméra.

## Jouer

Aucune installation : ouvre simplement [la page du jeu](https://llorenzoliverfouchet-gif.github.io/Formula-Apex-online/) dans un navigateur récent (Chrome, Firefox, Safari, Edge). Sur mobile, tu peux l'installer comme une app via « Ajouter à l'écran d'accueil ».

## Développement local

Le jeu est un unique fichier `index.html` autonome (pas de build, pas de dépendances à installer) : les bibliothèques (Three.js, Trystero, Supabase) sont chargées depuis un CDN au démarrage.

Pour lancer une version locale :

```bash
python3 -m http.server 8000
# puis ouvrir http://localhost:8000
```

(Ouvrir directement le fichier `index.html` sans serveur local fonctionne aussi pour l'essentiel, mais certaines fonctionnalités comme le service worker nécessitent un serveur HTTP.)

## Architecture

- `index.html` — tout le jeu : rendu 3D (Three.js), physique de course, IA, HUD, menu, réseau
- `manifest.json` / `service-worker.js` — PWA installable et jouable hors ligne
- `.github/workflows/deploy-pages.yml` — déploiement automatique sur GitHub Pages à chaque push sur `main`

### Multijoueur en ligne

Deux mécanismes coexistent, au choix dans le menu :

- **P2P (Trystero)** : connexion directe entre navigateurs via WebRTC, signalisation par trackers BitTorrent/Nostr. Rapide, mais peut échouer sur certains réseaux très restrictifs (NAT symétrique, wifi d'entreprise).
- **Serveur (Supabase Realtime)** : passe par un canal relais. Plus lent mais fonctionne presque partout, y compris en 4G.

## Licence

Projet personnel — tous droits réservés sauf mention contraire.
