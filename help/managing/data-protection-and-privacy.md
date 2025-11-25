---
title: Règlements sur la protection et la confidentialité des données – Préparation d’Adobe Experience Manager
description: Découvrez la prise en charge d’Adobe Experience Manager pour les règlements sur la protection et la confidentialité des données. Cela comprend le Règlement général sur la protection des données (RGPD) de l’UE, la loi sur la protection de la vie privée des consommateurs et consommatrices de Californie (California Consumer Privacy Act) et la manière de s’y conformer lors de la mise en œuvre d’un nouveau projet AEM.
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer, Leader, User
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 100%

---

# Préparation d’Adobe Experience Manager pour les règlements sur la protection et la confidentialité des données {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Le contenu de ce document ne constitue pas un avis juridique et ne vise pas à le remplacer.
>
>Consultez le service juridique de votre entreprise pour obtenir des conseils concernant les réglementations sur la protection et la confidentialité des données.

>[!NOTE]
>
>Pour plus d’informations sur la réponse d’Adobe aux problèmes de confidentialité et sur ce que cela signifie pour vous en tant que client ou cliente Adobe, voir [Centre de traitement des données personnelles d’Adobe](https://www.adobe.com/fr/privacy.html).

Adobe fournit de la documentation et des procédures (avec des API si elles sont disponibles), afin que l’administrateur ou l’administratrice de la confidentialité du client ou de la cliente ou l’administrateur ou l’administratrice d’AEM puisse traiter les demandes de protection et de confidentialité des données. Celles-ci pourront vous aider à vous conformer à ces règlements. Les procédures décrites permettent aux clients et aux clientes d’exécuter les demandes légales manuellement ou en appelant les API, si disponibles, à partir d’un portail ou d’un service externe.

>[!CAUTION]
>
>Les informations documentées ici sont limitées à Adobe Experience Manager.
>
>Les données d’un autre service à la demande d’Adobe, ainsi que toute demande associée d’accès à des informations personnelles, nécessitent des actions relatives à ce service.
>
>Pour plus d’informations, voir la section [Centre de traitement des données personnelles d’Adobe](https://www.adobe.com/fr/privacy.html).

## Présentation {#introduction}

Les instances d’Adobe Experience Manager, ainsi que les applications qui s’y exécutent, sont détenues et exploitées par nos clients et clientes d’Adobe.

Ainsi, les règlements relatifs à la protection des données, telles que le RGPD, le CCPA et d’autres, relèvent, en grande partie, de la responsabilité des clients et clientes.

En guise de petite introduction, les règlements relatifs à la confidentialité et à la protection des données incluent de nouvelles règles qui devront être appliquées par les entités exerçant les rôles suivants :

* Entités commerciales (CCPA) et/ou Contrôleurs de données (RGPD)

* Prestataires (CCPA) et/ou Responsables du traitement des données (RGPD)

Les principales dispositions de ces règlements sont les suivantes :

1. Définition étendue des données personnelles pour inclure tous les identifiants uniques ; comme dans des données identifiables directement et indirectement.

2. Amélioration des exigences en matière de consentement.

3. Accent accru sur les droits de suppression (effacement des données).

4. Droit d’opposition (opt-out) à la vente des données.

Pour Adobe Experience Manager :

* Les instances, ainsi que les applications qui s’y exécutent, sont détenues et exploitées par les clients et clientes.

   * Le client ou la cliente gère les rôles légaux, notamment les entités commerciales et les fournisseurs de services, le contrôleur de données et le responsable du traitement des données, entre autres.

   * Adobe Experience Platform Privacy Service ne fait pas partie du workflow d’AEM, comme illustré dans le diagramme ci-dessous.

* AEM comprend la documentation et les procédures permettant à l’administrateur de confidentialité du client et/ou à l’administrateur AEM d’exécuter les demandes d’accès à des informations personnelles, le cas échéant, manuellement, ou par le biais d’API.

* Aucun nouveau service ou interface utilisateur n’a été ajouté.

   * Au lieu de cela, les procédures et les API sont documentées pour une utilisation par les interfaces utilisateur/portails du client qui gèrent les demandes relatives à la réglementation de la confidentialité.

* AEM n’inclut aucun outil prêt à l’emploi pour prendre en charge le workflow des demandes d’accès à des informations personnelles.

   * Adobe fournit une documentation et des procédures à l’administrateur ou l’administratrice de confidentialité du client ou de la cliente et/ou à l’administrateur ou l’administratrice AEM, leur permettant d’exécuter manuellement les demandes liées aux règlements de confidentialité.

Adobe fournit des procédures pour le traitement des demandes d’accès à des informations personnelles liées à l’accès, à la suppression et au droit d’opposition pour Adobe Experience Manager. Dans certains cas, des API peuvent être appelées à partir d’un portail développé par le client ou la cliente ou de scripts pour faciliter l’automatisation.

Le diagramme suivant illustre à quoi pourrait ressembler un workflow de demande d’accès à des informations personnelles (illustré à l’aide d’Adobe Experience Manager 6.5) :

![Protection et confidentialité des données](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager et préparation par rapport aux réglementations {#aem-and-regulatory-readiness}

Veuillez consulter les sections ci-dessous pour en savoir plus sur la documentation relative à la réglementation des domaines de produit d’AEM.

## AEM Foundation {#aem-foundation}

Consultez [Gestion des demandes de protection et de confidentialité des données pour AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## Souscription AEM à la collecte de statistiques d’utilisation agrégées {#aem-opting-into-aggregate-usage-statistics-collection}

Voir [Collecte des statistiques d’utilisation agrégées](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Consultez [AEM Sites - Préparation à la protection des données et à la confidentialité.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

Consultez [AEM Commerce - Préparation à la protection des données et à la confidentialité.](/help/sites-administering/gdpr-compliance-commerce.md)

## AEM Mobile {#aem-mobile}

Consultez [AEM Mobile - Préparation à la protection des données et à la confidentialité.](/help/mobile/aem-mobile-gdpr-compliance.md)

## Intégration d’AEM à Adobe Target et Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Ces intégrations d’Adobe Experience Manager s’effectuent avec des services prêts pour la protection des données et la confidentialité (par exemple, le RGPD ou le CCPA). Aucune donnée personnelle provenant d’Adobe Target ou d’Adobe Analytics n’est stockée dans AEM en lien avec les intégrations.

Pour plus d’informations, consultez les sections suivantes :

* [Adobe Target – Présentation de la confidentialité](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=fr)

* [Processus relatif à la confidentialité des données Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities accorde aux titulaires de données le droit à la portabilité des données, le droit d’accès et le droit à l’oubli par des [API prêtes à l’emploi](/help/communities/user-ugc-management-service.md). Ces API permettent une suppression et une exportation en bloc du contenu créé par l’utilisateur ou l’utilisatrice, de même que la désactivation des comptes d’utilisateurs identifiés par leur ID autorisable. Toutefois, la suppression définitive du compte d’utilisateur est réalisable par la suppression du nœud utilisateur dans CRXDE Lite, ce qui répond à la nécessité d’un droit d’opposition facile du système.

En outre, AEM Communities offre par défaut une confidentialité en raison de sa console de modération en bloc, qui permet aux membres privilégiés de rechercher et de supprimer les contributions et les détails des utilisateurs et utilisatrices. La console de gestion des membres permet de limiter au point d’interdire un contributeur ou une contributrice. En outre, il autorise les titulaires de données à supprimer les contributions qu’ils ont créées.

## AEM Forms {#aem-forms}

AEM Forms comprend des composants et des workflows qui capturent, traitent et stockent des données pour orchestrer les processus d’entreprise et terminer les transactions numériques. Différents composants utilisent différents magasins de données et permettent l’intégration à des magasins de données personnalisés. La documentation suivante explique les procédures et les directives relatives à l’accès et à la gestion des données utilisateur afin de prendre en charge la protection des données et la confidentialité (par exemple, le RGPD ou le CCPA) pour un composant.

* [Portail Formulaires](/help/forms/using/forms-portal-handling-user-data.md)
* [Correspondence Management](/help/forms/using/correspondence-management-handling-user-data.md)
* [Intégration à Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Workflows basés sur Forms sur OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Workflows Forms JEE](/help/forms/using/forms-workflow-jee-handling-user-data.md) (AEM Forms JEE uniquement)
* [Sécurité des documents](/help/forms/using/document-security-handling-user-data.md) (AEM Forms JEE uniquement)
* [Gestion des utilisateurs et des utilisatrices](/help/forms/using/user-management-handling-user-data.md) (AEM Forms JEE uniquement)
