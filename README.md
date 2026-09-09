# Prix de l'immobilier par commune (agrégats DVF)

Prix au m² médians et statistiques de marché, **commune par commune**, calculés à
partir des ventes immobilières réellement enregistrées par l'administration fiscale
(base DVF de la DGFiP). Aucune estimation, aucune extrapolation : seulement des
ventes constatées.

Jeu de données produit et maintenu par [VendsMonBien](https://vendsmonbien.com),
à partir de données publiques.

## Contenu

- `prix-immobilier-communes-dvf.csv` : un enregistrement par commune (756 communes).
- `prix-immobilier-communes-dvf.geojson` : les mêmes communes, géolocalisées (points WGS-84), pour un usage cartographique.

## Couverture

756 communes, réparties sur 5 départements (Creuse, Orne, Puy-de-Dôme, Gironde,
Loire-Atlantique). Le périmètre s'étend au fil des publications. Ne figurent que les
communes dont le volume de ventes permet un calcul significatif.

## Méthode

- **Source** : DVF géolocalisées (DGFiP / Etalab), croisée avec les DPE (ADEME) et la
  population (INSEE).
- **Prix médian**, et non moyen : plus robuste sur de faibles volumes, où deux ventes
  atypiques suffisent à déformer une moyenne.
- **Mutations multi-locaux écartées** : une vente portant sur plusieurs locaux répète
  sa valeur totale sur chaque ligne DVF ; calculer un prix au m² ligne à ligne y serait
  faux. Ces mutations sont exclues du calcul.
- **Fiabilité graduée** selon le nombre de ventes unitaires : `élevée` (≥ 100),
  `bonne` (30–99), `indicative` (15–29). En dessous de 15 ventes, la commune n'est pas
  publiée.
- **Fraîcheur** : recalcul mensuel à partir des dernières publications DVF.

## Dictionnaire des champs (CSV)

| Champ | Description |
|---|---|
| `code_insee` | Code INSEE de la commune (5 caractères) |
| `nom_commune` | Nom de la commune |
| `code_departement` / `nom_departement` | Département |
| `region` | Nom de la région |
| `population` | Population municipale (INSEE) |
| `latitude` / `longitude` | Coordonnées de la commune (WGS-84) |
| `prix_m2_median` | Prix médian au m², tous types de biens (€) |
| `prix_m2_median_maison` | Prix médian au m² des maisons (€) |
| `prix_m2_median_appartement` | Prix médian au m² des appartements (€) |
| `prix_m2_q1` / `prix_m2_q3` | 1er et 3e quartile du prix au m² (€) |
| `prix_median_maison` / `prix_median_appartement` | Prix de vente médian par type (€) |
| `surface_mediane_m2` | Surface médiane des biens vendus (m²) |
| `nb_ventes` | Nombre de ventes unitaires retenues (multi-locaux exclus) |
| `nb_maisons` / `nb_appartements` | Détail des ventes par type |
| `periode_debut` | Première vente de la période couverte |
| `periode_fin` | Dernière vente de la période couverte |
| `evolution_prix_pct` | Évolution du prix au m² sur la période (%) |
| `part_passoires_dpe_pct` | Part de logements classés F ou G (DPE ADEME, %) ; vide si non calculé |
| `prix_m2_median_departement` | Prix médian au m² du département (contexte) |
| `fiabilite` | Niveau de fiabilité : `élevée`, `bonne` ou `indicative` |
| `url` | Page détaillée de la commune sur vendsmonbien.com |

Le GeoJSON expose un sous-ensemble de ces propriétés (`code_insee`, `nom`,
`departement`, `prix_m2_median`, `prix_m2_median_maison`, `prix_m2_median_appartement`,
`nb_ventes`, `evolution_prix_pct`, `part_passoires_dpe_pct`, `fiabilite`, `url`).

## Licence et attribution

Données publiées sous **Licence Ouverte / Open Licence 2.0** (Etalab), comme les
sources dont elles dérivent. La réutilisation est libre, sous réserve de mentionner la
source et la date. Source à citer :

> Prix DVF par commune, VendsMonBien (https://vendsmonbien.com), d'après DVF (DGFiP),
> DPE (ADEME) et INSEE.

## Limites

- DVF ne couvre pas l'Alsace-Moselle (régime du livre foncier) ni Mayotte.
- Les données sont publiées par semestre, avec plusieurs mois de délai : elles
  décrivent le marché de la période couverte, pas nécessairement le jour présent.
- Les communes en fiabilité `indicative` reposent sur peu de ventes : à lire avec
  prudence, en s'appuyant sur les quartiles pour la dispersion.

## Contact

timothee.jeanson@gmail.com
