---
title: Règlements sur la protection et la confidentialité des données – Préparation d’Adobe Experience Manager
description: Découvrez la prise en charge d’Adobe Experience Manager pour les différents règlements sur la protection et la confidentialité des données. Il comprend le règlement général sur la protection des données (RGPD) de l’UE, la loi sur la protection de la vie privée des consommateurs de Californie et la manière de se conformer lors de la mise en oeuvre d’un nouveau projet AEM.
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 41%

---

# Préparation d’Adobe Experience Manager pour les règlements sur la protection et la confidentialité des données {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Le contenu de ce document ne constitue pas un avis juridique et ne vise pas à le remplacer.
>
>Consultez le service juridique de votre entreprise pour obtenir des conseils sur les réglementations relatives à la protection des données et à la confidentialité des données.

>[!NOTE]
>
>Pour plus d’informations sur la réponse de l’Adobe aux problèmes de confidentialité et sur ce que cela signifie pour vous en tant que client Adobe, voir [Centre de traitement des données personnelles des Adobes](https://www.adobe.com/fr/privacy.html).

Adobe fournit de la documentation et des procédures (avec des API si elles sont disponibles), afin que l’administrateur de la confidentialité du client ou l’administrateur d’AEM puisse traiter les demandes de protection des données et de confidentialité des données. Il peut vous aider à vous conformer à ces règlements. Les procédures documentées permettent aux clients d’exécuter les demandes de réglementation manuellement ou en appelant vers des API, le cas échéant, à partir d’un portail ou d’un service externe.

>[!CAUTION]
>
>Les informations documentées ici sont limitées à Adobe Experience Manager.
>
>Les données d’un autre service On-demand Adobe, ainsi que toute demande d’accès à des informations personnelles associée, nécessitent des actions à entreprendre sur ce service.
>
>Pour plus d’informations, voir [Centre de traitement des données personnelles des Adobes](https://www.adobe.com/fr/privacy.html).

## Présentation {#introduction}

Les instances d’Adobe Experience Manager et les applications qui s’exécutent sur celles-ci sont détenues et exploitées par les clients Adobe.

Ainsi, les règlements relatifs à la protection des données, telles que le RGPD, le CCPA et d’autres, relèvent, en grande partie, de la responsabilité des clients.

En guise d’introduction, les réglementations relatives à la confidentialité et à la protection des données incluent de nouvelles règles qui seront suivies des rôles suivants :

* Entités commerciales (CCPA) et/ou Contrôleurs de données (RGPD)

* Prestataires (CCPA) et/ou Responsables du traitement des données (GDPR)

Les principales dispositions de ces règlements sont les suivantes :

1. Définition étendue des données personnelles pour inclure tous les identifiants uniques ; comme dans des données identifiables directement et indirectement.

2. Amélioration des exigences en matière de consentement.

3. Accent accru sur les droits de suppression (effacement des données).

4. Droit d’opposition (opt-out) à la vente des données.

Pour Adobe Experience Manager :

* Les instances et les applications qui s’exécutent sur ces instances sont détenues et exploitées par le client.

   * Le client gère les rôles de réglementation, notamment les entités commerciales et les fournisseurs de services, le contrôleur de données et le responsable du traitement des données.

   * Adobe Experience Platform Privacy Service ne fait pas partie du workflow d’AEM, comme illustré dans le diagramme ci-dessous.

* AEM comprend la documentation et les procédures permettant à l’administrateur de confidentialité du client et/ou à l’administrateur AEM d’exécuter les demandes d’accès à des informations personnelles, le cas échéant, manuellement, ou par le biais d’API.

* Aucun nouveau service ou interface utilisateur n’a été ajouté.

   * Au lieu de cela, les procédures et les API sont documentées pour une utilisation par les interfaces utilisateur/portails du client qui gèrent les demandes relatives à la réglementation de la confidentialité.

* AEM n’inclut aucun outil prêt à l’emploi pour prendre en charge le workflow de demandes d’accès à des informations personnelles.

   * Adobe fournit de la documentation et des procédures à l’intention de l’administrateur de la confidentialité et de l’administrateur d’AEM du client, ce qui leur permet d’exécuter manuellement les demandes liées aux réglementations de confidentialité.

Adobe fournit des procédures pour le traitement des demandes d’accès à des informations personnelles liées à l’accès, la suppression et l’exclusion pour Adobe Experience Manager. Il existe parfois des API disponibles qui peuvent être appelées à partir d’un portail développé par le client ou de scripts pour faciliter l’automatisation.

Le diagramme suivant illustre à quoi pourrait ressembler un workflow de demande d’accès à des informations personnelles (illustré à l’aide d’Adobe Experience Manager 6.5) :

![Protection et confidentialité des données](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager et préparation par rapport aux réglementations {#aem-and-regulatory-readiness}

Reportez-vous aux sections ci-dessous pour consulter la documentation relative à la réglementation des domaines d’AEM des produits.

## AEM Foundation {#aem-foundation}

Consultez [Gestion des demandes de protection et de confidentialité des données pour AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM de la collecte de statistiques d’utilisation agrégées {#aem-opting-into-aggregate-usage-statistics-collection}

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

* [Adobe Target – Présentation de la confidentialité](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)

* [Processus relatif à la confidentialité des données Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities accorde aux sujets des données le droit à leur portabilité des données, le droit d’accès et le droit à l’oubli par [API prêtes à l’emploi](/help/communities/user-ugc-management-service.md). Ces API permettent la suppression et l’exportation en masse de contenu généré par l’utilisateur, ainsi que la désactivation des comptes utilisateur identifiés au moyen de leurs ID autorisables. Toutefois, la suppression définitive du compte utilisateur est réalisable par la suppression du noeud utilisateur dans CRXDE Lite, ce qui répond à la nécessité d’un opt-out facile du système.

En outre, AEM Communities offre une confidentialité par conception en raison de sa console de modération en bloc, qui permet aux membres privilégiés de rechercher et de supprimer les contributions et les détails des utilisateurs. La console de gestion des membres permet de limiter au point d’interdire un contributeur. En outre, il autorise les sujets des données à supprimer les contributions qu’ils ont créées.

## AEM Forms {#aem-forms}

AEM Forms comprend des composants et des workflows qui capturent, traitent et stockent des données pour orchestrer les processus d’entreprise et terminer les transactions numériques. Différents composants utilisent différents entrepôts de données et permettent l’intégration à des entrepôts de données personnalisés. La documentation suivante explique les procédures et les directives relatives à l’accès et à la gestion des données utilisateur afin de prendre en charge la protection des données et la confidentialité (par exemple, le RGPD ou le CCPA) pour un composant.

* [Portail Formulaires](/help/forms/using/forms-portal-handling-user-data.md)
* [Correspondence Management](/help/forms/using/correspondence-management-handling-user-data.md)
* [Intégration à Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Workflows basés sur Forms sur OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Workflows Forms JEE](/help/forms/using/forms-workflow-jee-handling-user-data.md) (AEM Forms JEE uniquement)
* [Document Security](/help/forms/using/document-security-handling-user-data.md) (AEM Forms JEE uniquement)
* [Gestion des utilisateurs](/help/forms/using/user-management-handling-user-data.md) (AEM Forms JEE uniquement)
