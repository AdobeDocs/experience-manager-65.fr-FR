---
title: AEM Commerce – Préparation pour le RGPD
seo-title: AEM Commerce - GDPR Readiness
description: « AEM Commerce – Préparation pour le RGPD »
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 15%

---

# AEM Commerce – Préparation pour le RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>Le RGPD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les réglementations de protection des données et de confidentialité ; comme le RGPD et le CCPA.

Le règlement général sur la protection des données (RGPD) de l’Union européenne sur les droits de confidentialité des données entre en vigueur en mai 2018. Voir [Page RGPD du Centre de traitement des données personnelles des Adobes](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Voir [AEM Préparation au RGPD](/help/managing/data-protection-and-privacy.md) pour plus de détails.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Avec les intégrations Commerce d’Adobe prêtes à l’emploi, AEM est la couche d’expérience, qui consomme des services et renvoie des données à la plateforme de commerce client qui s’exécute en mode sans interface utilisateur.

Pour certaines plateformes commerciales, Adobe stocke des informations de profil ( `/home/users`) et les jetons commerciaux (pour vous connecter à la plateforme commerciale) dans AEM. Pour ces cas d’utilisation, reportez-vous à la section [Gestion des demandes RGPD pour la plateforme AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Traitement des requêtes de RGPD pour AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

Pour l’intégration du Commerce Cloud Salesforce, AEM Commerce ne stocke aucune information relative au RGPD. Transférez la requête à la fonction [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

Pour les intégrations hybris et HCL WebSphere® Commerce, il existe des données dans AEM. Utilisez la variable [Instructions relatives au RGPD AEM Platform](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) et tenez compte de ces questions :

1. **Où mes données sont-elles stockées/utilisées ?** Les informations de profil utilisateur mises en cache, telles que le nom, l’identifiant d’utilisateur commercial, le jeton, le mot de passe et l’adresse, sont affichées à partir d’AEM.
1. **Avec qui partager les données couvertes par le RGPD ?** Toute mise à jour des données relatives au RGPD dans AEM Commerce n’est pas stockée (à l’exception des informations de profil pertinentes, comme mentionné ci-dessus), mais est renvoyée par proxy vers la plateforme commerciale.
1. **Comment supprimer mes données utilisateur** ? Supprimez le profil utilisateur dans AEM et appelez la suppression de l’utilisateur sur la plateforme commerciale.

>[!NOTE]
>
>Consultez la section [wiki hybris](https://wiki.hybris.com/) ou le [Documentation sur HCL WebSphere® Commerce](https://help.hcltechsw.com/commerce/index.html), si nécessaire.
