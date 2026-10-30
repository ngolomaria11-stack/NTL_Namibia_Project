<p align="right"><a href="methodology.md">English</a></p>

# Méthodologie — Namibie (2014–2025)

## Données et nettoyage

VIIRS DNB mensuel (VCMSLCFG) et annuel VNL V2, DMSP–VIIRS harmonisé, Black Marble quotidien, GHSL/WorldPop, Sentinel-5P NO₂/SO₂, MODIS LST, Banque mondiale. Nettoyage : pixels valides si cf_cvg ≥ 2, unité-mois gardée si ≥ 80 % de pixels observés, pics remplacés, fond et torchères masqués.

## 📈 Cas d'usage 1 — Dynamiques temporelles

- **Question** — L'activité accélère-t-elle ou ralentit-elle, hors effet de saison ?
- **Données** — VIIRS VCMSLCFG (monthly), VIIRS VNL V2 (annual), Harmonised DMSP–VIIRS (Li et al., 2020)
- **Méthode** — STL robuste (période 12) sur log(somme des lumières) ; pente de Theil–Sen et test de Mann–Kendall sur les composites annuels ; détection d'anomalies et de ruptures.
- **Validation** — Significativité de la tendance (Mann–Kendall) et cohérence mensuel/annuel (**p-value = < 0,0001**)
- **Incertitude** — IC 95 % de la croissance annuelle : +4,1 % à +6,4 %
- **Limites** — Couverture nuageuse et nuits courtes en été ; la lumière n'est pas la valeur ajoutée.
- **Statut** — `experimental` · Confiance: élevée
- **Références** — Cleveland et al. (1990) STL ; Sen (1968) ; Elvidge et al. (2017).
- **Page du tableau de bord** — [`#time`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/fr/?country=NAM#time)

**Résultats de cette exécution**

- `F02` Entre 2014 et 2025, la lumière nocturne de Namibie a évolué de +5,6 % par an (IC 95 % : +4,1 % à +6,4 %). Sur les 12 derniers mois, le niveau désaisonnalisé est -1,6 % par rapport aux 12 mois précédents. (confiance élevée : tendance significative (p < 0,01 ; n = 12))
- `F70` Validation : Significativité de la tendance (Mann–Kendall) et cohérence mensuel/annuel (p-value = < 0,0001). Incertitude : IC 95 % de la croissance annuelle : +4,1 % à +6,4 % Limites : Couverture nuageuse et nuits courtes en été ; la lumière n'est pas la valeur ajoutée. Statut : statistique expérimentale ; confiance élevée.

## 🗺️ Cas d'usage 2 — Croissance régionale et convergence

- **Question** — Quelles régions décollent, lesquelles décrochent ?
- **Données** — VIIRS VNL V2, GHSL / WorldPop, Sentinel-5P NO₂
- **Méthode** — Croissance robuste par unité (Theil–Sen, Mann–Kendall), classes croissance/stagnation/déclin, β- et σ-convergence, indice de Herfindahl.
- **Validation** — Corrélation de rang avec le NO₂ troposphérique (source indépendante) (**Spearman ρ = -0,21**)
- **Incertitude** — Classe attribuée seulement si |pente| ≥ seuil et p < α ; IC de β (erreurs robustes).
- **Limites** — Petites unités : bruit et débordement de lumière (blooming) entre voisins.
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Barro et Sala-i-Martin (1992) convergence ; Henderson, Storeygard et Weil (2012).
- **Page du tableau de bord** — [`#regions`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/fr/?country=NAM#regions)

**Résultats de cette exécution**

- `F03` Sur 103 unités ADM2, 87 sont en croissance significative, 16 stagnent et 0 déclinent. L'activité lumineuse reste concentrée : Erongo concentre 17 % de la lumière nationale. (confiance moyenne : classement sur 103 unités, seuil ±1 %/an et p < 0,10)
- `F04` Entre unités ADM2, la lumière par habitant converge : les unités les moins éclairées rattrapent leur retard. (confiance moyenne : β = −0,033 [−0,045 ; −0,020], n = 103)
- `F24` Erongo (ADM1, 2025) : part de la lumière nationale 16,7 %, croissance annuelle +7,4 % (IC +4,8 % à +9,8 %, classe Croissance), lumière par habitant 0,892, population 0,01 M, dans le noir 37 %, PIB estimé (expérimental) 2,07 Md USD.
- `F25` Khomas (ADM1, 2025) : part de la lumière nationale 16,4 %, croissance annuelle +2,3 % (IC +1,4 % à +3,0 %, classe Croissance), lumière par habitant 0,442, population 0,02 M, dans le noir 23 %, PIB estimé (expérimental) 2,04 Md USD.

## 💹 Cas d'usage 3 — Relation lumières–PIB

- **Question** — Peut-on estimer la croissance avant sa publication, et le PIB régional ?
- **Données** — VIIRS, PIB réel (Banque mondiale, WDI)
- **Méthode** — log(lumière) ~ log(PIB) en niveaux et en croissance, MCO avec écarts-types HAC ; prévision hors échantillon ; PIB régional = PIB national réparti au prorata de la lumière.
- **Validation** — Suivi hors échantillon de la croissance officielle (**corrélation / EAM (points) = -0,55 / 3,6**)
- **Incertitude** — IC 95 % de l'élasticité : -0,48 à 4,17 ; intervalles de prévision 80 % et 95 %.
- **Limites** — Échantillon annuel court ; le PIB régional est une statistique expérimentale à confronter aux comptes régionaux.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Henderson et al. (2012) AER ; Chen et Nordhaus (2011) PNAS ; Gibson et al. (2021) JDE.
- **Page du tableau de bord** — [`#time`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/fr/?country=NAM#time)

**Résultats de cette exécution**

- `F05` L'élasticité de la lumière au PIB réel est de 1,85 en niveaux (IC 95 % : −0,48 à 4,17, R² = 0,22, 12 années) et de −0,24 en taux de croissance (IC : −0,82 à 0,33). Hors échantillon, la croissance des lumières suit celle du PIB avec une corrélation de −0,55 (erreur absolue moyenne : 3,6 point de croissance). (confiance faible : n = 12, non significatif (p = 0,12))
- `F40` Élasticité lumières–PIB réel en niveaux : β = 1,85 (IC 95 % -0,48 à 4,17, R² = 0,22, n = 12, confiance faible : n = 12, non significatif (p = 0,12)). +1 % de PIB ↔ +β % de lumière.
- `F41` Élasticité lumières–PIB réel en taux de croissance : β = -0,24 (IC 95 % -0,82 à 0,33, R² = 0,03, n = 11, confiance faible : n = 11, non significatif (p = 0,41)). +1 % de PIB ↔ +β % de lumière.
- `F42` Élasticité lumières–PIB réel en série longue DMSP–VIIRS : β = 0,85 (IC 95 % 0,59 à 1,10, R² = 0,92, n = 30, confiance élevée : n = 30, p < 0,01, IC étroit). +1 % de PIB ↔ +β % de lumière.

## ⚡ Cas d'usage 4 — Chocs et résilience

- **Question** — Quelle a été la profondeur d'un choc, et la vitesse de récupération ?
- **Données** — VIIRS (monthly), Black Marble VNP46A2 (daily), catalogue d'événements
- **Méthode** — Écart au niveau d'avant-choc sur la série désaisonnalisée ; ruptures structurelles ; indice quotidien Black Marble.
- **Validation** — Le creux dépasse-t-il la variabilité ordinaire ? (**creux (choc principal) = -2,9 % — non**)
- **Incertitude** — Variabilité mensuelle d'avant-choc (écart-type robuste) ; ruptures inexpliquées signalées.
- **Limites** — Les chocs touchant des activités peu éclairées (agriculture, services de jour) sont sous-estimés.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Román et al. (2018) ; Elvidge et al. (2020) lumières et confinements.
- **Page du tableau de bord** — [`#shocks`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/fr/?country=NAM#shocks)

**Résultats de cette exécution**

- `F06` Le choc le plus marqué dans la série désaisonnalisée est « COVID-19 » : creux de -2,9 % (03/2021), retour au niveau d'avant-choc après 13 mois. (confiance faible : creux comparé à la variabilité mensuelle d'avant-choc)
- `F44` COVID-19 (2020-03-01 → 2021-06-30) : creux de -2,9 % le 2021-03-01, retour au niveau d'avant-choc après 13 mois. Distinct du bruit : non.
- `F45` Ruptures structurelles : 2017-01-01 (13,4 %); 2023-02-01 (11,6 %). Sans événement connu à ±6 mois : 2.
- `F46` Régions les plus touchées (creux) : Hardap -30,0 % (covid19), Khomas -26,6 % (covid19), Omaheke -22,7 % (covid19), Erongo -16,9 % (covid19), Otjozondjupa -15,0 % (covid19).

## ⚖️ Cas d'usage 5 — Inégalités et électrification

- **Question** — Où vivent les populations privées d'électricité ?
- **Données** — VIIRS VNL V2, GHSL / WorldPop, GHSL SMOD, accès à l'électricité (WDI)
- **Méthode** — Gini et Theil pondérés par la population ; population des pixels habités sous le seuil de détection ; sensibilité à trois seuils ; IC bootstrap de la variation du Gini.
- **Validation** — Écart avec le taux d'accès à l'électricité de la Banque mondiale (**écart moyen (points) = 28,9**)
- **Incertitude** — Plage selon le seuil de radiance ; IC bootstrap du Gini.
- **Limites** — Proxy de l'éclairage extérieur, pas du raccordement : un foyer raccordé mais peu éclairé paraît « dans le noir ».
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Theil (1967) ; Falchetta et al. (2020) accès à l'électricité par les lumières.
- **Page du tableau de bord** — [`#inequality`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/fr/?country=NAM#inequality)

**Résultats de cette exécution**

- `F07` Le Gini de la lumière par habitant (ADM2) vaut 0,44 en 2025 (baisse significative depuis 2014). Environ 0,01 million(s) de personnes vivent dans des zones habitées sans lumière détectable (17 % de la population habitée). (confiance moyenne : sensible au seuil de radiance (de 0,01 à 0,01 M selon le seuil) ; proxy d'éclairage extérieur, pas de raccordement)
- `F47` Gini de la lumière par habitant (ADM2) : 0,533 en 2014 → 0,442 en 2025 (variation -0,091, IC bootstrap -0,142 à -0,049). Theil T 0,332 ; part entre régions 33 %.
- `F48` Habitants de zones habitées sans lumière détectable : 0,01 M (19 %) en 2014 → 0,01 M (17 %) en 2025. Rapport lumière/hab. urbain/rural 0,7. Proxy de l'accès à l'électricité, sensible au seuil.
- `F49` Écart moyen entre la part de la population en zone éclairée et le taux d'accès à l'électricité de la Banque mondiale : 28,9 points.

## 🏭 Cas d'usage 6 — Zones industrielles

- **Question** — Où est l'industrie, et son activité progresse-t-elle ?
- **Données** — VIIRS VNL V2, GHSL BUILT-S, Sentinel-5P NO₂/SO₂, MODIS MOD11A2, OpenStreetMap
- **Méthode** — Concordance de six signaux par pixel (≥ 3 dont la lumière), grappes 8-connexes, typologie et confiance.
- **Validation** — Comparaison avec la liste de référence (OpenStreetMap) (**précision / rappel / F1 = 51 % / 14 % / 0,22**)
- **Incertitude** — Confiance par grappe selon le nombre de signaux forts ; sites isolés à vérifier.
- **Limites** — Résolution de Sentinel-5P (≈ 5 km) et MODIS (1 km) : les signaux qualifient un voisinage.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Elvidge et al. (2016) torchères ; Pesaresi et al. (2023) GHSL.
- **Page du tableau de bord** — [`#industry`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/fr/?country=NAM#industry)

**Résultats de cette exécution**

- `F08` 45 grappes industrielles détectées par concordance de signaux satellitaires : 10 d'industrie lourde, 10 zones d'activités et de logistique, 8 sites d'hydrocarbures et 17 sites isolés à vérifier. Elles émettent 17,8 % de la lumière nationale (dernière année) ; leur lumière évolue de +2,0 % par an. Oshana concentre la plus forte activité industrielle. (confiance faible : précision 51 % et rappel 14 % face à la liste de référence)
- `F50` 45 grappes industrielles (≥ 3 signaux sur 6) : Site isolé à vérifier 17, Industrie lourde 10, Zone d'activités et logistique 10, Hydrocarbures et torchères 8. Part de la lumière nationale : 17,8 % ; croissance annuelle +2,0 %. Validation (OpenStreetMap) : précision 51 %, rappel 14 %.
- `F51` IND-001 — Site isolé à vérifier à Otjinene (Oshana) (55.04 km², 3 signaux, confiance faible); IND-002 — Site isolé à vérifier à Onesi (Oshana) (27.09 km², 3 signaux, confiance faible); IND-003 — Industrie lourde à Rundu Urban (Kavango) (23.435 km², 4 signaux, confiance moyenne); IND-008 — Hydrocarbures et torchères à Opuwo (Erongo) (6.235 km², 3 signaux, confiance faible); IND-004 — Industrie lourde à Karibib (Karas) (16.34 km², 3 signaux, confiance faible); IND-007 — Hydrocarbures et torchères à Walvisbay Urban (Khomas) (7.095 km², 3 signaux, confiance faible); IND-012 — Hydrocarbures et torchères à Windhoek West (Khomas) (3.01 km², 3 signaux, confiance faible); IND-005 — Site isolé à vérifier à Katima Muliro Urban (Caprivi) (11.395 km², 3 signaux, confiance faible); IND-006 — Site isolé à vérifier à Okatana (Ohangwena) (7.955 km², 3 signaux, confiance faible); IND-035 — Hydrocarbures et torchères à Windhoek Rural (Khomas) (0.86 km², 3 signaux, confiance faible)
- `F52` Oshana : 3 grappe(s) industrielle(s), 83,8 km², 68,3 % de la lumière de la région.

## 🏖️ Cas d'usage 7 — Tourisme saisonnier

- **Question** — Quelles zones vivent du tourisme, et comment évolue la saison ?
- **Données** — VIIRS (monthly), nuitées ou arrivées WDI
- **Méthode** — Surcroît estival net des unités comparables de même latitude ; test unilatéral ; indice de saison base 100 ; saisons recoupant le Ramadan signalées.
- **Validation** — Corrélation avec international tourist arrivals (WDI) (**r = -0,13**)
- **Incertitude** — p-valeur par unité ; années 2020–2021 exclues du classement.
- **Limites** — Toute activité estivale (diaspora, résidences secondaires, festivals) est captée, pas seulement le tourisme.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Analyses saisonnières des lumières et du tourisme, par ex. Hu et al. (2021).
- **Page du tableau de bord** — [`#tourism`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/fr/?country=NAM#tourism)

**Résultats de cette exécution**

- `F09` 4 unités sur 103 ont un surcroît de lumière estival net d'au moins 10 % : Otavi (Oshana), Ongenga (Ohangwena), Aminius (Ohangwena), Tsumkwe (Kunene). Le surcroît net médian atteint +17 % dans la zone la plus touristique. L'indice de saison (base 100 = 2019) tombe à 309 en 2020 et vaut 266 en 2025. (confiance faible : corrélation de -0,13 avec international tourist arrivals (WDI) (7 années))
- `F62` 4 zone(s) touristique(s) sur 103 unités ADM2 (surcroît estival net ≥ 10 %, mois de pointe [12, 1]) : Otavi (Oshana) (+17 %, confiance moyenne), Ongenga (Ohangwena) (+11 %, confiance élevée), Aminius (Ohangwena) (+11 %, confiance moyenne), Tsumkwe (Kunene) (+10 %, confiance moyenne).
- `F63` Indice de saison (base 100 = 2019) : 2014 : 263, 2015 : 200, 2016 : 204, 2017 : 544, 2018 : 277, 2019 : 100, 2020 : 309, 2021 : -65, 2022 : 257, 2023 : 480, 2024 : -159, 2025 : 266. Années avec Ramadan chevauchant la saison : 2021, 2022, 2023, 2024, 2025.
- `F64` Corrélation entre l'indice de saison et international tourist arrivals (WDI) : -0,13 (7 années ; en croissance : -0,62).

## 🏙️ Cas d'usage 8 — Signaux d'urbanisation

- **Question** — Où les villes s'étendent-elles, où les villages s'électrifient-ils, et où la population croît-elle sans lumière ?
- **Données** — VIIRS VNL V2, GHSL GHS-POP / WorldPop, GHSL GHS-BUILT-S R2023A, population urbaine (WDI)
- **Méthode** — Surface éclairée (pixels au-dessus du seuil) et population par unité ; croissances de Theil–Sen ; pixels nouvellement éclairés (sombres deux années de suite au début, éclairés deux années de suite à la fin), séparés entre électrification de zones habitées et nouvelles implantations ; typologie lumière/population.
- **Validation** — Corrélation de rang avec la croissance de la surface bâtie GHSL (source indépendante) (**Spearman ρ = 0,71**)
- **Incertitude** — Persistance exigée sur deux années pour limiter le bruit ; marge de ± 1 point entre croissances avant de classer.
- **Limites** — La lumière mesure l'éclairage extérieur, pas l'urbanisation au sens administratif ; le débordement (blooming) élargit les villes ; la population GHSL est interpolée entre époques.
- **Statut** — `experimental` · Confiance: élevée
- **Références** — Zhou et al. (2015) étendue urbaine par les lumières ; Pesaresi et al. (2023) GHSL ; Min et al. (2013) électrification des villages.
- **Page du tableau de bord** — [`#urban`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/fr/?country=NAM#urban)

**Résultats de cette exécution**

- `F65` Surface éclairée nationale : +11,0 % par an ; population : +1,7 % par an. Classes (ADM2) : Urbanisation électrifiée 86, Croissance équilibrée 7, Croissance non éclairée 7, Stable ou en déclin 3.
- `F66` Entre 2014 et 2025 : 2 678 km² nouvellement éclairés, dont 30 km² de zones déjà habitées (électrification, ≈ 1 k habitants) et 2 648 km² de nouvelles implantations ; 71 km² ont perdu leur lumière.
- `F67` Plus forte extension de la surface éclairée : Outapi (Oshana) (+39,2 %/an), Oshikuku (Oshana) (+35,9 %/an), Kalahari (Ohangwena) (+33,9 %/an), Okongo (Omusati) (+32,7 %/an), Okalongo (Oshana) (+31,0 %/an), Epembe (Omusati) (+30,4 %/an). Croissance non éclairée (population plus rapide que la lumière) : Mariental Rural (Karas), Windhoek East (Khomas), Epupa (Khomas), Khorixas (Khomas), Opuwo (Erongo), Eenhana (Khomas), Okakarara (Khomas).
- `F68` Corrélation de rang (Spearman) entre croissance de la surface éclairée et croissance du bâti GHSL : 0,71 (p = 0,000, 103 unités).

## Limites générales des lumières nocturnes

- **Ce que mesurent les lumières** — Radiance émise vers le haut vers 01 h 30 : l'agriculture, le commerce de jour, les services peu éclairés et l'économie informelle rurale sont mal captés.
- **Saturation et débordement** — DMSP sature au centre des villes (DN 63) et « déborde » (blooming) ; VIIRS est bien meilleur mais le débordement gonfle encore la surface éclairée des villes.
- **Torchères et sites isolés** — Le masque automatique peut retirer des mines, ports ou centrales isolés, et manquer de petites torchères ; les candidats sont exportés pour vérification.
- **Nuages, saisons, lune** — Les mois nuageux sont partiellement observés ; la STL retire la saisonnalité moyenne mais pas une saison anormale (neige, mousson tardive).
- **Ruptures de produit** — DMSP et VIIRS ne sont pas directement comparables : la série longue harmonisée (Li et al., 2020) est un produit modélisé, à lire en tendance seulement.
- **Élasticité NTL–PIB** — Estimée sur 10 à 30 points annuels : intervalles larges, instabilité possible, relation non causale et variable selon le niveau de développement.
- **Accès à l'électricité** — « Habité sans lumière » ≠ « non raccordé » : un foyer raccordé à faible consommation est invisible ; l'indicateur dépend fortement du seuil de radiance et de la population.
- **Limites administratives** — geoBoundaries/GAUL peuvent différer des limites officielles ; les petites unités ADM2 sont sensibles au débordement de la lumière des voisines.
- **Zones industrielles** — La détection repose sur des seuils : une centrale, un port ou un grand centre commercial peut cumuler les signaux ; une usine peu éclairée ou sans émissions visibles échappe à la détection. Sentinel-5P (≈ 5 km) et MODIS (1 km) sont plus grossiers que VIIRS : les signaux NO₂/SO₂/chaleur qualifient un voisinage, pas un bâtiment.
- **Tourisme estival** — Le surcroît estival mesure toute hausse de lumière en été (résidences secondaires, diaspora, fêtes, chantiers), pas seulement le tourisme ; aux hautes latitudes, les nuits d'été très courtes réduisent les observations VIIRS. Le Ramadan modifie l'activité nocturne : les étés concernés sont signalés.
- **Urbanisation** — La surface éclairée dépend du seuil de détection et du débordement de lumière (blooming) autour des villes ; un quartier raccordé mais peu éclairé reste invisible. La population (GHSL/WorldPop) est modélisée à partir des recensements : sa croissance n'est pas une observation indépendante, et les années entre deux millésimes sont interpolées.


---
<sub>Généré par le notebook le 2026-10-30 · version 2.1.0</sub>
