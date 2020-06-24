---
title: Conditions préalables à l’intégration à Adobe Target
seo-title: Conditions préalables à l’intégration à Adobe Target
description: Découvrez les conditions requises pour l’intégration avec Adobe Target.
seo-description: Découvrez les conditions requises pour l’intégration avec Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 63%

---


# Conditions préalables à l’intégration à Adobe Target{#prerequisites-for-integrating-with-adobe-target}

As part of the [integration of AEM and Adobe Target](/help/sites-administering/target.md), you need to register with Adobe Target, configure the replication agent, and secure activity settings on the publish node.

## Inscription à Adobe Target {#registering-with-adobe-target}

Pour intégrer AEM à Adobe Target, vous devez disposer d’un compte Adobe Target valide. This account must have **approver** level permissions at a minimum. Lorsque vous vous inscrivez à Adobe Target, vous recevez un code client. Vous avez besoin du code client et de vos nom d’utilisateur et mot de passe Adobe Target pour connecter AEM à Adobe Target.

Le code client identifie le compte client Adobe Target en appelant le serveur Adobe Target.

>[!NOTE]
>
>Votre compte doit également être activé par l’équipe Target pour pouvoir utiliser l’intégration.
>
>If it is not the case, please contact [Adobe Customer Care](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html).

## Activation de l’agent de réplication Target {#enabling-the-target-replication-agent}

The Test and Target [replication agent](/help/sites-deploying/replication.md) must be enabled on the author instance. Note that this replication agent is not enabled by default if you used the [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) run mode for installing AEM. Pour plus d’informations sur la sécurisation de votre environnement de production, voir [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md).

1. Sur la page d’accueil d’AEM, cliquez ou appuyez sur **Outils** > **Déploiement** > **Réplication**.
1. Cliquez ou appuyez sur **Agents sur l’auteur**.
1. Cliquez ou appuyez sur l’agent de réplication **Test&amp;Target**, puis cliquez ou appuyez sur **Modifier**.
1. Sélectionnez l’option Activé, puis cliquez ou appuyez sur **OK**.

   >[!NOTE]
   >
   >Lorsque vous configurez l’agent de réplication Test&amp;Target, sous l’onglet **transport**, l’URI est défini par défaut sur **tnt:///**. Do not replace this URI with **https://admin.testandtarget.omniture.com**.
   >
   >Veuillez noter que si vous tentez de tester la connexion avec **tnt:///**, elle renvoie une erreur. This is expected behavior as this URI is for internal use only and should not be used with **Test Connection**.

## Sécurisation du nœud de paramètres d’activité {#securing-the-activity-settings-node}

Vous devez sécuriser le nœud de paramètres d’activité **c:ActivitySettings** sur l’instance de publication de sorte qu’il ne soit pas accessible pour les utilisateurs normaux. Le nœud de paramètres d’activité doit être accessible uniquement au service gérant la synchronisation de l’activité avec Adobe Target.

The **cq:ActivitySettings** node is available in CRXDE lite under `/content/campaigns/*nameofbrand*`* *under the activities jcr:content node;* *for example `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Ce nœud est créé après que vous ciblez un composant.

The **cq:ActivitySettings** node under the activity&#39;s jcr:content is protected by the following ACLs:

* Tout refuser pour tout le monde
* Autoriser jcr:read,rep:write pour target-activity-authors (l’auteur est membre de ce groupe par défaut)
* Autoriser jcr:read,rep:write pour targetservice

Ces paramètres permettent de garantir que les utilisateurs ordinaires n’ont pas accès aux propriétés de nœud. Utilisez les mêmes listes ACL sur les instances de création et de publication. See [User Administration and Security](/help/sites-administering/security.md) for more information.

## Configuring the AEM Link Externalizer {#configuring-the-aem-link-externalizer}

Lors de la modification d’une activité dans Adobe Target, l’URL pointe sur **localhost**, à moins que vous ne modifiiez l’URL sur le nœud de création AEM. Vous pouvez configurer AEM Link Externalizer si vous souhaitez que le contenu exporté pointe vers un domaine de *publication* spécifique.

>[!NOTE]
>
>Voir aussi [Ajouter la configuration](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)de Cloud.

Pour configurer l’externaliseur AEM :

>[!NOTE]
>
>For more details see [Externalizing URLs](/help/sites-developing/externalizer.md).

1. Navigate to the OSGi web console at **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Recherchez **Day CQ Link Externalizer** et saisissez le domaine du nœud de création.

   ![chlimage_1-120](assets/aem-externalizer-01.png)

