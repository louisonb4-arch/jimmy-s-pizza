# LEGAL-TODO — Jimmy's Pizza

> État au 9 octobre 2026. Aucune donnée n'a été inventée : ce qui n'a pas pu être vérifié
> à une source est marqué `[à fournir]` ou `[à confirmer]` et apparaît **surligné en rose
> sur les pages légales**, exprès.
>
> Base professionnelle, à faire valider selon l'activité réelle — ne remplace pas un avocat.

---

## 1. Bloquant avant toute diffusion publique

### 1.1 Le site est une maquette non commandée

Le site utilise le nom, le logo, les photos et la carte de JIMMY'S PIZZA, et ses mentions
légales désignent la société comme éditeur et Yannick Kowalski comme directeur de la
publication. **Tant que l'établissement n'a pas validé le site, ces affirmations ne sont pas
vraies** : c'est Vokum qui publie.

Ce qui est en place pour limiter le risque :

- `noindex, nofollow` dans le `<head>` de `index.html` **et** en en-tête HTTP
  (`X-Robots-Tag` dans `vercel.json`) : Google ne référence pas la maquette et ne la
  confond pas avec la présence officielle de l'établissement ;
- le lien ne doit être envoyé **qu'au gérant**, pas diffusé (réseaux, portfolio public).

**À la signature :**
1. retirer la balise `<meta name="robots" content="noindex, nofollow">` de `index.html` ;
2. retirer l'en-tête `X-Robots-Tag` de `vercel.json` ;
3. brancher le domaine `jimmyspizza.fr` (aujourd'hui une page Squarespace « en construction ») ;
4. mettre à jour `canonical`, `og:url`, JSON-LD et `sitemap.xml` avec le domaine définitif ;
5. faire relire et valider les deux pages légales par le gérant.

### 1.2 Commande en ligne : ce qui a été fait, et pourquoi c'est légal

**Trouvé sur son site actuel** (site DISH, `jimmys-pizza-restaurant-nantes.eatbu.com`) :

| Canal | URL | État vérifié le 9/10/2026 |
|---|---|---|
| À emporter (click & collect) | `https://jimmys-pizza-nantes.order.app.hd.digital` | actif, **retrait seul** (livraison désactivée sur DISH), CGV + confidentialité propres |
| Livraison | `https://naofood.coopcycle.org/fr/restaurant/181-jimmy-s-pizza` | fiche existante, adresse concordante |
| Uber Eats | `ubereats.com/fr/store/jimmys-pizza/2DPAwIc9T5iDf8VpE47XZw` | **non vérifiable** (403 aux robots) → non ajouté, à confirmer avec lui |
| Réservation DISH | `reservation.dish.co/widget/hydra-…` | présent sur son site DISH, mais la presse indique « pas de réservation » → **non ajouté** |

**Analyse :**

- **Un lien simple vers ses propres pages de commande est licite** : un lien hypertexte vers
  une page publique n'est pas une reproduction (CJUE, *Svensson*, 2014). Ce sont ses canaux,
  il les publie lui-même, les commandes arrivent chez lui.
- **Pas d'intégration du widget DISH (iframe/script)** : il est rattaché à son compte DISH et
  à son site, l'intégrer ailleurs sans son accord sort de ce cadre ; il déposerait en plus des
  traceurs tiers → bannière de consentement obligatoire.
- **Aucune commande ni aucun paiement sur notre site** : sinon l'éditeur devient vendeur à
  distance → CGV, information précontractuelle, paiement sécurisé, etc. Ici, les CGV et la
  confidentialité de la commande sont celles de DISH et de Naofood (mentionné sur le site,
  sous les boutons et dans les mentions légales).
- **Pas de logos Uber Eats / DISH / Naofood** : libellés texte uniquement (marques de tiers).

→ **Donc : pas de `/cgv` à créer** tant que le site ne fait que renvoyer vers ces plateformes.

---

## 2. À fournir / à confirmer par l'établissement

| Point | Où | Pourquoi |
|---|---|---|
| Téléphone de l'hébergeur | `mentions-legales.html` | obligatoire (LCEN art. 6 III) ; Vercel ne le publie pas. Alternative : héberger chez un prestataire européen qui publie ses coordonnées |
| Médiateur de la consommation | `mentions-legales.html` | obligatoire pour toute vente aux consommateurs (C. conso. L612-1) — il doit en avoir désigné un |
| Auteur des photos + droits cédés | `mentions-legales.html` | photos de l'établissement, origine exacte non documentée |
| Durée de conservation des journaux Vercel | `politique-confidentialite.html` | dépend de l'offre Vercel utilisée |
| Information allergènes en salle | menu + mentions | le site affirme qu'elle est disponible sur demande : à vérifier sur place |
| Uber Eats actif ? | — | si oui, ajouter le lien à côté de Naofood |

---

## 3. Vérifié (sources)

| Donnée | Valeur | Source |
|---|---|---|
| Dénomination / forme | JIMMY'S PIZZA, SARL | registre national (API recherche-entreprises) |
| Capital | 10 000 € | annonce légale de constitution |
| RCS | Nantes 988 336 335 | annonce légale |
| SIRET | 988 336 335 00019 | registre national |
| TVA | FR26988336335 — **valide** | VIES (Commission européenne), 9/10/2026 |
| APE | 56.10C | registre national |
| Gérant = directeur de la publication | Yannick Kowalski | registre + loi 82-652 art. 93-2 (le gérant d'une SARL l'est de droit) |
| Téléphone / e-mail | 06 25 91 10 65 / yannick@jimmyspizza.fr | publiés par l'établissement (site DISH) |
| Hébergeur | Vercel Inc., 440 N Barranca Ave #4133, Covina, CA 91723 | conditions d'utilisation Vercel |
| Horaires | lun 12h–14h ; mar–ven 12h–14h + 18h30–22h ; sam 18h30–22h ; dim fermé | JSON-LD de son site DISH (corrigé : le site disait 21h45) |
| Carte | « Menu 10/26 » | PDF officiel sur son site DISH (la carte 06/26 affichée était périmée) |

---

## 4. Choix techniques liés au RGPD

- **Polices auto-hébergées** (`assets/fonts/`) : plus aucun appel à Google Fonts, qui
  transmettait l'adresse IP des visiteurs à Google (jurisprudence LG München, 2022).
- **Aucun cookie** → **pas de bannière de consentement** (inutile, et gênante).
- Un seul stockage navigateur : `sessionStorage.jimmys_intro_v2` (animation d'ouverture déjà
  vue). Aucune donnée personnelle, jamais transmis, effacé à la fermeture de l'onglet ;
  considéré comme réglage d'interface exempté de consentement (art. 82 loi I&L) —
  interprétation à garder en tête si un auditeur pointilleux passe.
- CSP durcie : `font-src 'self'`, plus aucune origine tierce.
- Accessibilité : en tant que micro-entreprise, l'établissement est a priori exempté des
  obligations de déclaration d'accessibilité (à confirmer : < 10 salariés et CA ≤ 2 M€).

## 5. Bon à savoir pour la suite

- La typo de sa marque (menu PDF) est **Bogart** (Zetafonts, licence payante). Le site utilise
  Caprasimo (gratuite, même famille Cooper) en attendant. S'il possède une licence web
  Bogart, on peut la brancher.
- Son site DISH héberge des photos de l'établissement plus grandes que celles du site
  (480 px) : à récupérer avec son accord pour gagner en netteté.
