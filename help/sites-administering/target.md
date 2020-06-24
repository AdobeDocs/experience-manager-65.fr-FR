---
title: Intégration à Adobe Target
seo-title: Intégration à Adobe Target
description: Pour en savoir plus sur l’intégration d’AEM à Adobe Target.
seo-description: Pour en savoir plus sur l’intégration d’AEM à Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 93%

---


# Intégration à Adobe Target{#integrating-with-adobe-target}

Dans le cadre d’Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) vous permet d’améliorer la pertinence du contenu en effectuant un ciblage et des mesures sur tous les canaux. Adobe Target est utilisé par les spécialistes marketing pour concevoir et exécuter des tests en ligne, créer des segments ciblés à la volée (en fonction du comportement) et automatiser le ciblage du contenu et les expériences en ligne. AEM a adopté le workflow de ciblage qui est utilisé dans Adobe Target Standard. Si vous utilisez la Cible, vous connaissez bien l’environnement de modification du ciblage dans AEM.

Intégrez vos sites AEM à Adobe Target pour personnaliser le contenu dans vos pages :

* Mettez en œuvre le ciblage du contenu.
* Utilisez les audiences Target pour créer des expériences personnalisées.
* Envoyez des données contextuelles à Target lorsque des visiteurs interagissent avec vos pages.
* Suivez les taux de conversion.

Pour assurer l’intégration à Target, effectuez les tâches suivantes :

1. [Effectuez les tâches préalables nécessaires](/help/sites-administering/target-requirements.md) : inscrivez-vous auprès d’Adobe Target et configurez certains aspects de l’instance de création AEM. Votre compte d’Adobe Target doit disposer au minimum d’autorisations **approbateur **niveau. En outre, vous devez sécuriser les paramètres d’activité sur le nœud de publication afin que celui-ci ne soit pas accessible par les utilisateurs.

1. Procédez de l’une des manières suivantes :

   1. [Adhérez à Adobe Target](/help/sites-administering/opt-in.md) : l’assistant d’inclusion récupère les informations de votre compte Target et crée une configuration cloud Adobe Target et une structure Target. L’assistant associe également vos sites à la structure Target. Si l’assistant ne parvient pas à se connecter à Target, consultez la section relative à la [résolution des incidents de connexion](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems). Vous pouvez ensuite [modifier les configurations cloud par défaut](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations) : si nécessaire, modifiez la configuration et la structure cloud créées par l’assistant de souscription. Par exemple, modifiez la structure pour envoyer des données contextuelles supplémentaires à Target. Si vous souhaitez utiliser Adobe Analytics en tant que source de création de rapports pour Adobe Target, vous devez modifier la configuration cloud pour qu’elle pointe sur la configuration A4T.
   1. [Réalisez une intégration manuelle à Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurez les activités](/help/sites-authoring/activitylib.md) : Associez vos activités à la configuration cloud Target.

>[!NOTE]
>
>Voir aussi la rubrique [Intégration d’AEM à Adobe Target et Adobe Analytics à l’aide de DTM](https://helpx.adobe.com/fr/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Si vous utilisez Target avec une configuration de proxy personnalisée, vous devez configurer les deux configurations de proxy client HTTP, car certaines fonctionnalités d’AEM utilisent les API 3.x et d’autres les API 4.x :
>
>* La version 3.x est configurée avec [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* Les API 4.x sont configurées avec [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>Vous devez sécuriser le nœud de paramètres d’activité **c:ActivitySettings** sur l’instance de publication de sorte qu’il ne soit pas accessible pour les utilisateurs normaux. Le nœud de paramètres d’activité doit être accessible uniquement au service gérant la synchronisation de l’activité avec Adobe Target.
>
>Voir [Préalables à l’intégration à Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) pour plus d’informations.

Une fois l’intégration terminée, vous pouvez [créer du contenu ciblé](/help/sites-authoring/content-targeting-touch.md) qui envoie les données de visiteur à Adobe Target. Notez que les composants de page requièrent un code spécifique pour activer le ciblage du contenu. (consultez [Développement pour le contenu ciblé](/help/sites-developing/target.md)).)

>[!NOTE]
>
>Lorsque vous ciblez un composant dans le mode Auteur AEM, il effectue une série d’appels côté serveur vers Adobe Target afin d’enregistrer la campagne, de configurer des offres et de récupérer des segments Adobe Target (si cela est configuré). Aucun appel côté serveur n’est effectué depuis la publication AEM vers Adobe Target.

## Sources d’informations sur le contexte  {#background-information-sources}

Intégrer AEM à Adobe Target nécessite des connaissances sur Adobe Target, la gestion des activités AEM et la gestion des publics AEM. Vous devez connaître les éléments suivants :

* Adobe Target (consultez la [documentation sur Adobe Target](https://docs.adobe.com/content/help/en/target/using/target-home.html)).
* Console des activités AEM (consultez [Gestion des activités](/help/sites-authoring/activitylib.md)).
* Audiences AEM (voir [Gestion des audiences](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Lorsque vous travaillez avec Adobe Target, le nombre maximal d’artefacts autorisés dans une campagne est le suivant :
>
>* 50 emplacements
>* 2 000 expériences
>* 50 mesures
>* 50 segments de création de rapports
>



