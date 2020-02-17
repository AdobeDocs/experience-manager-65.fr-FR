---
title: Règles relatives à la protection des données et à la confidentialité des données - Préparation d’Adobe Experience Manager
seo-title: Règlement sur la préparation d’Adobe Experience Manager pour la protection des données et la confidentialité des données ; tels que RDPC, ACCP, etc.
description: 'Découvrez la prise en charge d’Adobe Experience Manager pour les différentes règles de protection des données et de confidentialité des données ; notamment le Règlement général de protection des données de l’UE (RDPC), la Loi sur la protection des renseignements personnels des consommateurs de Californie et la façon de s’y conformer lors de la mise en oeuvre d’un nouveau projet AEM. '
seo-description: 'Découvrez la prise en charge d’Adobe Experience Manager pour les différentes règles de protection des données et de confidentialité des données ; notamment le Règlement général de protection des données de l’UE (RDPC), la Loi sur la protection des renseignements personnels des consommateurs de Californie et la façon de s’y conformer lors de la mise en oeuvre d’un nouveau projet AEM. '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: grdp
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
translation-type: tm+mt
source-git-commit: 9b16c8ae2ee28c60f35f9e0f990d79173463c33b

---


# Règlement sur la préparation d’Adobe Experience Manager pour la protection des données et la confidentialité des données {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Le contenu de ce document ne constitue pas un avis juridique et ne se substitue pas à un avis juridique.
>
>Veuillez consulter le service juridique de votre entreprise pour obtenir des conseils concernant les règles de protection des données et de confidentialité des données.

