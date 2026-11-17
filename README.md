# Salon — transformer l'iPhone 11 en hub de salon

Une web app plein écran, sans serveur, qui fait de l'iPhone une télécommande Spotify posée sur un support, avec horloge, météo, minuteur et mode nuit.

## Version express (tout depuis le téléphone)

1. Ouvre `https://maximesokol.github.io/salon/` dans **Safari** sur l'iPhone.
2. Suis l'assistant qui s'affiche : Partager › Sur l'écran d'accueil, puis ouvre l'icône « Salon ».
3. Dans l'app, l'assistant te guide pour créer ton accès Spotify (boutons « Copier » pour chaque valeur) et te connecter.
4. Réglages iPhone : Verrouillage auto › Jamais, et Accès guidé.

Le reste du guide détaille la version manuelle.

## Ce que fait l'app

- **Lecture** : grande pochette, fond flouté aux couleurs de l'album, lecture/pause, piste suivante/précédente, aléatoire, répétition, volume par glissement, toucher la barre pour avancer dans le morceau. Glisser sur la pochette vers la gauche ou la droite change de piste ; double-toucher met en pause.
- **Playlists** : tes playlists en grille, un toucher et ça joue.
- **File d'attente** : ce qui arrive ensuite.
- **Appareils (Spotify Connect)** : envoie la musique vers l'enceinte, l'ordi ou la télé de ton choix. L'iPhone ne joue pas le son, il pilote.
- **Horloge et météo** : quand rien ne joue depuis une minute, l'écran passe tout seul en grande horloge avec la météo du jour et des 3 jours suivants (Open-Meteo, pas de clé nécessaire).
- **Mode nuit** : de 22 h à 7 h (réglable), l'écran s'assombrit et passe en teintes chaudes. Toucher la grande horloge force jour/nuit.
- **Minuteur** : minuteur de cuisine avec sonnerie, ou « arrêter la musique dans 30 min » avec un fondu du volume (pratique pour s'endormir).
- **Mode démo** : sans compte, l'app tourne avec de faux morceaux pour voir à quoi elle ressemble.

## Ce qu'il te faut

- Un compte **Spotify Premium** (Spotify n'autorise le contrôle à distance qu'aux comptes Premium).
- Un compte **GitHub** gratuit, pour héberger l'app (elle doit être en HTTPS pour la connexion Spotify).
- 15 minutes.

## Étape 1 — Mettre l'app en ligne (GitHub Pages, gratuit)

1. Sur github.com, clique **New repository**. Nom : `salon`. Coche **Public**. Clique **Create repository**.
2. Sur la page du dépôt, clique **uploading an existing file** et glisse-dépose ces fichiers : `index.html`, `manifest.json`, `sw.js`, `icon-180.png`, `icon-512.png`. Clique **Commit changes**.
3. Va dans **Settings › Pages**. Sous *Branch*, choisis `main` et `/ (root)`, puis **Save**.
4. Au bout d'une minute, ton app est à l'adresse **`https://TON-PSEUDO.github.io/salon/`**. Ouvre-la : tu dois voir le mode démo.

Alternative sans GitHub : glisser le dossier sur app.netlify.com/drop marche aussi.

## Étape 2 — Créer ton « app » Spotify (pour avoir un Client ID)

1. Va sur developer.spotify.com/dashboard et connecte-toi avec ton compte Spotify.
2. **Create app**. Nom : `Salon`. Description : ce que tu veux.
3. **Redirect URI** : colle exactement `https://TON-PSEUDO.github.io/salon/` (avec le `/` final), puis **Add**.
4. Coche **Web API**, accepte les conditions, **Save**.
5. Dans **Settings** de l'app, copie le **Client ID** (pas besoin du Client Secret).

## Étape 3 — Installer sur l'iPhone

1. Dans **Safari** sur l'iPhone, ouvre `https://TON-PSEUDO.github.io/salon/`.
2. Bouton Partager › **Sur l'écran d'accueil** › Ajouter. Une icône « Salon » apparaît.
3. **Ouvre l'app depuis cette icône** (important : c'est elle qui gardera ta connexion Spotify, pas Safari).
4. Touche ⚙︎ (Réglages), colle le Client ID, tape ta ville pour la météo, puis **Enregistrer et se connecter à Spotify**. Autorise l'accès, tu reviens dans l'app connecté.

Spotify ne te redemandera plus de te connecter : l'app renouvelle la session toute seule.

## Étape 4 — En faire un vrai appareil de salon

- **Écran toujours allumé** : Réglages › Luminosité et affichage › Verrouillage auto › **Jamais**.
- **Bloquer l'iPhone sur l'app** : Réglages › Accessibilité › **Accès guidé** › activer. Dans l'app, triple-clic sur le bouton latéral › Démarrer. Pour en sortir : triple-clic + code.
- **Notifications** : active un mode Concentration « Ne pas déranger » permanent pour ne pas avoir de bannières.
- **Support** : un support de téléphone en paysage près de la chaîne ou sur une étagère, branché en continu. Astuce batterie : Réglages › Batterie › Santé et recharge › **Recharge optimisée** (ou la limite à 80 % si proposée) pour ménager la batterie.
- **Luminosité** : laisse la luminosité automatique active ; le mode nuit de l'app fait le reste.

## Si ça coince

- *« INVALID_CLIENT: Invalid redirect URI »* : l'adresse dans le dashboard Spotify ne correspond pas exactement à celle affichée dans ⚙︎ Réglages de l'app. Copie celle de l'app.
- *« Aucun appareil actif »* : ouvre Spotify sur un appareil (enceinte, ordi, téléphone) puis choisis-le dans l'onglet Appareils de l'app.
- *« Premium requis »* : le contrôle de lecture n'est possible qu'avec Premium.
- *La connexion s'ouvre dans Safari au lieu de revenir dans l'app* : ferme Safari, rouvre l'app depuis l'icône et réessaie.

## Note technique

Tout tient dans `index.html` (HTML/CSS/JS, aucune dépendance). Authentification Spotify en PKCE, donc aucun secret stocké ni serveur. Les jetons restent dans l'iPhone. Météo : Open-Meteo.
