# Pages légales de BUMI

Trois pages HTML autonomes (le CSS est intégré dans chaque fichier, il n'y a
rien d'autre à téléverser). Elles sont écrites pour un **éditeur particulier,
non professionnel, sans société**.

## 1. Combler les trous

Chaque trou s'affiche en rouge cerné de pointillés dans la page. Cherchez
`à compléter` dans les trois fichiers — il n'y a rien d'autre à modifier.

| À renseigner | Où | Pourquoi |
|---|---|---|
| Prénom et NOM réels | `confidentialite.html` uniquement | Choix de prudence — voir la réserve ci-dessous. |
| Adresse e-mail dédiée | les trois fichiers | Exigée par la règle 1.2 de l'App Store (« published contact information ») et par le RGPD. |
| Date de publication | `confidentialite.html`, `conditions.html` | — |
| Raison sociale + adresse de Supabase et de GitHub | `index.html` | C'est la contrepartie de l'anonymat : le II de l'article 1-1 de la LCEN permet de ne publier **que** les coordonnées de l'hébergeur. À recopier depuis leurs mentions légales, sans les inventer. |

Remplacez aussi les `mailto:CONTACT@EXEMPLE.COM` par la vraie adresse.

## 2. Ce qui n'a pas à être publié

**Votre adresse personnelle n'apparaît nulle part**, et c'est délibéré :

- **LCEN, article 1-1 II** (dans sa rédaction issue de la loi SREN du 21 mai
  2024 — l'ancien article 6 III est abrogé) : un éditeur non professionnel peut
  ne publier que le nom et l'adresse de son hébergeur, **à condition de lui
  avoir communiqué ses nom, prénoms, domicile et téléphone**.
- **RGPD, articles 13 et 14** : ils exigent « l'identité et les coordonnées »,
  sans imposer de format. Une adresse e-mail satisfait les « coordonnées ».

### Une réserve sur la publication de votre nom

L'article 13.1.a du RGPD exige « l'identité et les coordonnées » du responsable
de traitement. Il ne définit pas « identité », et aucune source primaire
consultée — texte, ligne directrice du CEPD, décision CNIL — n'impose
expressément le nom civil d'une personne physique éditant à titre non
professionnel. Faire figurer votre nom dans la politique de confidentialité est
donc l'option prudente, **pas une contrainte démontrée**.

C'est aussi une décision irréversible : une fois le nom publié et indexé, on ne
le retire pas. Si vous préférez ne pas le publier, la dérogation de l'article
1-1 II de la LCEN couvre déjà les mentions légales, et l'exposition résiduelle
porte sur ce seul point — à arbitrer, éventuellement avec un conseil.

Ce ne sera de toute façon pas votre seule exposition : Apple publie votre nom
légal comme vendeur sur la fiche App Store pour tout compte individuel, et cela
ne se masque pas.

### Une condition à remplir de votre côté

L'anonymat n'est acquis que si votre identité civile complète (nom, prénoms,
domicile, téléphone) figure bien chez votre hébergeur. Vérifiez le profil de
facturation de votre compte Supabase et gardez-en une preuve datée.

## 3. Héberger

Un dépôt GitHub **public** dédié, par exemple `bumi-legal` :

```
git init && git add . && git commit -m "Pages légales"
gh repo create bumi-legal --public --source=. --push
```

Puis, sur github.com : `Settings` → `Pages` → `Source: Deploy from a branch` →
`main` / `/ (root)` → `Save`. Les pages sont en ligne quelques minutes plus
tard à `https://<votre-compte>.github.io/bumi-legal/`.

## 4. Brancher l'app

Reportez les trois URL dans [`BUMI/App/LegalLinks.swift`](../BUMI/App/LegalLinks.swift) :

```swift
static let privacyPolicy: URL? = URL(string: "https://…/confidentialite.html")
static let termsOfUse: URL?    = URL(string: "https://…/conditions.html")
static let supportEmail: String? = "contact@…"
```

Tant qu'une valeur vaut `nil`, la ligne correspondante reste masquée dans les
Réglages, et un avertissement s'affiche dans la console Xcode à chaque
lancement en debug.

## 5. Dans App Store Connect

- **Privacy Policy URL** → `…/confidentialite.html`
- **Support URL** → `…/` (la page d'accueil ; ce champ est **obligatoire**, au
  même titre que la politique de confidentialité)

## 6. Un écart connu, à trancher

L'article 6, V de la LCEN impose de **détenir** les données permettant
d'identifier les auteurs des contenus, et le décret n° 2021-1362 fixe des durées
allant d'un an (données techniques de connexion, à compter de la connexion) à
cinq ans (identité civile).

L'app ne le fait pas : elle ne journalise aucune adresse IP de son côté, et les
journaux de Supabase sont purgés en quelques jours (environ un jour en plan
gratuit, sept en plan Pro ; une conservation longue suppose un *Log Drain*
payant). Les pages décrivent donc la réalité — elles n'annoncent pas une
conservation qui n'existe pas, ce qui serait pire.

Deux options : accepter cet écart, fréquent chez les petits éditeurs, ou mettre
en place une conservation délibérée. C'est votre décision, pas un oubli.

---

Ces textes sont des brouillons rédigés à partir des textes cités, pas un
conseil juridique. Faites-les relire si l'enjeu le justifie.
