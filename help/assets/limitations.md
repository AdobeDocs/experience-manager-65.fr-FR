---
title: Limites de Dynamic Media
description: Découvrez les bonnes pratiques et les limites appliquées lorsque vous créez une visionneuse d’images ou à 360° ou chargez un PDF. Découvrez également les combinaisons de navigateur web et de système d’exploitation non prises en charge pour Dynamic Media.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
source-git-commit: 9604d950d33e1b5d32ba8141a35059c6e5787aeb
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Limites de Dynamic Media

Les sections suivantes décrivent les limites dans Dynamic Media.

Cette rubrique comprend les sections suivantes :

* [Bonnes pratiques et limites appliquées par Dynamic Media sur les types de ressources](#best-practice-enforced-limits)
* [Combinaisons de navigateur web et de système d’exploitation non prises en charge pour Dynamic Media](#unsupported-browser-os)

## Bonnes pratiques et limites appliquées par Dynamic Media sur les types de ressources {#best-practice-enforced-limits}

Lorsque vous créez une visionneuse à 360° ou une visionneuse d’images, ou que vous chargez des PDF pour l’extraction de page, Adobe recommande les bonnes pratiques suivantes et applique les limites suivantes :

| Ressource - Type de limite | Bonne pratique | Limite imposée | Modification de la limite le 31 décembre 2022 |
| --- | --- | --- | --- |
| **Image** - Nombre de recadrages intelligents par image | 5 | 100 | Non applicable |
| **Tous les jeux** - Nombre de ressources en double par visionneuse | Aucun doublon | 20 | Non applicable |
| **Tous les jeux** - Nombre maximal de ressources par visionneuse | 5 à 10 images par ensemble | 1000 | Non applicable |
| **Visionneuse à 360°** - Nombre maximal de lignes/colonnes par visionneuse 2D | 12 à 18 images par visionneuse | 1000 | Non applicable |
| **PDF** - Nombre maximal de pages qu’un PDF doit prendre en compte pour l’extraction |  | 5000 (pour les nouveaux chargements) | 100 (pour tous les PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Combinaisons de navigateur web et de système d’exploitation non prises en charge pour Dynamic Media {#unsupported-browser-os}

Dynamic Media ne prend pas en charge les combinaisons de navigateur web et de système d’exploitation suivantes.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Mise à jour d’Internet Explorer 11 + Windows Phone 8.1
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

<!-- ## End of support for TLS 1.0 and 1.1 {#tls}

CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022)

Effective September 30, 2022, Adobe Dynamic Media will end support for the following:

* TLS (Transport Layer Security) 1.0 and 1.1
* The following weak ciphers in TLS 1.2:
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_RSA_WITH_AES_256_GCM_SHA384`
  * `TLS_RSA_WITH_AES_256_CBC_SHA256`
  * `TLS_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_AES_128_GCM_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  * `TLS_RSA_WITH_SDES_EDE_CBC_SHA` -->

