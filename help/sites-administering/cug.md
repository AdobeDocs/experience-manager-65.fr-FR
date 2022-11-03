---
title: Création d’un groupe d’utilisateurs fermé
seo-title: Creating a Closed User Group
description: Découvrez comment créer un groupe d’utilisateurs fermé.
seo-description: Learn how to create a Closed User Group.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: 64d174cc824c8bf200cece4e29f60f946ee5560e
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 66%

---

# Création d’un groupe d’utilisateurs fermé{#creating-a-closed-user-group}

Les groupes d’utilisateurs fermés permettent de restreindre l’accès à des pages spécifiques qui se trouvent sur un site Internet publié. Ces pages impliquent que les membres concernés se connectent et fournissent des informations d’identification de sécurité.

Pour configurer une zone de ce type dans votre site web, procédez comme suit :

* [Créez un groupe d’utilisateurs fermé réel et affectez-y des membres.](#creating-the-user-group-to-be-used)

* [Appliquez ce groupe aux pages concernées](#applying-your-closed-user-group-to-content-pages) et sélectionnez (ou créez) la page de connexion à utiliser par les membres du groupe d’utilisateurs fermé. Cela est spécifié également lors de l’application d’un groupe d’utilisateur fermé à une page de contenu.

* [Créez un lien, quelle qu’en soit la forme, vers au moins une page dans la zone protégée](#linking-to-the-cug-pages). Autrement, elle sera invisible.

* [Configurez Dispatcher](#configure-dispatcher-for-cugs) s’il est utilisé.

>[!CAUTION]
>
>Les groupes d’utilisateurs fermés doivent toujours être créés en pensant aux performances.
>
>Même si le nombre d’utilisateurs et de groupes dans un groupe d’utilisateurs fermé n’est pas limité, un nombre élevé de groupes d’utilisateurs fermés dans une page risque de ralentir les performances de rendu.
>
>L’impact des groupes d’utilisateurs fermés doit toujours être pris en compte lorsque vous effectuez des tests de performances.

## Création du groupe d’utilisateurs à utiliser {#creating-the-user-group-to-be-used}

Pour créer un groupe d’utilisateurs fermé :

1. Accédez à **Outils - Sécurité** depuis l’écran d’accueil d’AEM.

   >[!NOTE]
   >
   >Pour plus d’informations sur la création et la configuration des utilisateurs et des groupes, voir [Gestion des utilisateurs et des groupes](/help/sites-administering/security.md#managing-users-and-groups).

1. Sélectionnez la carte **Groupes** dans l’écran suivant.

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Appuyez sur le bouton **Créer** dans le coin supérieur droit pour créer un groupe.
1. Nommez votre groupe, par exemple `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Accédez à l’onglet **Membres** et affectez les utilisateurs requis à ce groupe.

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Activez les utilisateurs affectés à votre groupe d’utilisateurs fermé, en l’occurrence, le groupe `cug_access`.
1. Activez le groupe d’utilisateurs fermé de sorte qu’il soit disponible dans l’environnement de publication. Dans cet exemple, `cug_access`.

## Application de votre groupe d’utilisateurs fermé à des pages de contenu {#applying-your-closed-user-group-to-content-pages}

Pour appliquer le groupe d’utilisateurs fermé à une ou plusieurs pages :

1. Accédez à la page principale de la section restreinte que vous souhaitez affecter à votre groupe d’utilisateurs fermé.
1. Sélectionnez la page en cliquant sur sa miniature, puis en sélectionnant **Propriétés** dans la barre d’outils supérieure.

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. Dans la fenêtre suivante, ouvrez le **Avancé** .

1. Faites défiler l’écran vers le bas jusqu’à **Exigence d’authentification** .

   1. Activez la variable **Activer** coche.

   1. Ajoutez le chemin d’accès à votre **Page de connexion**.
Cette option est facultative. Si rien n’est indiqué, la page de connexion standard est utilisée.

   ![CUG ajouté](assets/cug-authentication-requirement.png)

1. Ensuite, accédez au **Autorisations** et sélectionnez **Modifier le groupe d’utilisateurs fermé**.

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >Les groupes d’utilisateurs fermés dans l’onglet Autorisations ne peuvent pas être déployés sur des Live Copies à partir de plans directeurs. Veuillez en tenir compte lors de la configuration de Live Copy.
   >
   >Pour plus d’informations, consultez [cette page](closed-user-groups.md#aem-livecopy).

1. Le **Modifier le groupe d’utilisateurs fermé** s’ouvre. Ici, vous pouvez rechercher et sélectionner votre groupe d’utilisateurs fermé, puis confirmer la sélection avec **Enregistrer**.

   Le groupe sera ajouté à la liste ; par exemple, le groupe **cug_access**.

   ![CUG ajouté](assets/cug-added.png)

1. Confirmez les modifications avec **Enregistrer et fermer**.

>[!NOTE]
>
>Pour plus d’informations sur les profils dans l’environnement de publication et pour proposer des formulaires de connexion et de déconnexion, voir [Gestion de l’identification](/help/sites-administering/identity-management.md).

## Liaison aux pages de CUG {#linking-to-the-cug-pages}

La cible des liens vers les pages des CUG n’étant pas visible par l’utilisateur anonyme, le vérificateur de liens supprime ces liens.

Pour éviter cela, il est conseillé de créer des pages de redirection non protégées qui pointent vers des pages dans la zone CUG. Les entrées de navigation sont alors rendues sans causer de problème au niveau du vérificateur de lien. Ce n’est qu’en accédant réellement à la page de redirection que l’utilisateur sera redirigé dans la zone CUG, après avoir fourni ses informations de connexion.

## Configuration de Dispatcher pour le groupe d’utilisateurs fermé {#configure-dispatcher-for-cugs}

Si vous utilisez Dispatcher, vous devez définir une ferme de serveurs Dispatcher avec les propriétés suivantes :

* [virtualhosts](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#identifying-virtual-hosts-virtualhosts) : correspond au chemin d’accès aux pages concernées par le groupe d’utilisateurs fermé.
* \sessionmanagement : voir ci-dessous.
* [cache](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache) : répertoire de cache dédié aux fichiers concernés par le groupe d’utilisateurs fermé.

### Configuration de la gestion des sessions Dispatcher pour les groupes d’utilisateurs fermés {#configuring-dispatcher-session-management-for-cugs}

Configurez la [gestion des sessions dans le fichier dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) pour le groupe d’utilisateurs fermé. Le gestionnaire d’authentification utilisé lorsque l’accès est demandé pour les pages des groupes d’utilisateurs fermés détermine comment configurer la gestion des sessions.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Lorsque la gestion des sessions est activée pour une ferme de serveurs de Dispatcher, toutes les pages gérées par la ferme de serveurs ne sont pas mises en cache. Pour mettre en cache les pages qui ne sont pas des groupes d’utilisateurs fermés, créez une seconde ferme de serveurs dans dispatcher.any.
>qui gère les pages non CUG.

1. Configurez [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) en définissant `/directory`, par exemple :

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Définissez [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#caching-when-authentication-is-used) sur `0`.
