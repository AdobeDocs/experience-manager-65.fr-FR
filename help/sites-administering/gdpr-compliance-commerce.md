---
title: AEM Commerce – Préparation pour le RGPD
seo-title: AEM Commerce - GDPR Readiness
description: Découvrez les procédures de gestion des demandes RGPD dans AEM Commerce et comment les utiliser.
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: 3400df1ecd545aa0fb0e3fcdcc24f629ce4c99ba
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 94%

---

# AEM Commerce – Préparation pour le RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>Le RGPD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les réglementations de protection des données et de confidentialité, comme le RGPD et le CCPA.

Le règlement général sur la protection des données (RGPD) de l’Union européenne sur les droits de confidentialité des données entre en vigueur en mai 2018. Consultez la [page consacrée au RGPD dans le centre de traitement des données personnelles d’Adobe](https://www.adobe.com/fr/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Pour plus d’informations, consultez la section [Conformité d’AEM au RGPD](/help/managing/data-protection-and-privacy.md).

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Grâce aux intégrations Commerce prêtes à l’emploi d’Adobe, AEM fait office de couche d’expérience, qui utilise des services et renvoie des données vers la plateforme commerciale du client ou de la cliente qui s’exécute en mode découplé.

Pour certaines plateformes commerciales, nous stockons des informations de profil (`/home/users`) et des jetons commerciaux (pour la connexion à la plateforme commerciale) dans AEM. Pour ces cas d’utilisation, consultez la section [Traiter les requêtes de RGPD pour la plateforme AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Traitement des requêtes de RGPD pour AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

Pour l’intégration de Commerce Cloud Salesforce, AEM Commerce ne stocke aucune information relative au RGPD. Transférez la requête au [cloud Salesforce](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

En ce qui concerne les intégrations Hybris et HCL WebSphere® Commerce, certaines données sont présentes dans AEM. Suivez les [instructions relatives au RGPD d’AEM Platform](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) et posez-vous les questions suivantes :

1. **Où mes données sont-elles stockées/utilisées ?** Les informations de profil utilisateur mises en cache, comme le nom, l’identifiant de l’utilisateur ou de l’utilisatrice de la plateforme commerciale, le jeton, le mot de passe, les coordonnées, etc. sont affichées à partir d’AEM.
1. **Avec qui dois-je partager les données couvertes par le RGPD ?** Toute mise à jour des données relatives au RGPD dans AEM Commerce n’est pas stockée (sauf les informations de profil pertinentes, comme mentionné ci-dessus), mais est renvoyée par proxy vers la plateforme commerciale.
1. **Comment supprimer mes données utilisateur** ? Supprimez le profil utilisateur dans AEM et supprimez la personne utilisatrice sur la plateforme commerciale.

>[!NOTE]
>
>Consultez le [wiki d’Hybris](https://wiki.hybris.com/) ou la [documentation de HCL WebSphere® Commerce](https://help.hcltechsw.com/commerce/index.html), si nécessaire.
