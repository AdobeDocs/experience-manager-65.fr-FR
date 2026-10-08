---
title: Conservation des données dans AEM Forms
description: Découvrez comment Adobe Experience Manager (AEM) Forms, par défaut, agit comme un serveur intermédiaire et ne stocke pas les données de l’utilisateur final, ce qui est compatible avec la confidentialité des données.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin, User
solution: Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ca1448119778a2bcfeca7189aab5b360d992d99d
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 2%
---
# Conservation des données dans AEM Forms {#data-retention-in-aem-forms}

AEM Forms stocke-t-il les données de formulaire ? Par défaut, non. Adobe Experience Manager (AEM) Forms agit comme un serveur intermédiaire pour les données capturées via Adaptive Forms et ne stocke pas les données de l’utilisateur final dans le référentiel AEM. Au lieu de cela, le serveur transmet les données envoyées à la destination que vous possédez et configurez. Ce comportement par défaut vous aide à atteindre vos objectifs de confidentialité et de conformité des données. Il s’applique à la fois à AEM Forms sur OSGi et à AEM Forms sur JEE.

AEM Forms étant une plateforme extensible, vous pouvez personnaliser AEM pour modifier ce comportement par défaut. Si votre personnalisation stocke les données envoyées par le biais d’un formulaire adaptatif dans le référentiel AEM ou les écrit dans les journaux AEM, vous devez vous assurer que ces données ne sont pas conservées sur vos systèmes de production et d’évaluation.

## Comportement par défaut avec des fonctionnalités prêtes à l’emploi {#default-behavior}

Lorsque vous utilisez des fonctionnalités de Forms adaptatif prêtes à l’emploi, AEM Forms ne stocke pas les données de l’utilisateur final. Le serveur transmet directement les données envoyées à la destination que vous possédez et configurez.

Les mécanismes prêts à l’emploi qui connectent un formulaire à une destination que vous possédez comprennent le modèle de données de formulaire (FDM), les connecteurs prêts à l’emploi et les actions d’envoi. Chacun de ces éléments envoie des données à un emplacement que vous possédez et configurez, afin qu’elles ne soient pas conservées dans le référentiel AEM. Un formulaire peut également appeler un service externe ou tiers, tel qu’une API REST, à partir d’une règle ou d’une action d’envoi, et transférer des données vers ce service sans conserver les données sur AEM.

