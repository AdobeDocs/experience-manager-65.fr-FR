---
title: Obsolescence des informations d’identification JWT dans Adobe Developer Console
description: Découvrez l’impact de l’obsolescence des informations d’identification JWT dans Adobe Developer Console sur AEM.
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 58%

---

# Obsolescence des informations d’identification JWT dans Adobe Developer Console {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service doit référencer [cet article](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) pour plus d’informations.

Les clientes et clients Adobe utilisent [Adobe Developer Console](https://developer.adobe.com/console) pour générer des informations d’identification qui permettent l’accès à diverses API. Les clientes et clients effectuent un choix parmi différents types d’informations d’identification, allant d’OAuth serveur à serveur jusqu’à l’application monopage. L’un de ces types d’informations d’identification, celui des informations d’identification du compte de service (JWT), a été abandonné au profit des informations d’identification OAuth serveur à serveur. Les informations d’identification du nouveau compte de service (JWT) ne peuvent plus être créées à partir du 3 juin 2024, et les informations d’identification JWT existantes ne fonctionneront plus à partir du 27 janvier 2025. Vous pouvez [en savoir plus sur l’obsolescence](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Cet article fournit un contexte supplémentaire sur la façon dont les clients AEM 6.5 doivent gérer l’obsolescence.

À ce stade, la principale leçon à retenir est que les fonctionnalités AEM ne prennent pas encore en charge les nouvelles informations d’identification OAuth serveur à serveur. La prise en charge sera bientôt disponible, d’ici la fin avril 2024 par le biais d’un package de compatibilité spécial à installer pour AEM 6.5, si vous exécutez le dernier pack de services 20 ou version antérieure (le pack de services 21 et versions ultérieures l’inclura automatiquement). Vous avez peut-être reçu un e-mail contenant des instructions pour migrer vos informations d’identification JWT, mais vous pouvez et devriez attendre avant de migrer des informations d’identification jusqu’à ce qu’AEM prenne en charge le nouveau type d’informations d’identification OAuth serveur à serveur.

Les sections ci-dessous répertorient les scénarios dans lesquels les clients doivent (ou ne doivent pas) remplacer leurs informations d’identification de compte de service (JWT) par des informations d’identification de serveur à serveur OAuth, une fois qu’AEM les aura prises en charge à la fin du mois d’avril. [Lisez comment](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) remplacer les informations d’identification ultérieurement.

## Intégrer AEM à d’autres solutions Adobe {#integrating-aem-with-other-adobe-solutions}

**Action**: attendez la fin du mois d’avril 2024 pour effectuer la migration, lorsqu’AEM la prendra en charge.

**Versions AEM pertinentes**: Adobe Managed Services (pack de services 20 et versions ultérieures).


Les clientes et clients AEM utilisent l’interface utilisateur de création AEM pour configurer des intégrations à toutes les autres solutions Adobe. Par exemple, Adobe Target, Adobe Analytics, Adobe Launch, AFCS, etc.

![Intégrer AEM à d’autres solutions](/help/sites-administering/assets/jwt-deprecation.png)

Par exemple, voici les [instructions](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=fr) pour configurer l’intégration à Adobe Target. La clé API dans le [Réalisation de la configuration IMS dans AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=fr#completing-the-ims-configuration-in-aem) doit être migré vers le type d’informations d’identification de serveur à serveur OAuth, une fois qu’AEM prend en charge ces informations d’identification à la fin du mois d’avril. Ces instructions seront mises à jour fin avril afin de vous aider à appliquer les nouvelles informations d’identification de serveur à serveur OAuth.

## API Cloud Manager {#cloud-manager-apis}

**Action**: attendez la fin du mois d’avril 2024 pour effectuer la migration, lorsqu’AEM la prendra en charge.

**Versions AEM pertinentes**: Adobe Managed Services (pack de services 20 et versions ultérieures).

Les clientes et clients créent des projets Adobe Developer Console pour pouvoir appeler les [API Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Les informations d’identification du projet Adobe Developer doivent être migrées vers le type OAuth serveur à serveur, une fois qu’AEM et Cloud Manager les prendront en charge.
