---
title: Intégration à Adobe Target
seo-title: Intégration à Adobe Target
description: Pour en savoir plus sur l’intégration d’AEM à Adobe Target.
seo-description: Pour en savoir plus sur l’intégration d’AEM à Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Intégration à Adobe Target{#integrating-with-adobe-target}

As part of the Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) lets you increase content relevance through targeting and measuring across all channels. Adobe Target est utilisé par les marketeurs pour concevoir et exécuter des tests en ligne, créer des segments de public à la volée (en fonction du comportement) et automatiser le ciblage du contenu et les expériences en ligne. AEM a adopté le workflow de ciblage qui est utilisé dans Adobe Target Standard. Si vous utilisez Target, vous serez familiarisé avec l’environnement de modification du ciblage dans AEM.

Intégrez vos sites AEM à Adobe Target pour personnaliser le contenu dans vos pages :

* Mettez en œuvre le ciblage du contenu.
* Utilisez les publics cibles pour créer des expériences personnalisées.
* Envoyez des données contextuelles à Target lorsque des visiteurs interagissent avec vos pages.
* Suivez les taux de conversion.

Pour assurer l’intégration à Target, effectuez les tâches suivantes :

1. [Effectuez les tâches préalables nécessaires](/help/sites-administering/target-requirements.md) : inscrivez-vous auprès d’Adobe Target et configurez certains aspects de l’instance de création AEM. Votre compte Adobe Target doit disposer au minimum d’autorisations **approbateur **niveau. En outre, vous devez sécuriser les paramètres d’activité sur le nœud de publication afin que celui-ci ne soit pas accessible pour les utilisateurs.

1. Procédez de l’une des manières suivantes :

   1. [Adhérez à Adobe Target](/help/sites-administering/opt-in.md) : l’assistant d’inclusion récupère les informations de votre compte Target et crée une configuration cloud Adobe Target et une structure Target. L’assistant associe également vos sites à la structure Target. Si l’assistant ne parvient pas à se connecter à Target, consultez la section relative à la [résolution des incidents de connexion](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems). Vous pouvez ensuite [modifier les configurations cloud par défaut](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations) : si nécessaire, modifiez la configuration et la structure cloud créées par l’assistant de souscription. Par exemple, modifiez la structure pour envoyer des données contextuelles supplémentaires à Target. Si vous souhaitez utiliser Adobe Analytics en tant que source de création de rapports pour Adobe Target, vous devez modifier la configuration cloud pour qu’elle pointe sur la configuration A4T.
   1. [Réalisez une intégration manuelle à Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurez les activités](/help/sites-authoring/activitylib.md) : Associez vos activités à la configuration cloud Target.

>[!NOTE]
>
>Voir aussi la rubrique [Intégration d’AEM à Adobe Target et Adobe Analytics à l’aide de DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Si vous utilisez Target avec une configuration de proxy personnalisée, vous devez configurer les deux configurations de proxy client HTTP, car certaines fonctionnalités d’AEM utilisent les API 3.x et d’autres les API 4.x :
>
>* 3.x is configured with [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* Les API 4.x sont configurées avec [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>Vous devez sécuriser le nœud de paramètres d’activité **c:ActivitySettings** sur l’instance de publication de sorte qu’il ne soit pas accessible pour les utilisateurs normaux. Le nœud de paramètres d’activité doit être accessible uniquement au service gérant la synchronisation de l’activité avec Adobe Target.
>
>Voir [Préalables à l’intégration à Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) pour plus d’informations.

When the integration is complete, you can [author targeted content](/help/sites-authoring/content-targeting-touch.md) that sends visitor data to Adobe Target. Notez que les composants de page nécessitent un code spécifique pour activer le ciblage de contenu. (See [Developing for Targeted Content](/help/sites-developing/target.md).)

>[!NOTE]
>
>Lorsque vous ciblez un composant dans le mode Auteur AEM, il effectue une série d’appels côté serveur vers Adobe Target afin d’enregistrer la campagne, de configurer des offres et de récupérer des segments Adobe Target (si cela est configuré). Aucun appel côté serveur n’est effectué depuis la publication AEM vers Adobe Target.

## Sources d’informations en arrière-plan {#background-information-sources}

Intégrer AEM à Adobe Target nécessite des connaissances sur Adobe Target, la gestion des activités AEM et la gestion des publics AEM. Vous devez connaître les informations suivantes :

* Adobe Target (See the [Adobe Target documentation](https://marketing.adobe.com/resources/help/en_US/target/)).
* AEM Activities console (See [Managing Activities](/help/sites-authoring/activitylib.md)).
* Publics AEM (voir [Gestion des publics](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Lorsque vous travaillez avec Adobe Target, le nombre maximal d’artefacts autorisés dans une campagne est le suivant :
>
>* 50 emplacements
>* 2 000 expériences
>* 50 mesures
>* 50 segments de création de rapports
>