>[!NOTE]
>
>Pour plus d’informations sur la réponse d’Adobe aux problèmes de confidentialité et sur ce que cela signifie pour vous en tant que client Adobe, consultez le Centre [de confidentialité d’](https://www.adobe.com/privacy.html)Adobe.

Adobe fournit de la documentation et des procédures (avec des API, le cas échéant), à l’administrateur de la confidentialité des clients ou à l’administrateur AEM pour qu’ils puissent traiter les demandes de protection des données et de confidentialité des données et aider nos clients à se conformer à ces règles. Les procédures documentées permettront aux clients d’exécuter les demandes de réglementation manuellement ou en appelant les API, le cas échéant, à partir d’un portail ou d’un service externe.

>[!CAUTION]
>
>Les détails décrits ici sont limités à Adobe Experience Manager.
>
>Les données provenant d’un autre service à la demande Adobe, ainsi que toute demande de confidentialité associée, nécessiteront des actions à entreprendre sur ce service.
>
>Pour plus d’informations, consultez le Centre [de confidentialité d’](https://www.adobe.com/privacy.html)Adobe.

## Présentation {#introduction}

Les instances d’Adobe Experience Manager et les applications qui s’exécutent dessus sont détenues et exploitées par nos clients.

Par conséquent, les règlements sur la protection des données, comme le RMCT, l&#39;ACCP et d&#39;autres, relèvent en grande partie de la responsabilité des clients.

En guise d&#39;introduction très brève, les règlements sur la protection et la confidentialité des données comprennent de nouvelles règles qui seront suivies des rôles suivants :

* Entités commerciales (ACCP) et/ou contrôleurs de données (RMMR)

* Fournisseurs de services (ACCP) et/ou Processeurs de données (RMMR)

Les principales dispositions de ces règlements sont les suivantes :

1. Définition étendue des données à caractère personnel pour inclure tous les identifiants uniques ; comme dans les données directement et indirectement identifiables.

2. Renforcement des exigences en matière de consentement.

3. Accent accru sur les droits de suppression (effacement des données).

4. Exclusion de la vente de données.

Pour Adobe Experience Manager :

* Les instances et les applications qui s’exécutent dessus sont détenues et exploitées par le client.

   * Cela signifie que le client gère efficacement les rôles de réglementation, notamment les entités commerciales et les fournisseurs de services, le contrôleur de données et le processeur de données.

   * Le service de confidentialité d’Adobe Experience Platform ne fera pas partie du processus pour AEM, comme illustré dans le diagramme ci-dessous.

* AEM inclut la documentation et les procédures permettant à l’administrateur de la confidentialité du client et/ou à l’administrateur AEM d’exécuter les demandes de réglementation de la confidentialité ; soit manuellement, soit par le biais d’API, le cas échéant.

* Aucun nouveau service ou interface utilisateur n’a été ajouté.

   * Les procédures et les API sont plutôt documentées pour être utilisées par les interfaces utilisateur/portails du client qui gèrent les demandes de réglementation de la confidentialité.

* AEM n’inclut aucun outil prêt à l’emploi pour prendre en charge le flux de travaux des demandes de confidentialité.

   * Adobe fournit une documentation et des procédures à l’administrateur de la confidentialité du client et/ou à l’administrateur AEM, lui permettant ainsi d’exécuter manuellement les requêtes liées aux règles de confidentialité.

Adobe fournit des procédures de traitement des demandes de confidentialité liées à Access, Delete et Opt-Out pour Adobe Experience Manager. Dans certains cas, des API peuvent être appelées à partir d’un portail développé par le client ou de scripts pour faciliter l’automatisation.

Le diagramme suivant illustre l’aspect d’un processus de demande de confidentialité (illustré à l’aide d’Adobe Experience Manager 6.5) :

![Protection des données et confidentialité](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager et la préparation à la réglementation {#aem-and-regulatory-readiness}

Consultez les sections ci-dessous pour obtenir de la documentation sur la réglementation des zones de produits d’AEM.

## AEM Foundation {#aem-foundation}

Voir [Gestion des demandes de protection des données et de confidentialité pour AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## Souscription à la collecte de statistiques d’utilisation agrégées dans AEM {#aem-opting-into-aggregate-usage-statistics-collection}

Voir [Collecte de statistiques d’utilisation agrégées](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Reportez-vous à la page Sites [AEM - Protection des données et état de préparation à la confidentialité.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

Reportez-vous à [AEM Commerce - Protection des données et état de préparation](/help/sites-administering/gdpr-compliance-commerce.md)à la confidentialité.

## AEM Mobile {#aem-mobile}

Reportez-vous à [AEM Mobile - Protection des données et état de préparation](/help/mobile/aem-mobile-gdpr-compliance.md)à la confidentialité.

## Intégration d’AEM à Adobe Target et Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Ces intégrations d’Adobe Experience Manager sont associées à des services de protection des données et de confidentialité (par exemple, GDPR ou CCPA). Aucune donnée personnelle provenant d’Adobe Target ou d’Adobe Analytics n’est stockée dans AEM par rapport aux intégrations.
Pour plus d’informations, voir :

* [Adobe Target - Présentation de la confidentialité](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Flux de travaux de confidentialité des données Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities accorde aux personnes concernées un droit sur la portabilité de leurs données, un droit à l’accès, ainsi qu’un droit à l’oubli à l’aide d’[API prêtes à l’emploi](/help/communities/user-ugc-management-service.md). Ces API permettent une suppression et une exportation en bloc du contenu généré par les utilisateurs, de même que la désactivation des comptes utilisateur identifiés par leur ID autorisable. Toutefois, la suppression définitive d’un compte utilisateur est réalisée par la suppression du nœud de l’utilisateur dans CRXDE Lite, ce qui satisfait la nécessité de disposer d’un moyen facile d’exclusion du système.

En outre, AEM Communities offre la confidentialité de par sa conception en raison de sa console de modération en masse, qui permet aux membres privilégiés de rechercher et de supprimer les contributions et les détails des utilisateurs. La console de gestion des membres permet une limitation pouvant aller jusqu’à l’interdiction d’un contributeur. De plus, elle permet aux personnes concernées de supprimer les contributions qu’elles ont écrites.

## AEM Forms {#aem-forms}

AEM Forms comprend des composants et des workflows qui capturent, traitent et stockent des données de manière à organiser les processus d’entreprise et à effectuer des transactions numériques. Les différents composants utilisent différents magasins de données et permettent également l’intégration avec des magasins de données personnalisés. La documentation suivante explique les procédures et les lignes directrices d’accès et de gestion des données utilisateur pour prendre en charge les flux de travail de protection des données et de confidentialité (par exemple, le RDPC ou l’ACCP) pour un composant.

* [Portail Formulaires](/help/forms/using/forms-portal-handling-user-data.md)
* [Correspondence Management](/help/forms/using/correspondence-management-handling-user-data.md)
* [Intégration à Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Workflows basés sur Forms sur OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Workflows Forms JEE](/help/forms/using/forms-workflow-jee-handling-user-data.md) (AEM Forms JEE uniquement)
* [Document Security](/help/forms/using/document-security-handling-user-data.md) (AEM Forms JEE uniquement)
* [User Management](/help/forms/using/user-management-handling-user-data.md) (AEM Forms JEE uniquement)
