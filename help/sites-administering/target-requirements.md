---
title: Conditions préalables à l’intégration à Adobe Target
description: Découvrez les conditions préalables à l’intégration à Adobe Target.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 65%

---

# Conditions préalables à l’intégration à Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Dans le cadre de l’[intégration d’AEM et Adobe Target](/help/sites-administering/target.md), vous devez vous inscrire à Adobe Target, configurer l’agent de réplication et sécuriser les paramètres d’activité sur le nœud de publication.

## Enregistrement auprès d’Adobe Target {#registering-with-adobe-target}

Pour intégrer AEM à Adobe Target, vous devez disposer d’un compte Adobe Target valide. Ce compte doit disposer au minimum des permissions de niveau **approbateur**. Lorsque vous vous inscrivez à Adobe Target, vous recevez un code client. Vous avez besoin du code client et de votre nom d’utilisateur et mot de passe Adobe Target pour vous connecter AEM à Adobe Target.

Le code client identifie le compte client Adobe Target lors de l’appel du serveur Adobe Target.

>[!NOTE]
>
>Votre compte doit également être activé par l’équipe Target pour utiliser l’intégration.
>
>Si ce n’est pas le cas, contactez [Adobe de l’assistance clientèle](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?lang=fr).

## Activation de l’agent de réplication Target {#enabling-the-target-replication-agent}

L’[agent de réplication](/help/sites-deploying/replication.md) Test&amp;Target doit être activé sur l’instance de création. Notez que cet agent de réplication n’est pas activé par défaut si vous utilisez le mode d’exécution [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) pour installer AEM. Pour plus d’informations sur la sécurisation de votre environnement de production, voir [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md).

1. Sur la page d’accueil AEM, cliquez ou appuyez sur **Outils** > **Déploiement** > **Réplication**.
1. Cliquez ou appuyez sur **Agents sur l’auteur**.
1. Cliquez ou appuyez sur **Test et ciblage (test et cible)** agent de réplication, puis cliquez ou appuyez sur **Modifier**.
1. Sélectionnez l’option Activé , puis cliquez ou appuyez sur **OK**.

   >[!NOTE]
   >
   >Lorsque vous configurez l’agent de réplication Test&amp;Target, sous l’onglet **transport**, l’URI est défini par défaut sur **tnt:///**. Ne remplacez pas cet URI par **https://admin.testandtarget.omniture.com**.
   >
   >Si vous essayez de tester la connexion avec **tnt:///**, il renvoie une erreur. Ce comportement est attendu, car cet URI est réservé à un usage interne. N’utilisez pas avec **Tester la connexion**.

## Sécurisation du nœud de paramètres d’activité {#securing-the-activity-settings-node}

Vous devez sécuriser le nœud de paramètres d’activité **c:ActivitySettings** sur l’instance de publication de sorte qu’il ne soit pas accessible pour les utilisateurs normaux. Le nœud de paramètres d’activité doit être accessible uniquement au service gérant la synchronisation de l’activité avec Adobe Target.

Le nœud **cq:ActivitySettings** est disponible dans CRXDE Lite sous `/content/campaigns/*nameofbrand*`/*sous le nœud jcr:content des activités,* par exemple, `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Ce nœud est créé après que vous ciblez un composant.

Le nœud **cq:ActivitySettings** sous le nœud jcr:content de l’activité est protégé par les ACL suivantes :

* Refuser tout pour tous
* Autoriser jcr:read,rep:write pour &quot;target-activity-authors&quot; (l’auteur est membre de ce groupe prêt à l’emploi)
* Autoriser jcr:read,rep:write pour &quot;targetservice&quot;

Ces paramètres permettent de garantir que les utilisateurs ordinaires n’ont pas accès aux propriétés de nœud. Utilisez les mêmes ACL sur les instances de création et de publication. Consultez la section [Administration et sécurité des utilisateurs](/help/sites-administering/security.md) pour plus d’informations.

## Configuration de l’externaliseur de liens Day CQ {#configuring-the-aem-link-externalizer}

Lors de la modification d’une activité dans Adobe Target, l’URL pointe sur **localhost**, à moins que vous ne modifiiez l’URL sur le nœud de création AEM. Vous pouvez configurer l’externaliseur de liens d’AEM si vous souhaitez que le contenu exporté pointe vers un domaine *publier*.

>[!NOTE]
>
>Consultez également la section [Ajout de la configuration cloud](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

Pour configurer l’externaliseur AEM, procédez comme suit :

>[!NOTE]
>
>Pour plus d’informations, consultez la section [Externalisation des URL](/help/sites-developing/externalizer.md).

1. Accédez à la console web OSGi : **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Recherchez **Externalisateur de lien Day CQ** et saisissez le domaine du nœud de création.

   ![Day CQ Link Externalizer](assets/aem-externalizer-01.png)
