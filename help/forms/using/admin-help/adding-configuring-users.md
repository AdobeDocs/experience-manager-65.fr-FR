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

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > User Management > Utilisateurs et groupes]**, puis sur **[!UICONTROL Nouvel utilisateur]**.
.
1. Sous **[!UICONTROL Paramètres généraux]**, fournissez les informations requises, puis cliquez sur **[!UICONTROL Suivant]**. Pour plus d’informations sur ces paramètres, voir [Paramètres utilisateur](adding-configuring-users.md#user-settings).
1. (Facultatif) Pour ajouter l’utilisateur à un groupe, cliquez sur **[!UICONTROL Rechercher des groupes]**, puis effectuez les tâches suivantes :

   * Dans la zone **[!UICONTROL Rechercher]**, entrez tout ou partie du nom du groupe.
   * Sélectionnez le domaine à rechercher, le nombre d’éléments à afficher, puis cliquez sur **[!UICONTROL Rechercher]**.
   * (Facultatif) Pour vue les détails du groupe, sélectionnez le nom du groupe, puis cliquez sur **[!UICONTROL OK]** pour revenir à la page des résultats de la recherche.
   * Cochez la case du groupe et cliquez sur **[!UICONTROL OK]**.
   * Cliquez sur **[!UICONTROL Next]** (Suivant).

1. (Facultatif) Pour attribuer des rôles à l’utilisateur, cliquez sur **[!UICONTROL Rechercher des rôles]**, cochez la case correspondant aux rôles à affecter, puis cliquez sur **[!UICONTROL OK]**.
1. Cliquez sur **[!UICONTROL Finish]** (Terminer). 

   >[!NOTE]
   >
   >Si vous rencontrez tout problème de connexion avec l’utilisateur, voir [L’utilisateur AEM Forms on JEE ne parvient pas à se connecter à partir d’AEM Forms on OSGi](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Paramètres utilisateur {#user-settings}

Spécifiez les paramètres ci-dessous lorsque vous créez ou modifiez un utilisateur.

**Nom canonique :**(obligatoire) identificateur unique de l’utilisateur. Tous les utilisateurs et groupes d’un domaine doivent disposer d’un nom canonique unique. Cochez la case Généré par le système pour laisser User Management affecter une valeur unique au paramètre Nom canonique ou désélectionnez la case et saisissez une valeur personnalisée.

Evitez d’utiliser des caractères de soulignement (_) dans les noms canoniques, par exemple `sample_user`. Lorsque vous recherchez des utilisateurs à l’aide de leur nom canonique, les noms contenant des caractères de soulignement n’apparaissent pas dans les résultats.

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

Dans les domaines d’entreprise, utilisez un attribut non ND comme ID utilisateur, car le ND d’un utilisateur peut changer si l’utilisateur évolue au sein de l’entreprise. Ce paramètre dépend du serveur d’annuaire. La valeur est `objectGUID` pour Principale Directory 2003, `nsuniqueID` pour Sun™ One et `guid` pour eDirectory.

Assurez-vous que l’ID utilisateur est unique. N’utilisez pas un ID qui était affecté à un utilisateur supprimé.

AEM forms ne peut pas différencier les comptes utilisateur qui possèdent des ID utilisateur et des mots de passe identiques mais qui appartiennent à des domaines différents. Pour éviter ce problème, ne créez pas de compte portant le même ID utilisateur dans plusieurs domaines.

Si vous utilisez une base de données SQL Server, vous ne pouvez pas créer d’ID utilisateur contenant plus de 255 caractères.

Avec MySQL, l’ID utilisateur peut contenir des caractères étendus. Cependant, en cas de comparaison entre deux chaînes telles que abcde et âbcdè, aucune distinction n’est faite entre les deux. Par exemple, lors d’une synchronisation après l’ajout d’un nouvel utilisateur à la base de données, une comparaison est effectuée pour vérifier si cet ID utilisateur existe dans la base de données. Si la base de données contient déjà l’utilisateur *abcde* lorsque vous ajoutez le nouvel utilisateur *âbcdè*, la comparaison ne différencie pas ces deux noms. Le système suppose que l’utilisateur existe déjà dans la base de données et ne procède donc pas à l’ajout de ce dernier.

Evitez de créer des noms d’utilisateur commençant par un dièse (#). Les recherches de tâches ne renvoient aucun résultat pour ces noms d’utilisateur (voir [Utilisation de tâches](/help/forms/using/admin-help/tasks.md#working-with-tasks)).

**Mot de passe et Confirmer le mot de passe :** mot de passe que l’utilisateur utilise pour se connecter. Il doit comporter huit caractères au minimum. Aucun mot de passe n’est exigé si l’utilisateur fait partie d’un domaine hybride.

## Affichage des détails d’un utilisateur  {#view-details-about-a-user}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Indiquez les informations permettant d’affiner la recherche, puis, dans la liste Dans, sélectionnez Utilisateurs et cliquez sur Rechercher. Les résultats de recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur les en-têtes de colonne.
1. Cliquez sur le nom de l’utilisateur dont vous souhaitez afficher les détails. La page Modifier l’utilisateur affiche les informations détaillées indiquées relatives à l’utilisateur :

   * informations d’identification d’ordre général, telles que nom, adresse électronique, adresse, domaine et société ;
   * rôles qui lui sont affectés ;
   * groupes dont il est membre.

## Modification du mot de passe d’un utilisateur local  {#change-the-password-for-a-local-user}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > User Management > Utilisateurs et groupes]**.
1. Spécifiez les informations permettant de restreindre la recherche d’un utilisateur particulier et cliquez sur **[!UICONTROL Rechercher]**. Les résultats de recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur les en-têtes de colonne.
1. Cliquez sur le nom de l’utilisateur, puis sur **[!UICONTROL Changer de mot de passe]**.
1. Saisissez et confirmez le nouveau mot de passe, puis cliquez sur **[!UICONTROL OK]**. Le mot de passe doit contenir au moins huit caractères.

## Modification des propriétés d’un utilisateur  {#edit-a-user-s-properties}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > User Management > Utilisateurs et groupes]**.
1. Pour rechercher l’utilisateur à modifier, procédez comme suit :

   * Dans la zone **[!UICONTROL Rechercher]**, entrez vos critères de recherche.
   * Dans la liste **[!UICONTROL Utilisation]**, sélectionnez **[!UICONTROL Nom]**, **[!UICONTROL Courriel]** ou **[!UICONTROL ID utilisateur]**.
   * Dans la **[!UICONTROL liste]**, sélectionnez **[!UICONTROL Utilisateurs]**.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur **[!UICONTROL Rechercher]**.

1. Cliquez sur l’utilisateur à modifier.
1. Pour un utilisateur faisant partie d’un domaine local ou hybride, dans l’onglet **[!UICONTROL Détails]**, modifiez les **[!UICONTROL Paramètres généraux]** et **[!UICONTROL Paramètres de connexion]**, puis cliquez sur **[!UICONTROL Enregistrer]**. Pour plus d’informations sur ces paramètres, voir [Paramètres utilisateur](adding-configuring-users.md#user-settings). Vous n’avez pas la possibilité de modifier les paramètres généraux ni les paramètres de connexion d’un utilisateur appartenant à un domaine d’entreprise.
1. Pour modifier les paramètres de groupe de l’utilisateur, cliquez sur l’onglet **[!UICONTROL Appartenance au groupe]** et procédez comme suit :

   * Cliquez sur **[!UICONTROL Rechercher un groupe]** et complétez les informations de recherche.
   * Pour ajouter l’utilisateur à un nouveau groupe, cochez la case correspondant au groupe, cliquez sur **[!UICONTROL OK]**, puis sur **[!UICONTROL Enregistrer]**.

   >[!NOTE]
   >
   >il n’est pas possible d’ajouter des utilisateurs locaux à des groupes d’annuaires. Néanmoins, il est possible d’ajouter des utilisateurs d’annuaire à des groupes locaux.

   * Pour supprimer l’utilisateur d’un groupe, activez la case à cocher correspondant au groupe, cliquez sur **[!UICONTROL Supprimer]**, puis sur **[!UICONTROL Enregistrer]**.


1. Pour modifier les rôles de l’utilisateur, cliquez sur l’onglet **[!UICONTROL Affectations de rôles]** et procédez comme suit :

   * Pour afficher une liste de rôles, cliquez sur **[!UICONTROL Rechercher des rôles]**.
   * Pour ajouter un rôle, cochez la case correspondant au rôle, cliquez sur **[!UICONTROL OK]**, puis sur **[!UICONTROL Enregistrer]**.
   * Pour supprimer un rôle, activez la case à cocher correspondante, cliquez sur **[!UICONTROL Annuler l&#39;affectation]**, puis sur **[!UICONTROL Enregistrer]**.

## Suppression d’un utilisateur {#delete-a-user}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > User Management > Utilisateurs et groupes]**.
1. Pour rechercher l’utilisateur à supprimer, procédez comme suit :

   * Dans la zone **[!UICONTROL Rechercher]**, entrez vos critères de recherche.
   * Dans la liste **[!UICONTROL Utilisation]**, sélectionnez **[!UICONTROL Nom]**, **[!UICONTROL Courriel]** ou **[!UICONTROL ID utilisateur]**.
   * Dans la **[!UICONTROL liste]**, sélectionnez **[!UICONTROL Utilisateurs]**.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur **[!UICONTROL Rechercher]**.

1. Cochez la case correspondant à l’utilisateur, cliquez sur **[!UICONTROL Supprimer]**, puis sur **[!UICONTROL OK]**.

>[!NOTE]
>
>AEM Forms sur JEE permet également aux utilisateurs du module complémentaire AEM Forms exécuté dans un environnement OSGi d’être reconnus en tant qu’utilisateurs AEM. Ceci est nécessaire dans les cas où une authentification unique entre AEM Forms sur JEE et le module complémentaire AEM Forms exécuté dans un environnement OSGi est requise (dans le cas de l’espace de travail HTML par exemple). L’opération de suppression mentionnée ci-dessus supprime un utilisateur d’AEM Forms sur JEE uniquement . L’utilisateur n’est pas supprimé du module complémentaire AEM Forms exécuté dans un environnement OSGi. Toutefois, toute tentative de connexion effectuée après la suppression de l’utilisateur (une tentative de connexion au module complémentaire AEM Forms sur un serveur JEE ou au module complémentaire AEM Forms dans un environnement OSGi) est refusée.

## Création d’un gestionnaire d’erreur de connexion personnalisé  {#create-custom-login-error-handler}

Si un utilisateur ne disposant pas des autorisations AEM forms et CQ requises tente de se connecter aux applications AEM forms suivantes intégrées à CQ, il est redirigé vers la page CQ 404, indiquant le suivi de l’erreur :

* Solution Correspondence Management
* AEM forms Workspace

   ***Remarque ** : Flex Workspace est obsolète pour la version d’AEM Forms.*

* Gestionnaire des formulaires
* Rapports de workflow 

CQ fournit un mécanisme de remplacement du gestionnaire jsp 404 par défaut.

Pour plus d’informations sur la personnalisation de la page de gestion des erreurs, voir [Personnalisation des pages affichées par le gestionnaire d’erreur](https://docs.adobe.com/docs/en/cq/current/developing/customizing_error_handler_pages.html) dans la documentation d’Adobe Experience Manager.
