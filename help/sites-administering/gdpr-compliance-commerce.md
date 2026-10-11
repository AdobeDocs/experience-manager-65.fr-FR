---
title: AEM Commerce – Préparation au RGPD
description: Découvrez les procédures de gestion des demandes RGPD dans AEM Commerce et apprenez à les utiliser.
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Developer, Leader, User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c42c36cf-eeed-484a-8b39-a33a68192a07
    internal-label: Compliance
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 80%
---
# AEM Commerce – Préparation au RGPD{#aem-commerce-gdpr-readiness}

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

1. **Où mes données sont-elles stockées/utilisées ?** Informations de profil utilisateur mises en cache telles que le nom, l’identifiant de l’utilisateur commercial, le jeton, le mot de passe et l’adresse, comme indiqué depuis AEM.
1. **Avec qui dois-je partager les données couvertes par le RGPD ?** Toute mise à jour des données relatives au RGPD dans AEM Commerce n’est pas stockée (sauf les informations de profil pertinentes, comme mentionné ci-dessus), mais est renvoyée par proxy vers la plateforme commerciale.
1. **Comment supprimer mes données utilisateur** ? Supprimez le profil utilisateur dans AEM et supprimez la personne utilisatrice sur la plateforme commerciale.

>[!NOTE]
>
>Consultez le [wiki d’Hybris](https://wiki.hybris.com/) ou la [documentation de HCL WebSphere® Commerce](https://help.hcltechsw.com/commerce/index.html), si nécessaire.
