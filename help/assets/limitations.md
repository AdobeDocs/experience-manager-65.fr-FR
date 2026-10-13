---
title: Limites de Dynamic Media
description: Découvrez les bonnes pratiques et les limites appliquées lorsque vous créez un ensemble d’images ou une visionneuse à 360°, ou chargez un PDF. Découvrez également les combinaisons de navigateur web et de système d’exploitation non prises en charge par Dynamic Media.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
  - id: d4b6216b-4a89-4ff0-8ac0-5a699ba23100
    internal-label: Images and videos
subfeature_v2:
  - id: c12bda38-aa1a-4647-b62e-42cd4537dac6
    internal-label: Dynamic Media Classic
  - id: e2dc1259-9034-40fc-a518-b92a34fe6642
    internal-label: Image sets
  - id: cb008a68-9156-4b10-9c66-391409a53067
    internal-label: Spin Sets
  - id: fb5874db-3110-450a-b647-a5c2ce139bef
    internal-label: eCatalog
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 100%
---
# Limites de Dynamic Media

Les sections suivantes décrivent les limites de Dynamic Media.

Cette rubrique comprend les sections suivantes :

* [Bonnes pratiques et limites appliquées par Dynamic Media sur les types de ressources](#best-practice-enforced-limits)
* [Combinaisons de navigateur web et de système d’exploitation non prises en charge par Dynamic Media](#unsupported-browser-os)

## Bonnes pratiques et limites appliquées par Dynamic Media sur les types de ressources {#best-practice-enforced-limits}

Lorsque vous créez une visionneuse à 360° ou un ensemble d’images, ou que vous chargez des PDF pour l’extraction de page, Adobe recommande les bonnes pratiques suivantes et applique les limites ci-dessous :

| Ressource - Type de limite | Bonne pratique | Limite imposée |
| --- | --- | --- |
| **Image** - Nombre de recadrages intelligents par image | 5 | 100 |
| **Tous les jeux** - Nombre de ressources en double par visionneuse | Aucun doublon | 20‡ |
| **Tous les jeux** - Nombre maximal de ressources par visionneuse | 5 à 10 images par ensemble | 1000 |
| **Visionneuse à 360°** - Nombre maximal de lignes/colonnes par visionneuse 2D | 12 à 18 images par visionneuse | 1000 |
| **PDF** - Nombre maximal de pages qu’un PDF doit prendre en compte pour l’extraction |  | 100 (pour tous les PDF) |

‡ La bonne pratique consiste à ne pas avoir de ressources en double dans un ensemble. La limite est de 20 doublons pour une seule ressource. Si vous ajoutez un autre doublon pour cette ressource (dans cet ensemble), la requête renvoie une erreur ou ignore le doublon.
<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Combinaisons de navigateur web et de système d’exploitation non prises en charge par Dynamic Media {#unsupported-browser-os}

Dynamic Media ne prend pas en charge les combinaisons de navigateur web et de système d’exploitation suivantes :

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Mise à jour d’Internet Explorer 11 + Windows Phone 8.1
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

## Fin de la prise en charge de Secure Socket Layer 2.0 et 3.0 et de Transport Layer Security 1.0 et 1.1. {#tls}

<!--
CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022)
-->

À compter du 30 avril 2024, Adobe Dynamic Media ne prendra plus en charge les éléments suivants :

* SSL (Secure Socket Layer) 2.0
* SSL 3.0
* TLS (Transport Layer Security) 1.0 et 1.1
* Les chiffrements faibles suivants dans TLS 1.2 :
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
  * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