Si vous utilisez des workflows AEM avec des processus de longue durée impliquant une étape d’approbation, AEM Forms peut conserver des données en mémoire et en stockage temporaire pour terminer l’opération. Pour plus d’informations sur la manière d’empêcher l’enregistrement de ces données sur AEM, reportez-vous à la section [Données dans les processus de workflow de longue durée](#long-lived-workflow-processes).

L’action d’envoi du portail Forms conserve les données capturées ou envoyées via le Forms adaptatif, mais les données sont enregistrées dans un emplacement de stockage que vous fournissez et possédez, et non dans le référentiel ou les journaux AEM. Pour plus d’informations, voir [Action d’envoi Sécuriser les données enregistrées par Forms Portal](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-saved-by-forms-portal-submit-action).

## Données en transit {#data-in-transit}

Bien qu’AEM Forms ne stocke pas les données de l’utilisateur final par défaut, les données continuent de se déplacer entre l’utilisateur final, AEM Forms et la destination que vous configurez. Sécurisez ce trafic à l’aide du protocole TLS (Transport Layer Security) afin que les données soient chiffrées en transit.

Pour sécuriser la connexion entre le navigateur et AEM, activez HTTPS sur l’instance AEM. Pour connaître les étapes, voir [SSL/TLS par défaut](/help/sites-administering/ssl-by-default.md).

En outre, assurez-vous que les points d’entrée auxquels AEM Forms envoie des données, tels que les configurations cloud, les URL d’action d’envoi et les sources de données du modèle de données de formulaire, utilisent des points d’entrée HTTPS sécurisés. Comme AEM Forms ne stocke pas les données qu’il transmet, le chiffrement au repos ne s’applique pas à ces données. Pour plus d’informations sur la sécurisation de la connexion, voir [&#x200B; Couche de transport sécurisée &#x200B;](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-transport-layer).

## Modèle de données de formulaire pour les magasins de données externes {#form-data-model}

Pour lire et écrire des données dans un magasin de données, utilisez un modèle de données de formulaire (FDM). FDM est le mécanisme recommandé pour connecter un formulaire à une source de données que vous possédez et gérez, telle qu’une base de données ou un service web RESTful.

Pour plus d’informations, voir [Présentation de l’intégration de données AEM Forms](/help/forms/using/data-integration.md). Pour plus d’informations sur la sécurisation des données gérées par un FDM, voir [Sécurisation des données gérées par le modèle de données de formulaire (FDM)](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-handled-by-form-data-model-fdm).

## Données dans les processus de workflow de longue durée {#long-lived-workflow-processes}

Si vous utilisez des processus de workflow de longue durée, AEM peut enregistrer les données temporairement dans le cadre de la payload du workflow. Les variables de workflow qui transportent cette payload sont stockées dans les métadonnées de l’instance de workflow dans le référentiel AEM et peuvent contenir des informations d’identification personnelle (PII) ou des données personnelles sensibles (SPD) fournies par les utilisateurs finaux lors du remplissage d’un formulaire adaptatif.

Pour conserver ces données dans un référentiel que vous possédez et gérez, tel que le stockage Blob d’Azure, plutôt que sur AEM, utilisez la fonctionnalité d’externalisation des données d’AEM. Lorsque vous externalisez les variables, les données ne sont pas enregistrées dans le référentiel AEM, mais stockées dans votre propre référentiel de données.

Pour connaître les étapes d’externalisation des données, voir [Paramétrer les données sensibles aux variables de workflow et les stocker dans des entrepôts de données externes](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables).

## Personnalisation et journalisation {#customization-and-logging}

AEM est une solution personnalisable. Si vous personnalisez AEM, assurez-vous que votre personnalisation ne stocke aucune donnée dans le référentiel ou les journaux AEM.

Lorsque vous utilisez les fonctionnalités par défaut, AEM Forms n’écrit pas les données de l’utilisateur final dans les journaux.

Le code personnalisé peut écrire des données dans les journaux. Si vous ajoutez le suivi ou la journalisation pendant le développement, supprimez les traces et les données envoyées aux journaux avant de déployer votre code dans les environnements d’évaluation et de production.

## Questions fréquentes sur la conservation des données dans AEM Forms {#faq}

AEM Forms stocke-t-il les données de formulaire ?**&#x200B;**

Non. Par défaut, Adobe Experience Manager (AEM) Forms agit comme un serveur intermédiaire pour les données capturées par le biais d’Adaptive Forms et ne stocke pas les données de l’utilisateur final dans le référentiel AEM. Le serveur transmet les données envoyées à la destination que vous possédez et configurez, telle qu’une source de données de modèle de données de formulaire, une cible d’action d’envoi ou une API externe. Ce comportement par défaut s’applique à la fois à AEM Forms sur OSGi et à AEM Forms sur JEE.

**Où les données de formulaire adaptatif sont-elles stockées ?**

Les données de formulaire adaptatif envoyées sont stockées dans la destination que vous possédez et configurez, et non dans le référentiel Adobe Experience Manager (AEM). Les mécanismes prêts à l’emploi tels que le modèle de données de formulaire (FDM), les connecteurs et les actions d’envoi envoient des données à votre propre emplacement. Un formulaire peut également transférer des données vers un service externe, tel qu’une API REST, sans les conserver dans AEM. L’action d’envoi du portail Forms enregistre également les données dans un emplacement de stockage que vous fournissez et possédez.

**Les workflows de longue durée stockent-ils les données de formulaire ?**

Les processus de workflow de longue durée dans Adobe Experience Manager (AEM) Forms peuvent enregistrer temporairement les données dans le cadre de la payload du workflow, stockée dans les métadonnées de l’instance de workflow dans le référentiel AEM. Pour conserver ces données dans un référentiel que vous possédez et gérez, tel que le stockage Blob d’Azure, plutôt que sur AEM, utilisez la [fonctionnalité d’externalisation des données d’AEM pour les variables de workflow](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables).

AEM Forms écrit-il des données dans les journaux ?**&#x200B;**

Non. Grâce aux fonctionnalités par défaut, Adobe Experience Manager (AEM) Forms n’écrit pas les données de l’utilisateur final dans les journaux. AEM étant une plateforme personnalisable, le code personnalisé peut écrire des données dans les journaux. Si vous ajoutez le suivi ou la journalisation pendant le développement, supprimez ces traces et toutes les données enregistrées avant le déploiement dans les environnements d’évaluation et de production. Une personnalisation ne doit pas stocker de données dans le référentiel ou les journaux AEM.

**Comment les données sont-elles protégées en transit ?**

Les données en transit sont protégées par le protocole TLS (Transport Layer Security) dans Adobe Experience Manager (AEM) Forms. Activez le protocole HTTPS sur l’instance AEM pour sécuriser la connexion entre le navigateur et AEM. En outre, assurez-vous que les points d’entrée auxquels AEM Forms envoie des données, tels que les configurations cloud, les URL d’action d’envoi et les sources de données du modèle de données de formulaire, utilisent des points d’entrée HTTPS sécurisés. Comme AEM Forms ne stocke pas les données qu’il transmet, le chiffrement au repos ne s’applique pas à ces données.

## Ressources connexes {#related-resources}

* [Présentation de l’intégration des données AEM Forms](/help/forms/using/data-integration.md)
* [Paramétrer les données sensibles aux variables de workflow et les stocker dans des magasins de données externes](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)
* [Configuration de l’action d’envoi](/help/forms/using/configuring-submit-actions.md)
* [Renforcement et sécurisation d’AEM Forms dans un environnement OSGi](/help/forms/using/hardening-securing-aem-forms-environment.md)
