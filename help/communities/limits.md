---
title: Limites de contribution des membres
seo-title: Limites de contribution des membres
description: La fonction Limites de contribution permet de limiter les contributions à protéger contre le spam
seo-description: La fonction Limites de contribution permet de limiter les contributions à protéger contre le spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Limites de contribution des membres {#member-contribution-limits}

## Présentation {#overview}

La fonction des limites de contribution permet de limiter les contributions des membres de la communauté comme moyen de protéger contre le spam.

Lorsqu’un membre est limité, toute publication qui dépasse le nombre autorisé de contributions génère une alerte indiquant que la limite a été dépassée et que la publication est rejetée. Le membre de la communauté peut alors se rendre au centre de messages de la communauté et communiquer avec un gestionnaire de la communauté qui peut supprimer les limites, le cas échéant.

Les limites de contribution peuvent être activées individuellement à partir de la console [](members.md) Membres et/ou configurées pour être automatiquement activées lorsque les visiteurs du site deviennent de nouveaux membres.

À l’aide de la console Membres, les limites de contribution peuvent être supprimées de manière proactive pour un membre par un gestionnaire de communauté à tout moment, ou supprimées de manière réactive lorsqu’un membre envoie un message à un gestionnaire de communauté qui fait une telle demande.

## Configuration des limites de contribution du contenu généré par l’utilisateur des communautés AEM {#aem-communities-user-generated-content-contribution-limits-configuration}

Cette configuration OSGi

* Définit les caractéristiques des limites de contribution (nombre de postes au cours d&#39;une période)
* Identifie le membre qui sera en mesure de transmettre un message lorsque la limite a été atteinte.
* Identifie les domaines qui ne doivent jamais être limités.

Pour atteindre cette configuration OSGi :

* Sur l’éditeur principal
* Connexion avec droits d’administrateur
* Access the [Web Console](../../help/sites-deploying/configuring-osgi.md)

   * For example, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localiser `AEM Communities User Generated Content Contribution Limits Configuration`
* Sélectionner l’icône Modifier

![chlimage_1-127](assets/chlimage_1-127.png)

* **[!UICONTROL Appliquer automatiquement les limites de contribution UGC]**

   Si cette option est cochée, définissez automatiquement des limites de contribution pour les utilisateurs lorsqu’ils s’inscrivent en tant que membres de la communauté. Cela se reflète dans le profil du membre de la communauté et peut être activé/désactivé depuis la console [des membres](members.md). Les nouveaux membres dotés d’une adresse électronique provenant d’un domaine de liste blanche ne sont jamais limités.

   Cette option n’est pas cochée par défaut.

* **[!UICONTROL Limite UGC]**

   Nombre maximal de contributions.

   La valeur par défaut est de 10 publications.

* **[!UICONTROL Fréquence limite UGC]**

   Période limitant la limite UGC.

   La valeur par défaut est de 60 minutes.

* **[!UICONTROL Domaines]**

   Liste blanche d’un ou de plusieurs domaines de courriel. Sélectionnez l’icône + pour ajouter des entrées.

   Les utilisateurs dont les adresses électroniques se trouvent dans les domaines de liste blanche ne sont pas affectés lorsque les limites de contribution UGC sont appliquées automatiquement. Par exemple, si domaine `mycompany.com` est ajouté à la liste des domaines, un membre avec une adresse électronique `me@mycompany.com` n’est jamais limité à la publication.

   La valeur par défaut est une liste blanche vide.

* **[!UICONTROL Destinataires de la messagerie]**

   Liste d&#39;un ou de plusieurs ID autorisés des membres pouvant modifier les limites de contribution des membres. Sélectionnez l’icône + pour ajouter des entrées.

   Les membres ne peuvent communiquer avec des membres spécifiés que lorsque leur limite a été atteinte.

   La valeur par défaut n’est pas un destinataire de messagerie.

Remarque : La configuration par défaut génère une limite de 10 publications sur une période d’une heure.
