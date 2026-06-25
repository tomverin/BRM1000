# BRM 1000 CCK 2026 — Guide d'utilisation

Companion **jour J** pour le parcours officiel (~1022 km, 100 % bitume).  
Site : **https://tomverin.github.io/BRM1000/**

Cette application fonctionne **hors ligne** une fois chargée (PWA). Elle ne suit pas le GPS en continu : tu rafraîchis ta position quand tu en as besoin, pour préserver la batterie.

---

## Avant le départ

1. **Ouvre le site** sur ton téléphone (Chrome / Safari).
2. **Ajoute à l'écran d'accueil** (installer la PWA) pour un accès rapide et un meilleur mode plein écran.
3. **Pré-charge les tuiles carte** (panneau Outils → « Pré-charger tuiles ») si tu as du réseau la veille ou au départ — utile en zone mal couverte.
4. Autorise la **géolocalisation** quand le navigateur le demande.
5. Vérifie l'heure de départ affichée dans les checkpoints (utilisée pour les ETA horaires).

---

## Les trois vues

Swipe horizontal **sur l'écran principal** (geste franc, ~130 px) ou onglets en haut :

| Vue | Usage |
|-----|--------|
| **Glance** | Lecture rapide : km, prochain ravito, eau/solide/service, refresh GPS |
| **Carte** | Trace, position, tous les POI filtrés, checkpoints |
| **Profil** | Dénivelé et pente sur 20 km, le reste, ou tout le parcours |

Le swipe est désactivé sur la carte, les listes et le profil (scroll / pan carte sans changer de vue).

---

## GPS et position

- **Refresh GPS** (bouton principal en glance, ou panneau Position en vue carte) : enregistre un point, projette sur la trace, met à jour km, ratio et ETAs.
- Pas de suivi continu : chaque refresh = une **consultation** dans l'historique.
- **Hors trace** : distance affichée en mètres ; reste sur la route pour le km course.
- Badge 📍 en haut : état GPS (fix récent ou en attente).

**Conseil** : refresh au départ, puis régulièrement en roulant (toutes les 15–30 min). Après un long arrêt, un refresh suffit : l'app gère la pause automatiquement.

---

## Équipe (partage de position)

Si le partage est activé sur le site déployé :

- **Pas de compte** : au premier lancement, saisis ton prénom (ou ouvre un lien du type `?rider=tom`).
- Chaque **Refresh GPS** envoie ta position aux autres coureurs de l'équipe.
- Le panneau **Équipe** (vue Glance + carte) affiche les autres : prénom, km sur la trace, temps depuis la dernière mise à jour.
- Des marqueurs colorés sur la carte indiquent où sont les autres.
- Nécessite du **réseau** pour publier/recevoir (pas de sync offline).
- Les positions sont visibles par toute personne disposant de l'app et de la salle partagée — usage entre amis sur la course uniquement.

---

## Détection automatique des pauses

Pas de bouton pause à appuyer. L'algorithme analyse chaque segment entre deux refresh :

1. **Pause évidente** (temps réel >> temps prévu, typiquement > 15 min de « surplus ») → le segment est **exclu du ratio** automatiquement.
2. **Près d'un CP ou POI** (300 m / 150 m) → exclusion automatique encore plus fiable (ravito, contrôle).
3. **Bannière informative** : « Pause détectée — exclue du rythme ». Tu n'as rien à faire.
4. **Inclure quand même** : si l'app s'est trompée (montée lente confondue avec pause), tu peux forcer l'inclusion du segment dans le ratio.

Terrain technique lent (hors bitume / gravel) : impact rythme **atténué** — peu pertinent sur ce BRM 100 % bitume.

---

## Rythme adaptatif et ETA

- **Ratio adaptatif** : compare ta vitesse réelle au modèle terrain (bitume ~24 km/h sur ce BRM).
- **> 1** = plus rapide que prévu, **< 1** = plus lent.
- Les ETAs des POI et CP utilisent ce ratio quand la **confiance** est suffisante :
  - **Haute** : segment récent ≥ 10 km
  - **Moyenne** : segment ≥ 5 km
  - **Faible** : peu de données récentes (après pause, peu de refresh)

Le modèle ignore les segments trop courts (< 5 km ou < 10 min) pour éviter le bruit GPS.

---

## POIs (points d'intérêt)

**~385 POI** le long du parcours (OnRouteMap + BPF/ravitos orga) :

- **Eau** : fontaines, cimetières (eau potable)
- **Solide** : boulangeries, cafés, supermarchés, restauration rapide, BPF orga
- **Services** : toilettes, stations-service

**Filtres** : active/désactive les catégories (panneau POI en vue carte).

- **Carte** : affiche **tous** les POI des catégories actives sur le parcours.
- **Liste « Prochains »** : fenêtre **50 km** devant ta position.
- **Liste « Tous »** : ordre kilométrique sur tout le parcours.

Les **BPF et ravitos organisation** du parcours officiel sont marqués dans les données (`orga`).

---

## Checkpoints

Contrôles et arrivée extraits du GPX officiel :

| CP | Lieu (indicatif) | km |
|----|------------------|-----|
| Départ | — | 0 |
| CP1 | Besançon | ~154 |
| CP2 | Château-Chalon | ~289 |
| CP3 | Brançion | ~419 |
| CP4 | Autun | ~508 |
| CP5 | Veselay | ~616 |
| CP6 | Alésia | ~699 |
| CP7 | Froideconche | ~897 |
| CP8 | Grand Ballon | ~984 |
| Arrivée | — | ~1022 |

Heures limites et temps de contrôle : **fiche officielle BRM** (l'app affiche des ETA indicatives, pas l'horaire réglementaire).

---

## Outils

- **Raster / Vector** : bascule moteur carte (Leaflet raster vs MapLibre vectoriel).
- **Pré-charger tuiles** : cache offline pour la zone du parcours.
- **Exporter historique** : JSON des consultations (débrief post-course).
- **Nouvelle session** : efface l'historique local (confirmation).
- **Effacer historique** : idem sans relancer un GPS.

---

## Limites connues

- Pas de navigation turn-by-turn.
- Pas de suivi live permanent (choix batterie).
- Partage équipe : mise à jour uniquement à chaque refresh GPS (pas de tracking continu des autres).
- POI issus d'OpenStreetMap / OnRouteMap : **vérifier sur place** (horaires, eau réellement dispo).
- Une seule trace : parcours **non bouclé** (1022 km linéaires).
- Détection de pause heuristique : micro-arrêts < ~15 min peuvent encore influencer le ratio ; refresh espacés après un ravito aident.

---

## Dépannage

| Problème | Piste |
|----------|--------|
| Pas de GPS | Autorisation navigateur, mode avion désactivé, refresh en extérieur |
| Vieille version | Vider cache / réinstaller PWA ; le service worker se met à jour au chargement |
| Carte vide offline | Pré-charger les tuiles avec du réseau avant |
| ETA incohérent après pause | Attendre 5–10 km de roulage + refresh ; la pause est normalement déjà exclue |
| Ratio faussé par une pause non détectée | Bannière → « Inclure quand même » si besoin inverse, ou effacer historique |
| Trop de changements d'écran | Swipe uniquement sur la zone glance centrale, geste plus long |

---

*Généré depuis training-journal — modèle pacing V2 (Corsica 555 / BRM 1000).*
