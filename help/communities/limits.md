---
title: Limites des contributions des membres
seo-title: Limites des contributions des membres
description: La fonction Limites de contribution permet de limiter les contributions à protéger contre les spams
seo-description: La fonction Limites de contribution permet de limiter les contributions à protéger contre les spams
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Administrator
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# Limites des contributions des membres {#member-contribution-limits}

## Présentation {#overview}

La fonctionnalité Limites de contribution permet de limiter les contributions des membres de la communauté en tant que moyen de protection contre le spam.

Lorsqu’un membre est limité, toute publication qui dépasse le nombre autorisé de contributions déclenche une alerte indiquant que la limite a été dépassée et que la publication est rejetée. Le membre de la communauté peut alors se rendre au centre de messagerie de la communauté et contacter un responsable de la communauté qui peut supprimer les limites, le cas échéant.

Les limites de contribution peuvent être activées individuellement à partir de la [console Membres](members.md) et/ou configurées pour être activées automatiquement lorsque les visiteurs du site deviennent de nouveaux membres.

À l’aide de la console Membres, les limites de contribution peuvent être supprimées de manière proactive pour un membre par un responsable de la communauté à tout moment, ou supprimées de manière réactive lorsqu’un membre envoie un message à un responsable de la communauté qui effectue une telle requête.

## Configuration des limites de contribution du contenu généré par les utilisateurs d’AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Cette configuration OSGi :

* Définit les caractéristiques des limites de contribution (nombre de publications au cours d’une période).
* Identifie qui le membre pourra envoyer un message lorsque la limite a été atteinte.
* Identifie les domaines qui n’ont jamais besoin d’être limités.

Pour atteindre cette configuration OSGi :

* Sur le Principal éditeur :
* Connectez-vous avec les privilèges d’administrateur.
* Accédez à la [console web](../../help/sites-deploying/configuring-osgi.md).

   * Par exemple, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Recherchez `AEM Communities User Generated Content Contribution Limits Configuration`.
* Sélectionnez l’icône de modification.

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL Application automatique des limites de contribution du contenu généré par l’utilisateur]**

   Si cette case est cochée, définissez automatiquement des limites de contribution pour les utilisateurs lorsqu’ils s’enregistrent en tant que membres de la communauté. Cela se reflète dans le profil du membre de la communauté et peut être activé/désactivé à partir de la [console membres](members.md). Les nouveaux membres disposant d’une adresse électronique provenant d’une liste autorisée de domaines ne sont jamais contraints.

   Cette option n’est pas cochée par défaut.

* **[!UICONTROL Limite UGC]**

   Nombre maximum de contributions.

   La valeur par défaut est de 10 publications.

* **[!UICONTROL Fréquence des limites UGC]**

   La période limitant la limite du contenu généré par l’utilisateur.

   La valeur par défaut est de 60 minutes.

* **[!UICONTROL Domaines]**

   Liste de liste autorisée d’un ou de plusieurs domaines de messagerie. Sélectionnez l’icône + pour effectuer d’autres entrées.

   Les utilisateurs dont les adresses électroniques se trouvent dans la liste autorisée des domaines ne sont pas affectés lorsque les limites de contribution du contenu généré par l’utilisateur sont automatiquement appliquées. Par exemple, si le domaine `mycompany.com` est ajouté à la liste des domaines, un membre avec l’adresse électronique `me@mycompany.com` n’est jamais restreint à la publication.

   La liste autorisée par défaut est vide.

* **[!UICONTROL Destinataires de la messagerie]**

   Liste d’un ou plusieurs ID autorisables des membres pouvant modifier les limites de contribution des membres. Sélectionnez l’icône + pour effectuer d’autres entrées.

   Les membres ne peuvent atteindre que les membres spécifiés lorsque leur limite a été atteinte.

   La valeur par défaut n’est pas un destinataire de messagerie.

Remarque : La configuration par défaut génère une limite de 10 publications sur une période d’une heure.
