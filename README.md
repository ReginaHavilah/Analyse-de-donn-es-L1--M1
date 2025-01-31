# Projet1 - Analyse ACP et Classification

## Présentation
Projet réalisé dans le cadre de la L3 ACP par **BADAR & VOEDZO**.

Date de finalisation : **16 novembre 2023**

Ce projet porte sur l'analyse d'un ensemble de données contenant des informations sur **250 clients d'une banque**. L'objectif principal est d'explorer ces données à l'aide de l'**Analyse en Composantes Principales (ACP)** et de techniques de **classification**.

## Données étudiées
Les données analysées incluent les variables suivantes pour chaque client :
- **AGE** : Âge du client
- **RELAT** : Ancienneté de la relation bancaire (en mois)
- **HAVEF** : Montant total des avoirs en épargne financière
- **ENDET** : Taux d'endettement
- **ROCNB** : Nombre de paiements effectués par carte bancaire le mois précédent
- **NTCAS** : Nombre total de cartes bancaires possédées
- **SCORE** : Score attribué par la banque (classification en cinq groupes distincts : A, B, C, D, E)

## Objectifs de l'analyse
1. **Normalisation des données** pour assurer une ACP optimale.
2. **Calcul et interprétation des valeurs propres** pour choisir les axes les plus pertinents.
3. **Représentation des individus et des variables** dans l'espace factoriel.
4. **Identification des individus bien représentés et mal représentés** dans l'ACP.
5. **Calcul des contributions des individus et des variables** aux axes principaux.

## Méthodologie
### Chargement et traitement des données
Les données sont importées sous **R** et prétraitées pour l'ACP :
```r
# Chargement des données
library(FactoMineR)
data <- read.table("clients.txt", header = TRUE)

# Application de l'ACP
result <- PCA(data[,-7])
```

### Sélection des axes pour l'ACP
Les valeurs propres obtenues montrent qu'il faut **retenir cinq axes** afin d'expliquer plus de 80% de la variance totale.

```r
# Affichage des valeurs propres
result$eig
```

### Identification des individus mal représentés
Certains individus sont mal représentés dans l’espace factoriel et sont exclus de l’analyse principale.
```r
# Sélection des individus mal représentés
somme_ligne <- rowSums(result$ind$cos2)
individus_mal_representes <- unique(which(somme_ligne < 0.6))
```

### Analyse des contributions
Les variables et les individus ayant les **contributions les plus élevées** permettent d’interpréter les axes principaux de l’ACP.
```r
# Contributions des individus
result$ind$contrib
```

## Résultats et Interprétation
1. **L'ACP a permis de réduire la dimensionnalité des données** tout en conservant l’essentiel de l’information.
2. **Les individus bien représentés ont une forte contribution sur les axes sélectionnés**, ce qui permet une analyse plus précise de leur comportement bancaire.
3. **Les variables AGE, RELAT et ENDET sont parmi les plus contributives**, influençant fortement les axes de l'ACP.

## Conclusion
Ce projet a permis d’explorer les profils des clients de la banque grâce à l’ACP et la classification. Ces résultats sont utiles pour segmenter les clients selon leurs comportements financiers et améliorer les stratégies de gestion bancaire.
Technologies utilisées

## Langage principal : R

Librairies : FactoMineR, ggplot2, dplyr
---
**Auteurs** : BADAR & VOEDZO  
**Date** : 16 novembre 2023

