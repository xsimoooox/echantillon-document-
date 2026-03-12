# Jeu de données « sol parfait arganier » (exemple de terroir proche d'Agadir, Maroc)

Ce document explique, en termes simples, ce que contient le fichier :

- `gee_raw_export/exports/raw_20260312T134958Z.json`

Tu peux le considérer comme une **photo numérique complète** d’un petit terroir arganier « réussi » : climat, état de la végétation, humidité, altitude, etc. Tout vient de **Google Earth Engine** (GEE), à partir de différents satellites et modèles météo.

---

## 1. Où se trouve ce terroir ?

Dans le JSON :

- `bbox.west`: -9.2263  
- `bbox.east`: -9.2211  
- `bbox.south`: 29.7285  
- `bbox.north`: 29.7323  

C’est une petite zone au **sud-ouest du Maroc**, à l’intérieur de la zone naturelle de l’arganier, autour de 1200 m d’altitude.

La période étudiée est :

- `period.start`: **2026‑02‑10**  
- `period.end`: **2026‑03‑12**  

Donc une **fin d’hiver / début de printemps**, moment clé pour la recharge en eau du sol et la préparation de la saison de croissance.

---

## 2. Que mesurons-nous exactement ?

Le fichier JSON contient plusieurs blocs :

- `sources` : d’où viennent les données (nom du satellite ou du modèle météo).  
- `stats` : **valeurs moyennes / min / max** sur toute la zone.  
- `pixel_samples` : un échantillon de **points individuels** (longitude, latitude) avec leurs valeurs de bandes.  
- `thumbnails` : des **URL d’images** (PNG) pour visualiser NDVI, RGB, relief, etc.

Pour ce terroir arganier, les sources principales sont :

- **Sentinel‑2** (`sentinel2`) : satellites optiques (couleurs, végétation).  
- **Landsat 8** (`landsat8`) : autre satellite optique, utile pour vérifier / comparer.  
- **Sentinel‑1** (`sentinel1`) : radar (structure du sol, humidité, rugosité).  
- **ERA5‑Land** (`era5`) : climat (température de l’air, pluie) reconstitué.  
- **NASADEM** (`dem`) : altitude du terrain.

Pour simplifier la lecture, on se concentre sur :

- **Végétation : NDVI** (vigueur des arbres) et **NDMI** (humidité des couronnes).  
- **Climat : pluie et température**.  
- **Altitude**.

---

## 3. Lecture des principaux indicateurs (en langage simple)

### 3.1 Végétation – « À quel point l’arganier est vert ? »

Dans `stats.sentinel2.stats` :

- `ndvi_mean` ≈ **0.34**  
  - NDVI est un indice de verdure (0 = sol nu, 0.2‑0.3 = végétation clairsemée, >0.5 = végétation très dense).  
  - Ici, ~0.34 signifie : **couvert d’arganiers et/ou d’arbustes, pas une forêt fermée mais une végétation bien présente**.

- `ndmi_mean` ≈ **0.007**  
  - NDMI est un indice d’humidité de la canopée (valeurs positives = couvert plutôt humide).  
  - Ici, la valeur est proche de zéro mais légèrement positive : **canopée ni très sèche ni saturée en eau**, ce qui est cohérent avec un système adapté à la sécheresse.

En résumé :  
> La végétation d’arganiers est **présente**, plutôt en bon état, sans être « luxuriante ». C’est typique d’un système sec mais fonctionnel.

---

### 3.2 Climat récent – « Froid / chaud / pluvieux ? »

Dans `stats.era5.stats` :

- `t2m_c_mean` ≈ **13.8 °C** (température moyenne de l’air à 2 m)  
  → **fin d’hiver frais**, confortable pour l’arganier (loin des canicules estivales).

- `era5_precip_sum_mm_mean` ≈ **19.7 mm** sur ~1 mois  
  → une vingtaine de millimètres de pluie sur la période.  
  Pour un système sec comme l’arganier, ce volume n’est pas énorme mais **suffit à maintenir un minimum de recharge** du sol si on cumule plusieurs événements dans l’hiver.

