---
title: Règlements sur la protection et la confidentialité des données – Préparation d’Adobe Experience Manager
seo-title: Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations; such as GDPR, CCPA, etc
description: Découvrez la prise en charge d’Adobe Experience Manager des différents règlements de protection et de confidentialité des données ; notamment le règlement général sur la protection des données (RGPD) de l’Union européenne, la loi sur la protection de la vie privée des consommateurs de Californie et la manière de s’y conformer lors de la mise en œuvre d’un nouveau projet AEM
seo-description: Learn about Adobe Experience Manager support for the various Data Protection and Data Privacy Regulations; including the EU General Data Protection Regulation (GDPR), the California Consumer Privacy Act and how to comply when implementing a new AEM project.
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 100%

---

# Préparation d’Adobe Experience Manager pour les règlements sur la protection et la confidentialité des données {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Le contenu de ce document ne constitue pas un avis juridique et ne vise pas à le remplacer.
>
>Consultez le service juridique de votre entreprise pour obtenir des conseils concernant les réglementations sur la protection des données et la confidentialité des données.

>[!NOTE]
>
>Pour plus d’informations sur la réponse d’Adobe à ces questions de données personnelles et sur ce que cela signifie pour vous en tant que client Adobe, consultez le [Centre de traitement des données personnelles d’Adobe](https://www.adobe.com/fr/privacy.html).

Adobe propose de la documentation et des procédures (avec des API si disponibles), afin que l’administrateur de confidentialité du client ou l’administrateur AEM traite la protection des données et les demandes d’accès à des informations personnelles et aide nos clients à se conformer à ces règlements. Les procédures décrites permettront aux clients d’exécuter les demandes légales manuellement ou en appelant les API, si disponibles, à partir d’un portail ou d’un service externe.

>[!CAUTION]
>
>Les informations documentées ici sont limitées à Adobe Experience Manager.
>
>Les données d’un autre service à la demande d’Adobe, ainsi que toute demande associée d’accès à des informations personnelles, nécessiteront des actions relatives à ce service.
>
>Pour plus d’informations, voir la section [Centre de traitement des données personnelles d’Adobe](https://www.adobe.com/privacy.html).

## Présentation {#introduction}

Les instances d’Adobe Experience Manager, ainsi que les applications qui s’y exécutent, sont détenues et exploitées par nos clients.

Ainsi, les règlements relatifs à la protection des données, telles que le RGPD, le CCPA et d’autres, relèvent, en grande partie, de la responsabilité des clients.

En guise d’introduction succincte, les règlements relatifs à la confidentialité et à la protection des données incluent de nouvelles règles qui devront être appliquées par les entités exerçant les rôles suivants :

* Entités commerciales (CCPA) et/ou Contrôleurs de données (RGPD)

* Prestataires (CCPA) et/ou Responsables du traitement des données (GDPR)

Les principales dispositions de ces règlements sont les suivantes :

1. Définition étendue des données personnelles pour inclure tous les identifiants uniques ; comme dans des données identifiables directement et indirectement.

2. Amélioration des exigences en matière de consentement.

3. Accent accru sur les droits de suppression (effacement des données).

4. Droit d’opposition (opt-out) à la vente des données.

Pour Adobe Experience Manager :

* Les instances et les applications qui s’exécutent sur ces instances sont détenues et exploitées par le client.

   * Cela signifie effectivement que le client gère les rôles légaux, notamment les entités commerciales et les fournisseurs de services, le contrôleur de données et le responsable du traitement des données.

   * Adobe Experience Platform Privacy Service ne fait pas partie du workflow d’AEM, comme illustré dans le diagramme ci-dessous.

* AEM comprend la documentation et les procédures permettant à l’administrateur de confidentialité du client et/ou à l’administrateur AEM d’exécuter les demandes d’accès à des informations personnelles, le cas échéant, manuellement, ou par le biais d’API.

* Aucun nouveau service ou interface utilisateur n’a été ajouté.

   * Au lieu de cela, les procédures et les API sont documentées pour une utilisation par les interfaces utilisateur/portails du client qui gèrent les demandes relatives à la réglementation de la confidentialité.

* AEM n’inclura aucun outil prêt à l’emploi pour prendre en charge le workflow des demandes d’accès à des informations personnelles.

   * Adobe fournira une documentation et des procédures à l’administrateur de confidentialité du client et/ou à l’administrateur AEM, leur permettant d’exécuter manuellement les demandes liées à la réglementation de la confidentialité.

Adobe fournit des procédures pour le traitement des demandes d’accès à des informations personnelles liées à l’accès, à la suppression et au droit d’opposition pour Adobe Experience Manager. Dans certains cas, des API peuvent être appelées à partir d’un portail développé par le client ou de scripts pour faciliter l’automatisation.

Le diagramme suivant illustre à quoi pourrait ressembler un workflow de demande d’accès à des informations personnelles (illustré à l’aide d’Adobe Experience Manager 6.5) :

![Protection et confidentialité des données](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager et préparation par rapport aux réglementations {#aem-and-regulatory-readiness}

Consultez les sections ci-dessous pour en savoir plus sur la réglementation des domaines de produit d’AEM.

## AEM Foundation {#aem-foundation}

Consultez [Gestion des demandes de protection et de confidentialité des données pour AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## Souscription à la collecte de statistiques d’utilisation agrégées dans AEM {#aem-opting-into-aggregate-usage-statistics-collection}

Voir [Collecte de statistiques d’utilisation agrégées](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Consultez [AEM Sites - Préparation à la protection des données et à la confidentialité.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

Consultez [AEM Commerce - Préparation à la protection des données et à la confidentialité.](/help/sites-administering/gdpr-compliance-commerce.md)

## AEM Mobile {#aem-mobile}

Consultez [AEM Mobile - Préparation à la protection des données et à la confidentialité.](/help/mobile/aem-mobile-gdpr-compliance.md)

## Intégration d’AEM à Adobe Target et Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Ces intégrations d’Adobe Experience Manager s’effectuent avec des services prêts pour la protection des données et la confidentialité (par exemple, le RGPD ou le CCPA). Aucune donnée personnelle provenant d’Adobe Target ou d’Adobe Analytics n’est stockée dans AEM en lien avec les intégrations.
Pour plus d’informations, voir :

* [Adobe Target – Présentation de la confidentialité](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html?lang=fr)

* [Processus relatif à la confidentialité des données Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=fr)

## AEM Communities {#aem-communities}

AEM Communities accorde aux personnes concernées un droit sur la portabilité de leurs données, un droit à l’accès, ainsi qu’un droit à l’oubli à l’aide d’[API prêtes à l’emploi](/help/communities/user-ugc-management-service.md). Ces API permettent une suppression et une exportation en bloc du contenu généré par les utilisateurs, de même que la désactivation des comptes utilisateur identifiés par leur ID autorisable. Toutefois, la suppression définitive d’un compte utilisateur est réalisée par la suppression du nœud de l’utilisateur dans CRXDE Lite, ce qui satisfait la nécessité de disposer d’un moyen facile d’exclusion du système.

En outre, AEM Communities offre la confidentialité de par sa conception en raison de sa console de modération en masse, qui permet aux membres privilégiés de rechercher et de supprimer les contributions et les détails des utilisateurs. La console de gestion des membres permet une limitation pouvant aller jusqu’à l’interdiction d’un contributeur. De plus, elle permet aux personnes concernées de supprimer les contributions qu’elles ont écrites.

## AEM Forms {#aem-forms}

AEM Forms comprend des composants et des workflows qui capturent, traitent et stockent des données de manière à organiser les processus d’entreprise et à effectuer des transactions numériques. Les différents composants utilisent différents magasins de données et permettent également l’intégration avec des magasins de données personnalisés. La documentation suivante explique les procédures et les directives relatives à l’accès et à la gestion des données utilisateur afin de prendre en charge la protection des données et la confidentialité (par exemple, le RGPD ou le CCPA) pour un composant.

* [Portail Formulaires](/help/forms/using/forms-portal-handling-user-data.md)
* [Correspondence Management](/help/forms/using/correspondence-management-handling-user-data.md)
* [Intégration à Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Workflows basés sur Forms sur OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Workflows Forms JEE](/help/forms/using/forms-workflow-jee-handling-user-data.md) (AEM Forms JEE uniquement)
* [Document Security](/help/forms/using/document-security-handling-user-data.md) (AEM Forms JEE uniquement)
* [User Management](/help/forms/using/user-management-handling-user-data.md) (AEM Forms JEE uniquement)
