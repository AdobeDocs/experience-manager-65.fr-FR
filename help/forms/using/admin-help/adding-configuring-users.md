---
title: 'Ajout et configuration d’utilisateurs '
seo-title: 'Ajout et configuration d’utilisateurs '
description: Les paramètres User Management dans la console d’administration vous permettent de créer ou supprimer des utilisateurs et de configurer d’autres paramètres utilisateur.
seo-description: Les paramètres User Management dans la console d’administration vous permettent de créer ou supprimer des utilisateurs et de configurer d’autres paramètres utilisateur.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 73%

---


# Ajout et configuration d’utilisateurs {#adding-and-configuring-users}

Les informations relatives aux utilisateurs et aux groupes sont gérées dans un système de stockage tiers, tel qu’un annuaire LDAP. User Management n’a pas la possibilité d’écrire dans le système de stockage tiers, mais assure la synchronisation de ces informations avec sa propre base de données

## Créer un utilisateur {#create-a-user}

Lorsque vous créez des utilisateurs, vous pouvez les ajouter à des groupes et leur affecter des rôles.

1. In administration console, click **[!UICONTROL Settings > User Management > Users and Groups]**, and click **[!UICONTROL New User]**.
.
1. Under **[!UICONTROL General Settings]**, provide information as required, and then click **[!UICONTROL Next]**. Pour plus d’informations sur ces paramètres, voir [Paramètres utilisateur](adding-configuring-users.md#user-settings).
1. (Optional) To add the user to a group, click **[!UICONTROL Find Groups]**, and do these tasks:

   * In the **[!UICONTROL Find]** box, type all or part of the group name.
   * Select the domain to search, select the number of items to display, and click **[!UICONTROL Find]**.
   * (Optional) To view group details, select the group name, and then click **[!UICONTROL OK]** to return to the search results page.
   * Select the check box for the group and click **[!UICONTROL OK]**.
   * Cliquez sur **[!UICONTROL Suivant]**.

1. (Optional) To assign roles to the user, click **[!UICONTROL Find Roles]**, select the check box for the roles to assign, and then click **[!UICONTROL OK]**.
1. Cliquez sur **[!UICONTROL Terminer]**.

   >[!NOTE]
   >
   >Si vous rencontrez tout problème de connexion avec l’utilisateur, voir [L’utilisateur AEM Forms on JEE ne parvient pas à se connecter à partir d’AEM Forms on OSGi](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Paramètres utilisateur {#user-settings}

Spécifiez les paramètres ci-dessous lorsque vous créez ou modifiez un utilisateur.

**Nom canonique :**(obligatoire) identificateur unique de l’utilisateur. Tous les utilisateurs et groupes d’un domaine doivent disposer d’un nom canonique unique. Cochez la case Généré par le système pour laisser User Management affecter une valeur unique au paramètre Nom canonique ou désélectionnez la case et saisissez une valeur personnalisée.

Avoid using underscore characters (_) in canonical names, for example, `sample_user`. Lorsque vous recherchez des utilisateurs à l’aide de leur nom canonique, les noms contenant des caractères de soulignement n’apparaissent pas dans les résultats.

**Prénom :**(obligatoire) prénom de l’utilisateur.

**Nom :**(obligatoire) nom de l’utilisateur.

**Nom commun :** nom complet ou nom d’affichage de l’utilisateur. Par exemple, si Prénom = Gloria et Nom = Rios, alors Nom commun = Gloria Rios.

**Adresse électronique :** adresse électronique de l’utilisateur.

**Téléphone :** numéro de téléphone de l’utilisateur.

**Description :** description facultative. Utilisez ce champ en fonction des besoins de votre entreprise.

**Adresse :** adresse postale de l’utilisateur.

**Société :** entreprise dont l’utilisateur fait partie.

**Alias de messagerie :** alias de messagerie de l’utilisateur. Séparez les alias de messagerie par des virgules.

**Domaine :** domaine dont l’utilisateur fait partie.

**Paramètres régionaux :** paramètres régionaux ISO de l’utilisateur.

**Clé du calendrier professionnel :** (facultatif) permet d’associer un calendrier professionnel à un utilisateur, en fonction de la valeur de ce paramètre. Les calendriers professionnels définissent les jours ouvrés et non ouvrés. AEM forms peut faire appel à des calendriers professionnels lors du calcul des dates et heures futures associées à des événements, tels que rappels, échéances et transmissions. Les clés de calendrier professionnel sont attribuées à des utilisateurs en fonction du domaine utilisé, tel que le domaine d’entreprise, local ou hybride (voir [Ajout de domaines](/help/forms/using/admin-help/adding-domains.md#adding-domains)).

Si vous utilisez un domaine local ou hybride, les informations relatives aux utilisateurs ne sont stockées que dans la base de données User Management. Pour ces utilisateurs, définissez la clé de calendrier professionnel sur une chaîne. Associez ensuite cette clé (la chaîne) à un calendrier professionnel dans le processus des formulaires.

Si vous utilisez un domaine d’entreprise, les informations relatives aux utilisateurs résident dans un système de stockage tiers, comme un annuaire LDAP. User Management synchronise les informations utilisateur de l’annuaire avec la base de données User Management. Cette fonction vous permet d’associer une clé de calendrier professionnel à un champ de l’annuaire LDAP. Imaginons, par exemple, un scénario où chaque utilisateur enregistré dans votre annuaire dispose d’un champ pays et où vous souhaitez affecter des calendriers professionnels en fonction du pays dans lequel l’utilisateur se trouve. Dans ce cas, vous indiquez le nom du champ pays dans le champ Clé du calendrier professionnel. Vous pouvez ensuite associer les clés de calendrier professionnel (valeurs définies pour le champ « pays » dans l’annuaire LDAP) aux calendriers professionnels dans le processus des formulaires.

Pour plus d’informations sur les calendriers professionnels, notamment sur la manière d’associer des clés de calendrier professionnel à des calendriers professionnels, voir [Configuration des calendriers professionnels](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limitez la longueur du nom à moins de 53 caractères. Un nom court contribue à réduire les problèmes d’affichage de la clé de calendrier professionnel dans les pages Process Management de Administration Console.

**ID utilisateur :**(obligatoire) ID que l’utilisateur utilise pour se connecter. L’ID utilisateur n’est pas sensible à la casse et doit être unique pour tout le domaine.

Dans les domaines d’entreprise, utilisez un attribut non ND comme ID utilisateur, car le ND d’un utilisateur peut changer si l’utilisateur évolue au sein de l’entreprise. Ce paramètre dépend du serveur d’annuaire. The value is `objectGUID` for Active Directory 2003, `nsuniqueID` for Sun™ One, and `guid` for eDirectory.

Assurez-vous que l’ID utilisateur est unique. N’utilisez pas un ID qui était affecté à un utilisateur supprimé.

AEM forms ne peut pas différencier les comptes utilisateur qui possèdent des ID utilisateur et des mots de passe identiques mais qui appartiennent à des domaines différents. Pour éviter ce problème, ne créez pas de compte portant le même ID utilisateur dans plusieurs domaines.

Si vous utilisez une base de données SQL Server, vous ne pouvez pas créer d’ID utilisateur contenant plus de 255 caractères.

Avec MySQL, l’ID utilisateur peut contenir des caractères étendus. Cependant, en cas de comparaison entre deux chaînes telles que abcde et âbcdè, aucune distinction n’est faite entre les deux. Par exemple, lors d’une synchronisation après l’ajout d’un nouvel utilisateur à la base de données, une comparaison est effectuée pour vérifier si cet ID utilisateur existe dans la base de données. Si la base de données contient déjà l’utilisateur *abcde* lorsque vous ajoutez le nouvel utilisateur *âbcdè*, la comparaison ne différencie pas ces deux noms. Le système suppose que l’utilisateur existe déjà dans la base de données et ne procède donc pas à l’ajout de ce dernier.

Evitez de créer des noms d’utilisateur commençant par un dièse (#). Les recherches de tâches ne renvoient aucun résultat pour ces noms d’utilisateur (voir [Utilisation de tâches](/help/forms/using/admin-help/tasks.md#working-with-tasks)).

**Mot de passe et Confirmer le mot de passe :** mot de passe que l’utilisateur utilise pour se connecter. Il doit comporter huit caractères au minimum. Aucun mot de passe n’est exigé si l’utilisateur fait partie d’un domaine hybride.

## Affichage des détails d’un utilisateur {#view-details-about-a-user}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Indiquez les informations permettant d’affiner la recherche, puis, dans la liste Dans, sélectionnez Utilisateurs et cliquez sur Rechercher. Les résultats de recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur les en-têtes de colonne.
1. Cliquez sur le nom de l’utilisateur dont vous souhaitez afficher les détails. La page Modifier l’utilisateur affiche les informations détaillées indiquées relatives à l’utilisateur :

   * informations d’identification d’ordre général, telles que nom, adresse électronique, adresse, domaine et société ;
   * rôles qui lui sont affectés ;
   * groupes dont il est membre.

## Modification du mot de passe d’un utilisateur local {#change-the-password-for-a-local-user}

1. In administration console, click **[!UICONTROL Settings > User Management > Users and Groups]**.
1. Specify information to narrow the search for a particular user and click **[!UICONTROL Find]**. Les résultats de recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur les en-têtes de colonne.
1. Click the name of the user and then click **[!UICONTROL Change Password]**.
1. Type and confirm the new password, and then click **[!UICONTROL OK]**. Le mot de passe doit contenir au moins huit caractères.

## Modification des propriétés d’un utilisateur {#edit-a-user-s-properties}

1. In administration console, click **[!UICONTROL Settings > User Management > Users and Groups]**.
1. Pour rechercher l’utilisateur à modifier, procédez comme suit :

   * In the **[!UICONTROL Find]** box, type your search criteria.
   * In the **[!UICONTROL Using]** list, select **[!UICONTROL Name]**, **[!UICONTROL Email]**, or **[!UICONTROL User ID]**.
   * In the **[!UICONTROL In list]**, select **[!UICONTROL Users]**.
   * Select the domain, select the number of items to display, and then click **[!UICONTROL Find]**.

1. Cliquez sur l’utilisateur à modifier.
1. For a user who is part of a local or hybrid domain, on the **[!UICONTROL Detail]** tab, edit the **[!UICONTROL General Settings]** and **[!UICONTROL Login Settings]**, and click **[!UICONTROL Save]**. Pour plus d’informations sur ces paramètres, voir [Paramètres utilisateur](adding-configuring-users.md#user-settings). Vous n’avez pas la possibilité de modifier les paramètres généraux ni les paramètres de connexion d’un utilisateur appartenant à un domaine d’entreprise.
1. To edit the group settings for the user, click the **[!UICONTROL Group Membership]** tab and do these tasks:

   * Click **[!UICONTROL Find Group]** and complete the search information.
   * To add the user to a new group, select the check box for the group, click **[!UICONTROL OK]**, and then click **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >il n’est pas possible d’ajouter des utilisateurs locaux à des groupes d’annuaires. Néanmoins, il est possible d’ajouter des utilisateurs d’annuaire à des groupes locaux.

   * To remove the user from a group, select the check box for the group, click **[!UICONTROL Delete]**, and then click **[!UICONTROL Save]**.


1. To edit the user’s roles, click the **[!UICONTROL Role Assignments]** tab and do these tasks:

   * To display a list of roles, click **[!UICONTROL Find Roles]**.
   * To add a role, select the check box for the role, click **[!UICONTROL OK]**, and then click **[!UICONTROL Save]**.
   * To remove a role, select the check box for the role, click **[!UICONTROL Unassign]**, and then click **[!UICONTROL Save]**.

## Suppression d’un utilisateur {#delete-a-user}

1. In administration console, click **[!UICONTROL Settings > User Management > Users and Groups]**.
1. Pour rechercher l’utilisateur à supprimer, procédez comme suit :

   * In the **[!UICONTROL Find]** box, type your search criteria.
   * In the **[!UICONTROL Using]** list, select **[!UICONTROL Name]**, **[!UICONTROL Email]**, or **[!UICONTROL User ID]**.
   * In the **[!UICONTROL In list]**, select **[!UICONTROL Users]**.
   * Select the domain, select the number of items to display, and then click **[!UICONTROL Find]**.

1. Select the check box for the user, click **[!UICONTROL Delete]**, and then click **[!UICONTROL OK]**.

>[!NOTE]
>
>AEM Forms sur JEE permet également aux utilisateurs du module complémentaire AEM Forms exécuté dans un environnement OSGi d’être reconnus en tant qu’utilisateurs AEM. Ceci est nécessaire dans les cas où une authentification unique entre AEM Forms sur JEE et le module complémentaire AEM Forms exécuté dans un environnement OSGi est requise (dans le cas de l’espace de travail HTML par exemple). L’opération de suppression mentionnée ci-dessus supprime un utilisateur d’AEM Forms sur JEE uniquement . L’utilisateur n’est pas supprimé du module complémentaire AEM Forms exécuté dans un environnement OSGi. Toutefois, toute tentative de connexion effectuée après la suppression de l’utilisateur (une tentative de connexion au module complémentaire AEM Forms sur un serveur JEE ou au module complémentaire AEM Forms dans un environnement OSGi) est refusée.

## Création d’un gestionnaire d’erreur de connexion personnalisé {#create-custom-login-error-handler}

Si un utilisateur ne disposant pas des autorisations AEM forms et CQ requises tente de se connecter aux applications AEM forms suivantes intégrées à CQ, il est redirigé vers la page CQ 404, indiquant le suivi de l’erreur :

* Solution Correspondence Management
* AEM forms Workspace

   ***Remarque ** : Flex Workspace est obsolète pour la version d’AEM Forms.*

* Gestionnaire des formulaires
* Rapports de workflow 

CQ fournit un mécanisme de remplacement du gestionnaire jsp 404 par défaut.

Pour plus d’informations sur la personnalisation de la page de gestion des erreurs, voir [Personnalisation des pages affichées par le gestionnaire d’erreur](https://docs.adobe.com/docs/en/cq/current/developing/customizing_error_handler_pages.html) dans la documentation d’Adobe Experience Manager.
