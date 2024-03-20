---
title: Ajouter et configurer des utilisateurs et des utilisatrices
description: Les paramètres User Management dans la console d’administration vous permettent de créer ou supprimer des utilisateurs ou des utilisatrices et de configurer d’autres paramètres utilisateur.
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 100%

---

# Ajouter et configurer des utilisateurs {#adding-and-configuring-users}

Les informations relatives aux utilisateurs, utilisatrices et aux groupes sont gérées dans un système de stockage tiers, tel qu’un annuaire LDAP. User Management n’a pas la possibilité d’écrire dans le système de stockage tiers, mais assure la synchronisation de ces informations avec sa propre base de données

## Créer un utilisateur {#create-a-user}

Lorsque vous créez des utilisateurs pu des utilisatrices, vous pouvez les ajouter à des groupes et leur affecter des rôles.

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
   >Si vous rencontrez tout problème de connexion avec l’utilisateur ou l’utilisatrice, consultez [L’utilisateur AEM Forms on JEE ne parvient pas à se connecter à partir d’AEM Forms on OSGi](https://helpx.adobe.com/fr/aem-forms/kb/AEM-users-fails-to-login.html).

## Paramètres utilisateur {#user-settings}

Spécifiez les paramètres ci-dessous lorsque vous créez ou modifiez un utilisateur ou une utilisatrice.

**Nom canonique :**(obligatoire) identificateur unique de l’utilisateur. Tous les utilisateurs, utilisatrices et groupes d’un domaine doivent disposer d’un nom canonique unique. Cochez la case Généré par le système pour laisser User Management affecter une valeur unique au paramètre Nom canonique ou désélectionnez la case et saisissez une valeur personnalisée.

Évitez l’utilisation de caractères de soulignement (_) dans les noms canoniques, par exemple, `sample_user`. Lorsque vous recherchez des utilisateurs à l’aide de leur nom canonique, les noms contenant des caractères de soulignement n’apparaissent pas dans les résultats.

**Prénom :**(obligatoire) prénom de l’utilisateur ou de l’utilisatrice.

**Nom :**(obligatoire) nom de l’utilisateur ou de l’utilisatrice.

**Nom commun :** nom complet ou nom d’affichage de l’utilisateur. Par exemple, si Prénom = Gloria et Nom = Rios, alors Nom commun = Gloria Rios.

**Adresse électronique :** adresse électronique de l’utilisateur ou de l’utilisatrice.

**Téléphone :** numéro de téléphone de l’utilisateur ou de l’utilisatrice.

**Description :** description facultative. Utilisez ce champ en fonction des besoins de votre entreprise.

**Adresse :** adresse postale de l’utilisateur ou de l’utilisatrice.

**Organisation :** organisation à laquelle appartient l’utilisateur ou l’utilisatrice.

**Alias de messagerie :** alias de messagerie de l’utilisateur ou de l’utilisatrice. Séparez les alias de messagerie par des virgules.

**Domaine :** domaine dont l’utilisateur ou l’utilisatrice fait partie.

**Paramètres régionaux :** paramètres régionaux ISO de l’utilisateur ou de l’utilisatrice.

**Clé du calendrier professionnel :** (facultatif) permet d’associer un calendrier professionnel à un utilisateur, en fonction de la valeur de ce paramètre. Les calendriers professionnels définissent les jours ouvrés et non ouvrés. AEM forms peut faire appel à des calendriers professionnels lors du calcul des dates et heures futures associées à des événements, tels que rappels, échéances et transmissions. Les clés de calendrier professionnel sont attribuées à des utilisateurs et des utilisatrices en fonction du domaine utilisé, tel que le domaine d’entreprise, local ou hybride. (Voir [Ajout de domaines](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Si vous utilisez un domaine local ou hybride, les informations relatives aux utilisateurs et utilisatrices ne sont stockées que dans la base de données User Management. Pour ces utilisateurs et utilisatrices, définissez la clé de calendrier professionnel sur une chaîne. Associez ensuite la clé de calendrier professionnel (la chaîne) à un calendrier professionnel dans Forms Workflow.

Si vous utilisez un domaine d’entreprise, les informations sur les utilisateurs et utilisatrices résident dans un système de stockage tiers, tel qu’un annuaire LDAP. User Management synchronise les informations utilisateur de l’annuaire avec la base de données User Management. Cette fonctionnalité vous permet d’associer une clé de calendrier professionnel à un champ de l’annuaire LDAP. Imaginons, par exemple, un scénario où chaque utilisateur ou utilisatrice enregistré(e) dans votre annuaire dispose d’un champ pays et où vous souhaitez affecter des calendriers professionnels en fonction du pays dans lequel l’utilisateur ou l’utilisatrice se trouve. Dans ce cas, vous indiquez le nom du champ pays dans le champ clé du calendrier professionnel. Vous pouvez ensuite associer les clés de calendrier professionnel (valeurs définies pour le champ pays dans l’annuaire LDAP) aux calendriers professionnels dans Forms Workflow.

Pour plus d’informations sur les calendriers professionnels, notamment sur la façon d’associer des clés de calendrier professionnel à des calendriers professionnels, voir [Configuration des calendriers professionnels](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limitez la longueur du nom à moins de 53 caractères. Un nom court contribue à réduire les problèmes d’affichage de la clé de calendrier professionnel dans les pages Process Management d’Administration Console.

**ID utilisateur :**(obligatoire) ID que l’utilisateur utilise pour se connecter. L’ID utilisateur n’est pas sensible à la casse et doit être unique pour tout le domaine.

Dans les domaines d’entreprise, utilisez un attribut non ND comme ID utilisateur, car le ND d’un utilisateur ou d’une utilisatrice peut changer si l’utilisateur évolue au sein de l’entreprise. Ce paramètre dépend du serveur d’annuaire. La valeur est `objectGUID` pour Active Directory 2003, `nsuniqueID` pour Sun™ One et `guid` pour eDirectory.

Assurez-vous que l’ID utilisateur est unique. N’utilisez pas un ID qui était affecté à un utilisateur ou une utilisatrice supprimé(e).

AEM forms ne peut pas différencier les comptes d’utilisateurs qui possèdent des ID utilisateur et des mots de passe identiques mais qui appartiennent à des domaines différents. Pour éviter ce problème, ne créez pas de comptes portant le même ID utilisateur dans plusieurs domaines.

Si vous utilisez une base de données SQL Server, vous ne pouvez pas créer d’ID utilisateur contenant plus de 255 caractères.

Avec MySQL, l’ID utilisateur peut contenir des caractères étendus. Cependant, en cas de comparaison entre deux chaînes telles que abcde et âbcdè, aucune distinction n’est faite entre les deux. Par exemple, lors d’une synchronisation après l’ajout d’un nouvel utilisateur ou d’une nouvelle utilisatrice à la base de données, une comparaison est effectuée pour vérifier si cet ID utilisateur existe dans la base de données. Si la base de données contient déjà l’utilisateur ou l’utilisatrice *abcde* lorsque vous ajoutez le nouvel utilisateur ou la nouvelle utilisatrice *âbcdè*, la comparaison ne différencie pas ces deux noms. Le système suppose que l’utilisateur ou l’utilisatrice existe dans la base de données et ne procède donc pas à l’ajout de ce dernier.

Évitez de créer des noms d’utilisateur commençant par un dièse (#). Les recherches de tâches ne renvoient aucun résultat pour ces noms d’utilisateur. (Voir [Utilisation des tâches](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Mot de passe et Confirmer le mot de passe :** mot de passe que l’utilisateur ou l’utilisatrice utilise pour se connecter. Il doit contenir au moins huit caractères. Aucun mot de passe n’est exigé si l’utilisateur ou l’utilisatrice fait partie d’un domaine hybride.

## Afficher les détails d’un utilisateur ou d’une utilisatrice {#view-details-about-a-user}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Indiquez les informations permettant d’affiner la recherche, puis, dans la liste Dans, sélectionnez Utilisateurs et cliquez sur Rechercher. Les résultats de la recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur l’un des en-têtes de colonne.
1. Cliquez sur le nom de l’utilisateur ou de l’utilisatrice dont vous souhaitez afficher les détails. La page Modifier l’utilisateur affiche les informations détaillées indiquées relatives à l’utilisateur ou l’utilisatrice :

   * Informations d’identification d’ordre général, telles que nom, adresse e-mail, adresse, domaine et société
   * Rôles qui lui sont affectés
   * Groupes dont il ou elle est membre

## Modifier le mot de passe d’un utilisateur local ou d’une utilisatrice locale {#change-the-password-for-a-local-user}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > Gestion des utilisateurs > Utilisateurs et groupes]**.
1. Indiquez les informations permettant d’affiner la recherche pour un utilisateur particulier et cliquez sur **[!UICONTROL Rechercher]**. Les résultats de la recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur l’un des en-têtes de colonne.
1. Cliquez sur le nom de l’utilisateur, puis sur **[!UICONTROL Modifier le mot de passe]**.
1. Saisissez et confirmez le nouveau mot de passe puis cliquez sur **[!UICONTROL OK]**. Le mot de passe doit contenir au moins huit caractères.

## Modifier les propriétés d’un utilisateur ou d’une utilisatrice {#edit-a-user-s-properties}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > Gestion des utilisateurs > Utilisateurs et groupes]**.
1. Pour rechercher l’utilisateur à modifier, procédez comme suit :

   * Dans la zone **[!UICONTROL Rechercher]**, saisissez vos critères de recherche.
   * Dans la liste **[!UICONTROL Utilisation]**, sélectionnez **[!UICONTROL Nom]**, **[!UICONTROL E-mail]** ou **[!UICONTROL ID utilisateur]**.
   * Dans la liste **[!UICONTROL Dans]**, sélectionnez **[!UICONTROL Utilisateurs]**.
   * Sélectionnez le domaine, indiquez le nombre d’éléments à afficher, puis cliquez sur **[!UICONTROL Rechercher]**.

1. Cliquez sur l’utilisateur à modifier.
1. Dans le cas d’un utilisateur appartenant à un domaine local ou hybride, modifiez les **[!UICONTROL paramètres généraux]** et les **[!UICONTROL paramètres de connexion]** dans l’onglet **[!UICONTROL Détails]**, puis cliquez sur **[!UICONTROL Enregistrer]**. Pour plus d’informations sur ces paramètres, voir [Paramètres utilisateur](adding-configuring-users.md#user-settings). Vous ne pouvez pas modifier les paramètres généraux ni les paramètres de connexion d’un utilisateur ou d’une utilisatrice appartenant à un domaine d’entreprise.
1. Pour modifier les paramètres du groupe de l’utilisateur, cliquez sur l’onglet **[!UICONTROL Membres du groupe]** et procédez comme suit :

   * Cliquez sur **[!UICONTROL Rechercher des groupes]** et renseignez les informations de recherche.
   * Pour ajouter l’utilisateur à un nouveau groupe, cochez la case correspondant au groupe, cliquez sur **[!UICONTROL OK]**, puis sur **[!UICONTROL Enregistrer]**.

   >[!NOTE]
   >
   >Les utilisateurs locauxet les utilisatrices locales ne peuvent pas être ajoutés aux groupes de répertoires. Toutefois, les utilisateurs et utilisatrices de répertoires peuvent être ajoutés aux groupes locaux.

   * Pour supprimer l’utilisateur d’un groupe, activez la case à cocher correspondant au groupe, cliquez sur **[!UICONTROL Supprimer]**, puis sur **[!UICONTROL Enregistrer]**.

1. Pour modifier les rôles de l’utilisateur ou de l’utilisatrice, cliquez sur l’onglet **[!UICONTROL Affectations de rôles]** et procédez comme suit :

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
>AEM Forms on JEE permet également aux utilisateurs et utilisatrices du module complémentaire AEM Forms exécuté dans un environnement OSGi d’être reconnus comme des utilisateurs et utilisatrices d’AEM. Cela est nécessaire dans les cas où une authentification unique entre AEM Forms on JEE et AEM Forms exécuté dans un environnement OSGi est requise (par exemple, lʼespace de travail HTML). L’opération de suppression mentionnée ci-dessus supprime un utilisateur d’AEM Forms sur JEE uniquement. L’utilisateur ou l’utilisatrice n’est pas supprimé du module complémentaire AEM Forms exécuté dans un environnement OSGi. Cependant, toute tentative de connexion effectuée après la suppression de l’utilisateur ou de l’utilisatrice (une tentative de connexion au serveur de module complémentaire AEM Forms JEE ou au module complémentaire AEM Forms dans un environnement OSGi) est refusée.

## Créer un gestionnaire d’erreur de connexion personnalisé {#create-custom-login-error-handler}

Si un utilisateur ou une utilisatrice ne disposant pas des autorisations AEM Forms et CQ requises tente de se connecter aux applications suivantes intégrées à CQ, la personne est redirigée vers la page CQ 404 par défaut contenant la trace de l’erreur :

* Solution Correspondence Management
* Espace de travail AEM Forms

  ***Remarque ** : Flex Workspace est obsolète pour la version d’AEM Forms.*

* gestionnaire de formulaires
* Rapports de workflow

CQ fournit un mécanisme pour remplacer le jsp du gestionnaire 404 par défaut.

Pour plus d’informations sur la personnalisation de la page de gestion des erreurs, reportez-vous à la rubrique [Personnalisation des pages affichées par le gestionnaire d’erreur](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=fr) dans la documentation d’Adobe Experience Manager.
