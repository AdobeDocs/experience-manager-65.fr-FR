---
title: Ajout et configuration d’utilisateurs
seo-title: Adding and configuring users
description: Les paramètres User Management dans la console d’administration vous permettent de créer ou supprimer des utilisateurs et de configurer d’autres paramètres utilisateur.
seo-description: The User Management settings in the administration console allow you to create or delete users  and configure other user settings.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 37%

---

# Ajouter et configurer des utilisateurs {#adding-and-configuring-users}

Les informations sur les utilisateurs et les groupes sont conservées dans un système de stockage tiers, tel qu’un annuaire LDAP. User Management n’écrit pas sur le système de stockage tiers. Au lieu de cela, User Management synchronise les informations sur les utilisateurs et les groupes avec sa propre base de données.

## Création d’un utilisateur {#create-a-user}

Lorsque vous créez des utilisateurs, vous pouvez les ajouter à des groupes et leur attribuer des rôles.

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > Gestion des utilisateurs > Utilisateurs et groupes]**, puis sur **[!UICONTROL Nouvel utilisateur]**.
.
1. Sous **[!UICONTROL Paramètres généraux]**, fournissez les informations requises, puis cliquez sur Suivant. **[!UICONTROL Suivant]**. Pour plus d’informations sur ces paramètres, voir [Paramètres utilisateur](adding-configuring-users.md#user-settings).
1. (Facultatif) Pour ajouter l’utilisateur à un groupe, cliquez sur **[!UICONTROL Rechercher des groupes]** et procédez comme suit :

   * Dans la zone **[!UICONTROL Rechercher]**, saisissez tout ou partie du nom du groupe.
   * Sélectionnez le domaine dans lequel effectuer la recherche, le nombre d’éléments à afficher et cliquez sur **[!UICONTROL Rechercher]**.
   * (Facultatif) Pour afficher les détails d’un groupe, sélectionnez son nom et cliquez sur **[!UICONTROL OK]** pour revenir à la page des résultats de recherche.
   * Cochez la case du groupe, puis cliquez sur **[!UICONTROL OK]**.
   * Cliquez sur **[!UICONTROL Suivant]**.

1. (Facultatif) Pour affecter des rôles à l’utilisateur, cliquez sur **[!UICONTROL Rechercher des rôles]**, cochez les cases en regard des rôles à affecter, puis cliquez sur **[!UICONTROL OK]**.
1. Cliquez sur **[!UICONTROL Finish]** (Terminer). 

   >[!NOTE]
   >
   >Si vous rencontrez un problème de connexion avec l’utilisateur, reportez-vous à la section [L’utilisateur d’AEM Forms on JEE ne parvient pas à se connecter à AEM Forms côté OSGi.](https://helpx.adobe.com/fr/aem-forms/kb/AEM-users-fails-to-login.html).

## Paramètres utilisateur {#user-settings}

Spécifiez les paramètres suivants lorsque vous créez ou modifiez un utilisateur.

**Nom canonique :**(obligatoire) identificateur unique de l’utilisateur. Chaque utilisateur et groupe d’un domaine doit avoir un nom canonique unique. Cochez la case Généré par le système pour laisser User Management attribuer une valeur unique ou décochez la case et spécifiez une valeur personnalisée pour le Nom canonique.

Évitez l’utilisation de caractères de soulignement (_) dans les noms canoniques, par exemple, `sample_user`. Lorsque vous recherchez des utilisateurs à l’aide de leur nom canonique, les noms contenant des caractères de soulignement n’apparaissent pas dans les résultats.

**Prénom :** (obligatoire) prénom de l’utilisateur

**Nom :** (obligatoire) nom de famille de l’utilisateur

**Nom commun :** nom complet ou nom d’affichage de l’utilisateur. Par exemple, si Prénom = Gloria et Nom = Rios, alors Nom commun = Gloria Rios.

**Email :** Adresse électronique de l’utilisateur

**Téléphone :** Numéro de téléphone de l’utilisateur

**Description :** description facultative. Utilisez ce champ en fonction des besoins de votre entreprise.

**Adresse :** Adresse postale de l’utilisateur

**Organisation :** Organisation à laquelle appartient l’utilisateur

**Alias de messagerie :** alias de messagerie de l’utilisateur. Séparez les alias de messagerie par des virgules.

**Domaine :** Domaine auquel appartient l’utilisateur

**Paramètres régionaux :** Paramètre régional ISO de l’utilisateur

**Clé du calendrier professionnel :** (facultatif) permet d’associer un calendrier professionnel à un utilisateur, en fonction de la valeur de ce paramètre. Les calendriers professionnels définissent les jours ouvrés et non ouvrés. AEM les formulaires peuvent utiliser des calendriers professionnels pour calculer les dates et heures futures des événements tels que les rappels, les échéances et les transmissions. La manière dont vous attribuez des clés de calendrier professionnel aux utilisateurs varie selon que vous utilisez un domaine d’entreprise, local ou hybride. (Voir [Ajout de domaines](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Si vous utilisez un domaine local ou hybride, les informations sur les utilisateurs sont stockées uniquement dans la base de données User Management. Pour ces utilisateurs, définissez la clé du calendrier professionnel sur une chaîne. Associez ensuite la clé de calendrier professionnel (la chaîne) à un calendrier professionnel dans le processus des formulaires.

Si vous utilisez un domaine d’entreprise, les informations sur les utilisateurs résident dans un système de stockage tiers, tel qu’un annuaire LDAP. User Management synchronise les informations utilisateur de l’annuaire avec la base de données User Management. Cette fonctionnalité vous permet de mapper une clé de calendrier professionnel à un champ de l’annuaire LDAP. Supposons, par exemple, que chaque utilisateur enregistré dans votre annuaire dispose d’un champ pays et que vous souhaitiez attribuer des calendriers professionnels en fonction du pays où se trouve l’utilisateur. Dans ce cas, vous indiquez le nom du champ de pays comme valeur du paramètre Clé du calendrier professionnel . Vous pouvez ensuite associer les clés de calendrier professionnel (valeurs définies pour le champ pays dans l’annuaire LDAP) aux calendriers professionnels dans le processus des formulaires.

Pour plus d’informations sur les calendriers professionnels, y compris sur la façon de mapper des clés de calendrier professionnel à des calendriers professionnels, voir [Configuration des calendriers professionnels](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limitez le nom à moins de 53 caractères. Un nom court contribue à réduire les problèmes d’affichage de la clé de calendrier professionnel dans les pages Process Management d’Administration Console.

**ID utilisateur :**(obligatoire) ID que l’utilisateur utilise pour se connecter. L’ID utilisateur n’est pas sensible à la casse et doit être unique dans l’ensemble du domaine.

Dans les domaines d’entreprise, utilisez un attribut non ND comme identifiant utilisateur, car le ND d’un utilisateur peut changer s’il se déplace vers une autre partie de l’organisation. Ce paramètre dépend du serveur d’annuaire. La valeur est `objectGUID` pour Active Directory 2003, `nsuniqueID` pour Sun™ One et `guid` pour eDirectory.

Assurez-vous que l’ID utilisateur est unique. N’utilisez pas celui qui a été affecté à un utilisateur supprimé.

AEM formulaires ne peuvent pas différencier les comptes d’utilisateurs qui possèdent des identifiants utilisateur et des mots de passe identiques mais qui appartiennent à des domaines différents. Pour éviter ce problème, ne créez pas de comptes portant le même ID utilisateur sur plusieurs domaines.

Lors de l’utilisation de SQL Server comme base de données, vous ne pouvez pas créer d’ID utilisateur contenant plus de 255 caractères.

Lorsque vous utilisez MySQL, l’ID utilisateur peut contenir des caractères étendus. Cependant, lorsqu’une comparaison est effectuée entre deux chaînes, telles que abcde et âbcdè, elles sont considérées comme identiques. Par exemple, lors de la synchronisation, si un nouvel utilisateur a été ajouté à la base de données, une comparaison est effectuée pour vérifier si un utilisateur portant le même ID utilisateur existe dans la base de données. Si l’utilisateur *abcde* existe dans la base de données lorsque le nouvel utilisateur *âbcdè* est ajouté, la comparaison ne peut pas distinguer les deux noms. On suppose que l’utilisateur existe dans la base de données et que le nouvel utilisateur est ignoré et n’est pas ajouté.

Évitez de créer des noms d’utilisateur commençant par un signe dièse (#). L’exécution de recherches de tâches ne renvoie aucun résultat pour ces noms d’utilisateur. (Voir [Utilisation des tâches](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Mot de passe et Confirmer le mot de passe :** Mot de passe utilisé par l’utilisateur pour se connecter. Il doit comporter au minimum huit caractères. Aucun mot de passe n’est requis pour un utilisateur faisant partie d’un domaine hybride.

## Affichage des détails d’un utilisateur {#view-details-about-a-user}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Indiquez les informations pour affiner la recherche, puis, dans la liste Dans, sélectionnez Utilisateurs et cliquez sur Rechercher. Les résultats de la recherche sont répertoriés au bas de la page. Vous pouvez trier la liste en cliquant sur l’un des en-têtes de colonne.
1. Cliquez sur le nom de l’utilisateur dont vous souhaitez afficher les détails. La page Modifier l’utilisateur affiche les détails suivants sur l’utilisateur :

   * Informations d’identification générales, telles que le nom, l’adresse électronique, l’adresse, le domaine et l’organisation
   * Rôles affectés à l’utilisateur
   * Groupes dont l’utilisateur est membre

## Modification du mot de passe d’un utilisateur local {#change-the-password-for-a-local-user}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > Gestion des utilisateurs > Utilisateurs et groupes]**.
1. Indiquez les informations permettant d’affiner la recherche pour un utilisateur particulier et cliquez sur **[!UICONTROL Rechercher]**. Les résultats de la recherche sont répertoriés au bas de la page. Vous pouvez trier la liste en cliquant sur l’un des en-têtes de colonne.
1. Cliquez sur le nom de l’utilisateur, puis sur **[!UICONTROL Modifier le mot de passe]**.
1. Saisissez et confirmez le nouveau mot de passe puis cliquez sur **[!UICONTROL OK]**. Le mot de passe doit comporter au minimum huit caractères.

## Modification des propriétés d’un utilisateur {#edit-a-user-s-properties}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > Gestion des utilisateurs > Utilisateurs et groupes]**.
1. Pour rechercher l’utilisateur à modifier, procédez comme suit :

   * Dans la zone **[!UICONTROL Rechercher]**, saisissez vos critères de recherche.
   * Dans la liste **[!UICONTROL Utilisation]**, sélectionnez **[!UICONTROL Nom]**, **[!UICONTROL E-mail]** ou **[!UICONTROL ID utilisateur]**.
   * Dans la liste **[!UICONTROL Dans]**, sélectionnez **[!UICONTROL Utilisateurs]**.
   * Sélectionnez le domaine, indiquez le nombre d’éléments à afficher, puis cliquez sur **[!UICONTROL Rechercher]**.

1. Cliquez sur l’utilisateur à modifier.
1. Dans le cas d’un utilisateur appartenant à un domaine local ou hybride, modifiez les **[!UICONTROL paramètres généraux]** et les **[!UICONTROL paramètres de connexion]** dans l’onglet **[!UICONTROL Détails]**, puis cliquez sur **[!UICONTROL Enregistrer]**. Pour plus d’informations sur ces paramètres, voir [Paramètres utilisateur](adding-configuring-users.md#user-settings). Vous ne pouvez pas modifier les paramètres généraux ni les paramètres de connexion d’un utilisateur appartenant à un domaine d’entreprise.
1. Pour modifier les paramètres du groupe de l’utilisateur, cliquez sur l’onglet **[!UICONTROL Membres du groupe]** et procédez comme suit :

   * Cliquez sur **[!UICONTROL Rechercher des groupes]** et renseignez les informations de recherche.
   * Pour ajouter l’utilisateur à un nouveau groupe, cochez la case correspondant au groupe, cliquez sur **[!UICONTROL OK]**, puis sur **[!UICONTROL Enregistrer]**.

   >[!NOTE]
   >
   >Les utilisateurs locaux ne peuvent pas être ajoutés aux groupes d’annuaires. Toutefois, les utilisateurs d’annuaire peuvent être ajoutés aux groupes locaux.

   * Pour supprimer l’utilisateur d’un groupe, activez la case à cocher correspondant au groupe, cliquez sur **[!UICONTROL Supprimer]**, puis sur **[!UICONTROL Enregistrer]**.


1. Pour modifier les rôles de l’utilisateur, cliquez sur le bouton **[!UICONTROL Affectations de rôles]** et procédez comme suit :

   * Pour afficher une liste de rôles, cliquez sur **[!UICONTROL Rechercher des rôles]**.
   * Pour ajouter un nouveau rôle, activez la case à cocher qui lui correspond, cliquez sur **[!UICONTROL OK]**, puis sur **[!UICONTROL Enregistrer]**.
   * Pour supprimer un rôle, activez la case à cocher qui lui correspond, cliquez sur **[!UICONTROL Retirer]**, puis sur **[!UICONTROL Enregistrer]**.

## Suppression d’un utilisateur {#delete-a-user}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > Gestion des utilisateurs > Utilisateurs et groupes]**.
1. Pour rechercher l’utilisateur à supprimer, procédez comme suit :

   * Dans la zone **[!UICONTROL Rechercher]**, saisissez vos critères de recherche.
   * Dans la liste **[!UICONTROL Utilisation]**, sélectionnez **[!UICONTROL Nom]**, **[!UICONTROL E-mail]** ou **[!UICONTROL ID utilisateur]**.
   * Dans la liste **[!UICONTROL Dans]**, sélectionnez **[!UICONTROL Utilisateurs]**.
   * Sélectionnez le domaine, indiquez le nombre d’éléments à afficher, puis cliquez sur **[!UICONTROL Rechercher]**.

1. Cochez la case située en regard de l’utilisateur, cliquez sur **[!UICONTROL Supprimer]**, puis sur **[!UICONTROL OK]**.

>[!NOTE]
>
>AEM Forms on JEE permet également aux utilisateurs du module complémentaire AEM forms s’exécutant sur OSGi d’être reconnus comme AEM utilisateurs. Cela est nécessaire dans les cas où l’authentification unique entre AEM Forms on JEE et le module complémentaire d’AEM forms exécuté sur OSGi est requise (par exemple, l’espace de travail HTML). L’opération de suppression mentionnée ci-dessus supprime un utilisateur d’AEM Forms sur JEE uniquement. L’utilisateur n’est pas supprimé du module complémentaire AEM Forms exécuté dans un environnement OSGi. Cependant, toute tentative de connexion effectuée après la suppression de l’utilisateur (une tentative de connexion au serveur de module complémentaire AEM Forms JEE ou au module complémentaire AEM Forms dans un environnement OSGi) est refusée.

## Créer un gestionnaire d’erreur de connexion personnalisé {#create-custom-login-error-handler}

Si un utilisateur ne disposant pas des autorisations AEM et CQ requises tente de se connecter aux applications suivantes intégrées à CQ, il est redirigé vers la page CQ 404 par défaut contenant la trace de l’erreur :

* Solution Correspondence Management
* Espace de travail des formulaires AEM

   ***Remarque ** : Flex Workspace est obsolète pour la version d’AEM Forms.*

* gestionnaire de formulaires
* Rapports de workflow

CQ fournit un mécanisme pour remplacer le jsp du gestionnaire 404 par défaut.

Pour plus d’informations sur la personnalisation de la page de gestion des erreurs, voir [Personnalisation des pages affichées par le gestionnaire d’erreurs](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=en) dans la documentation Adobe Experience Manager.