En résumé :  
> Climat **frais et modérément humide** sur ce mois, ce qui aide les arbres à refaire leurs réserves en eau avant les fortes chaleurs.

---

### 3.3 Altitude – « Relief et exposition »

Dans `stats.dem.stats` :

- `elevation_m_mean` ≈ **1 200 m**  
  → plateau / versant d’altitude moyenne, typique de **l’arganeraie intérieure** (loin du littoral plat).

Cette altitude contribue à :

- des **nuits plus fraîches**,  
- une certaine **variabilité locale** (pentes, vallons) qui peut créer des zones un peu plus humides ou plus sèches.

---

## 4. Pourquoi dire que c’est un « sol parfait » pour l’arganier ?

Dans ce contexte, « parfait » ne veut pas dire « sol riche, humide, sans stress », mais plutôt :

> **Un environnement typique où l’arganier exprime bien son potentiel naturel**  
> (bonne survie, port correct, production d’amandons et d’huile de qualité),  
> **sans interventions artificielles lourdes**.

Les éléments qui vont dans ce sens :

- **Climat sec mais pas extrême** sur la période récente : ~14 °C de moyenne, un peu de pluie.  
- **Végétation en forme** (NDVI ~0.34, NDMI légèrement positif) : les arbres ne sont pas en stress hydrique aigu.  
- **Altitude ~1200 m** : contexte de relief favorable aux arganiers (moins de chaleur extrême qu’en plaine basse, mais assez de soleil).  
- Les valeurs de `pixel_samples.sentinel2` montrent des NDVI locaux pouvant dépasser **0.45‑0.47** : certaines micro‑zones sont même plus vigoureuses que la moyenne.

Ce jeu de données sert donc de **référence** : il décrit ce à quoi ressemble, statistiquement, un terroir où l’arganier « se sent bien ».

---

## 5. À quoi ça sert concrètement ?

Même si on ne connaît pas les termes techniques agricoles, on peut utiliser ce JSON pour :

- **Comparer d’autres parcelles** à ce terroir :  
  - On calcule les mêmes indicateurs (NDVI, NDMI, pluie, température, altitude…) pour une autre zone.  
  - On regarde si cette autre zone est **plus sèche**, **plus chaude**, **plus pauvre en végétation**, etc.

- **Construire une « recette »** pour rapprocher une parcelle de ce terroir idéal :
  - Si NDVI est bien plus bas → améliorer l’occupation du sol (densité, régénération, protection des jeunes plants).  
  - Si NDMI est plus faible → agir sur la gestion de l’eau / couverture du sol (paillage, lutte contre le ruissellement).  
  - Si la température est plus élevée et les pluies plus rares → adapter densité, variétés, et surtout pratiques de conservation de l’eau.

- **Alimenter un modèle de machine learning** :  
  - Chaque terroir (dont celui‑ci) devient une **ligne de données** avec :  
    NDVI moyen, NDMI moyen, pluie, température, altitude, etc.  
  - Le modèle peut apprendre à prédire, par exemple, un **score de qualité arganier** ou une **probabilité de réussite de plantation**.

---

## 6. Comment expliquer ça à quelqu’un qui n’est pas agronome ?

On peut résumer ainsi :

- Ce fichier représente **un endroit réel** où l’arganier pousse bien.  
- On y a mesuré, avec des satellites et des modèles météo :
  - à quel point c’est **vert**,  
  - à quel point c’est **sec ou humide**,  
  - combien il a **plu récemment**,  
  - s’il fait plutôt **frais ou très chaud**,  
  - et à quelle **altitude** on se trouve.

Ensuite, pour un **nouveau terrain**, on peut :

1. Mesurer les mêmes choses avec les mêmes outils (GEE).  
2. Comparer les chiffres à ceux de ce terroir « réussi ».  
3. En déduire une liste d’actions : où il faut améliorer l’eau, la couverture du sol, la densité d’arbres, etc.

Cette approche permet de **parler de terroir d’arganier avec des nombres simples**, même pour des personnes qui ne sont pas spécialistes en agronomie, et de s’appuyer dessus pour entraîner des modèles de machine learning plus tard.



