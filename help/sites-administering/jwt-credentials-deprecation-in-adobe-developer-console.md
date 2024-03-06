---
title: Obsolescence des informations d’identification JWT dans Adobe Developer Console
description: Découvrez l’impact de l’obsolescence des informations d’identification JWT dans Adobe Developer Console sur AEM.
source-git-commit: 72974d27fecbd9c242f66e203b02463c22b93108
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 80%

---


# Obsolescence des informations d’identification JWT dans Adobe Developer Console {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud service doit faire référence [cet article](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) pour plus d’informations.

Les clientes et clients Adobe utilisent [Adobe Developer Console](https://developer.adobe.com/console) pour générer des informations d’identification qui permettent l’accès à diverses API. Les clientes et clients effectuent un choix parmi différents types d’informations d’identification, allant d’OAuth serveur à serveur jusqu’à l’application monopage. L’un de ces types d’informations d’identification, celui des informations d’identification du compte de service (JWT), a été abandonné au profit des informations d’identification OAuth serveur à serveur. Les informations d’identification du nouveau compte de service (JWT) ne peuvent plus être créées à partir du 1er mai 2024, et les informations d’identification JWT existantes ne fonctionneront plus à partir du 1er janvier 2025. Vous pouvez [en savoir plus sur l’obsolescence](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Cet article fournit un contexte supplémentaire sur la manière dont AEM clients 6.5 doivent gérer l’obsolescence.

À ce stade, la principale leçon à retenir est que les fonctionnalités AEM ne prennent pas encore en charge les nouvelles informations d’identification OAuth serveur à serveur. La prise en charge sera assurée prochainement : d’ici la mi-avril 2024 via un package de compatibilité spécial à installer pour AEM 6.5, si vous exécutez le dernier Service Pack 20 ou version antérieure (Service Pack 21 et version ultérieure l’inclura automatiquement). Vous avez peut-être reçu un e-mail contenant des instructions pour migrer vos informations d’identification JWT, mais vous pouvez et devriez attendre la migration des informations d’identification jusqu’à ce qu’AEM prenne en charge le nouveau type d’informations d’identification OAuth serveur à serveur.

Les sections ci-dessous répertorient les scénarios où les clientes et clients doivent (ou dans certains cas ne doivent pas) remplacer leurs informations d’identification de compte de service (JWT) par des informations d’identification OAuth serveur à serveur, une fois qu’AEM les prend en charge à la mi-avril. [Lisez comment](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) remplacer les informations d’identification ultérieurement.

## Intégrer AEM à d’autres solutions Adobe {#integrating-aem-with-other-adobe-solutions}

**Action** : patientez jusqu’à la mi-avril 2024, date à laquelle AEM les prendra en charge.

**Versions d’AEM pertinentes**: Adobe Managed Services (Service Pack 20 et versions antérieures).


Les clientes et clients AEM utilisent l’interface utilisateur de création AEM pour configurer des intégrations à toutes les autres solutions Adobe. Par exemple, Adobe Target, Adobe Analytics, Adobe Launch, AFCS, etc.

![Intégrer AEM à d’autres solutions](/help/sites-administering/assets/jwt-deprecation.png)

Par exemple, voici les [instructions](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=fr) pour configurer l’intégration à Adobe Target. La clé API dans la section [Réalisation de la configuration IMS dans AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=fr#completing-the-ims-configuration-in-aem) doit être migrée vers le type d’informations d’identification OAuth serveur à serveur, une fois qu’AEM prendra en charge ces informations d’identification à la mi-avril. Ces instructions seront mises à jour à la mi-avril afin de vous aider à appliquer les nouvelles informations d’identification OAuth serveur à serveur.

## API Cloud Manager {#cloud-manager-apis}

**Action** : patientez jusqu’à la mi-avril 2024, date à laquelle AEM les prendra en charge.

**Versions d’AEM pertinentes**: Adobe Managed Services (Service Pack 20 et versions antérieures).

Les clientes et clients créent des projets Adobe Developer Console pour pouvoir appeler les [API Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Les informations d’identification du projet Adobe Developer doivent être migrées vers le type OAuth serveur à serveur, une fois qu’AEM et Cloud Manager les prendront en charge.
