---
title: Configurer votre campagne
description: La configuration d’une nouvelle campagne nécessite la création d’une marque pour organiser vos campagnes, la création d’une campagne pour organiser des expériences et, enfin, la définition des propriétés de votre nouvelle campagne.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b607a52-f065-4e35-8215-d54df7c8403d
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2194'
ht-degree: 100%

---

# Configurer votre campagne{#setting-up-your-campaign}

La configuration d’une nouvelle campagne comprend les étapes (génériques) suivantes :

1. [Créer une marque](#creating-a-new-brand) pour organiser vos campagnes.
1. Le cas échéant, vous pouvez[ définir les propriétés de votre nouvelle marque](#defining-the-properties-for-your-new-brand).
1. [Créer une campagne](#creating-a-new-campaign) pour organiser des expériences, par exemple des pages teaser ou une newsletter.
1. Le cas échéant, vous pouvez[ définir les propriétés de votre nouvelle campagne](#defining-the-properties-for-your-new-campaign).

Ensuite, selon le type d’expériences que vous créez, vous devez[ créer une expérience](#creating-a-new-experience). Les détails de l’expérience et les actions qui suivent sa création dépendent du type d’expérience que vous souhaitez créer :

* Pour la création d’un teaser :

   1. [Créez une expérience de teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaserexperience).
   1. [Ajoutez du contenu à votre teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttoyourteaser).
   1. [Créez un Touchpoint pour votre teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) (ajoutez votre teaser à une page de contenu).

* Pour la création d’une newsletter :

   1. [Créez une expérience de newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletterexperience).
   1. [Ajoutez du contenu aux diapositives.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   1. [Personnalisez la newsletter.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   1. [Créez une page de destination convaincante pour une newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage).
   1. [Envoyez la newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters) aux personnes abonnées ou aux prospects.

* Pour la création d’une offre Adobe Target (anciennement Test&amp;Target) :

   1. [Créez une expérience d’offre Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetofferexperience).
   1. [Intégrez-la à Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#integratewithadobetesttarget)

>[!NOTE]
>
>Voir [Segmentation](/help/sites-administering/campaign-segmentation.md) pour des instructions détaillées sur la définition de vos segments.

## Création d’une marque {#creating-a-new-brand}

1. Ouvrez le **MCM** et sélectionnez **Campagnes** dans le volet de gauche.

1. Sélectionnez **Nouveau...** pour saisir le **Titre** et le **Nom** ainsi que le modèle à utiliser pour votre nouvelle marque :

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Cliquez sur **Créer**. Votre nouvelle marque est affichée dans le MCM (avec une icône par défaut).

### Définir les propriétés de votre nouvelle marque {#defining-the-properties-for-your-new-brand}

1. Dans **Campagnes** dans le volet de gauche, sélectionnez votre nouvelle icône de marque dans le volet de droite puis cliquez sur **Propriétés...**.

   Vous pouvez saisir un **Titre**, une **Description** et une image à utiliser comme icône.

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. Cliquez sur **OK** pour enregistrer.

### Création d’une campagne {#creating-a-new-campaign}

1. Dans **Campagnes**, sélectionnez votre nouvelle marque dans le volet de gauche ou double-cliquez sur l’icône dans le volet de droite.

   La vue d’ensemble s’affiche (vide si la marque est nouvelle).

1. Cliquez sur **Nouveau...** et indiquez le **Titre**, le **Nom** et le modèle à utiliser pour votre nouvelle campagne.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Cliquez sur **Créer**. Votre nouvelle campagne s’affiche dans le MCM.

### Définir les propriétés de votre nouvelle campagne {#defining-the-properties-for-your-new-campaign}

Configurez les propriétés de campagne qui contrôlent le comportement :

* **Priorité :** indique la priorité de cette campagne par rapport aux autres campagnes. Si plusieurs campagnes sont en cours au même moment, la campagne présentant la priorité la plus élevée contrôle l’expérience des visiteurs.
* **Heures d’activation et de désactivation :** ces propriétés contrôlent la période pendant laquelle la campagne contrôle l’expérience du visiteur ou de la visiteuse. La propriété Heure d’activation contrôle l’heure à laquelle la campagne commence à contrôler l’expérience. La propriété Heure de désactivation contrôle le moment où les campagnes cessent de contrôler l’expérience.
* **Image :** l’image qui représente la campagne dans AEM.
* **Services Cloud :** les configurations des services cloud auxquels la campagne est intégrée (Voir [Intégration à Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md).)

* **Adobe Target :** propriétés qui configurent les campagnes intégrées à Adobe Target. (Voir [Intégration à Adobe Target](/help/sites-administering/target.md).)

1. Dans **Campagnes**, sélectionnez votre marque. Dans le volet de droite, sélectionnez votre campagne et cliquez sur **Propriétés**.

   Vous pouvez définir différentes propriétés, telles qu’un **Titre**, une **Description** et les **Services cloud** de votre choix.

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Cliquez sur **OK** pour enregistrer.

### Création d’une expérience {#creating-a-new-experience}

La procédure à suivre pour créer une expérience dépend du type d’expérience :

* [Création d’un teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaser)
* [Création d’une newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletter)
* [Création d’une offre Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetoffer)

>[!NOTE]
>
>Comme dans les versions précédentes, il est toujours possible de créer l’expérience sous forme de page dans la console **Sites Web** (et toutes les pages créées dans les versions précédentes sont toujours entièrement prises en charge).
>
>La pratique recommandée consiste désormais à utiliser le MCM pour créer des expériences.

### Configuration de votre nouvelle expérience {#configuring-your-new-experience}

Maintenant que vous avez configuré le schéma de base de votre expérience, vous devez poursuivre en réalisant les actions suivantes, en fonction du type d’expérience :

* [Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) :

   * [Connectez la page de teaser aux segments de visiteurs.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#applyingasegmenttoyourteaser)
   * [Créez un Touchpoint pour votre teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) (ajoutez votre teaser à une page de contenu).

* [Newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters) :

   * [Ajoutez du contenu aux diapositives.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   * [Personnalisez la newsletter.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   * [Envoyez la newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters) aux personnes abonnées ou aux prospects.
   * [Créez une page de destination attrayante pour une newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage).

* [Offre Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#testtargetoffers) :

   * [Intégrez-la à Adobe Target](/help/sites-administering/target.md)

### Ajout d’un nouveau point de contact {#adding-a-new-touchpoint}

Si vous disposez d’expériences existantes, vous pouvez ajouter un point de contact directement à partir de la vue Calendrier de MCM :

1. Sélectionnez la vue Calendrier pour votre campagne.

1. Cliquez sur **Ajouter un point de contact...** pour ouvrir la boîte de dialogue. Indiquez l’expérience que vous souhaitez ajouter :

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. Cliquez sur **OK** pour enregistrer.

## Utilisation des prospects {#working-with-leads}

>[!NOTE]
>
>Adobe ne prévoit pas d’optimiser cette fonctionnalité (gestion des prospects).
>Il est conseillé d’utiliser [Adobe Campaign et l’intégration à AEM](/help/sites-administering/campaign.md).

Dans AEM MCM, vous pouvez organiser et ajouter des prospects en les saisissant manuellement ou en important une liste séparée par des virgules. par exemple, une liste de diffusion. Pour générer des prospects, il existe d’autres méthodes comme les abonnements aux newsletters ou aux communautés (s’ils sont configurés de la sorte, ils peuvent déclencher un workflow pour renseigner les prospects).

Les prospects sont généralement catégorisés et mis dans une liste afin que vous puissiez ensuite effectuer des actions sur l’ensemble de la liste ; par exemple, envoyer un e-mail personnalisé à une certaine liste.

Dans le tableau de bord, vous accédez à tous les prospects en cliquant sur **Prospects** dans le volet gauche. Vous pouvez également accéder aux prospects à partir du volet **Listes**.

![screen_shot_2012-02-21at114748am](assets/screen_shot_2012-02-21at114748am.png)

>[!NOTE]
>
>Pour ajouter ou modifier les avatars des utilisateurs et utilisatrices, ouvrez le cloud clickstream (Ctrl+Alt+c), chargez le profil et cliquez sur **Modifier**.

### Création de prospects {#creating-new-leads}

Une fois les nouveaux prospects créés, assurez-vous de [les activer](#activating-or-deactivating-leads) pour pouvoir suivre leur activité sur l’instance de publication et personnaliser leur expérience.

Pour créer un prospect manuellement :

1. Dans AEM, accédez à MCM. Dans le tableau de bord, cliquez sur **Prospects**.
1. Cliquez sur **Nouveau**. La fenêtre **Créer** s’ouvre.

   ![screen_shot_2012-02-21at115008am](assets/screen_shot_2012-02-21at115008am.png)

1. Saisissez les informations dans les champs, le cas échéant. Cliquez sur l’onglet **Adresse**.

   ![screen_shot_2012-02-21at115045am](assets/screen_shot_2012-02-21at115045am.png)

1. Saisissez les informations d’adresse, le cas échéant. Cliquez sur **Enregistrer** pour enregistrer le prospect. Si vous avez besoin d’ajouter des prospects supplémentaires, cliquez sur **Enregistrer et Nouveau**.

   Le nouveau prospect apparaît dans le volet Prospects. Lorsque vous cliquez sur l’entrée, toutes les informations saisies apparaissent dans le volet de droite. Une fois que vous avez créé un prospect, vous pouvez l’ajouter à une liste.

   ![screen_shot_2012-02-21at120307pm](assets/screen_shot_2012-02-21at120307pm.png)

### Activer ou désactiver des prospects {#activating-or-deactivating-leads}

L’activation des prospects vous aide à suivre leur activité sur l’instance de publication et vous permet de personnaliser leur expérience. Lorsque vous ne souhaitez plus suivre leur activité, vous pouvez les désactiver.

Vers des prospects actifs ou désactivés :

1. Dans AEM, accédez à MCM et cliquez sur **Leads**.

1. Sélectionnez les prospects à activer ou désactiver et cliquez sur **Activer** ou **Désactiver**.

   ![screen_shot_2012-02-21at120620pm](assets/screen_shot_2012-02-21at120620pm.png)

   À l’instar des pages AEM, le statut de publication est indiqué dans la colonne **Publié**.

   ![screen_shot_2012-02-21at122901pm](assets/screen_shot_2012-02-21at122901pm.png)

### Importer de nouveaux prospects {#importing-new-leads}

Lorsque vous importez de nouveaux prospects, vous pouvez les ajouter automatiquement à une liste existante ou créer une liste pour les y inclure.

Pour importer des prospects à partir d’une liste séparée par des virgules :

1. Dans AEM, accédez à MCM et cliquez sur **Leads**.

   >[!NOTE]
   >
   >Vous pouvez également importer des prospects en effectuant l’une des opérations suivantes :
   >
   >* Dans le tableau de bord, cliquez sur **Importer des prospects** dans le volet **Listes**.
   >* Cliquez sur **Listes**. Dans le menu **Outils**, sélectionnez **Importer des prospects**.

1. Dans le menu **Outils**, sélectionnez **Importer** **les pistes**.

1. Saisissez les informations, tel qu’indiqué dans Données d’exemple. Les champs suivants peuvent être importés : email,familyName,givenName,gender,aboutMe,city,country,phoneNumber,postalCode,region,streetAddress.

   >[!NOTE]
   >
   >La première ligne de la liste CSV contient des libellés prédéfinis qui doivent être écrits exactement comme dans l’exemple :
   >
   >
   >`email,givenName,familyName` - En cas d’utilisation du format `givenname`, par exemple, le système ne le reconnaîtra pas.
   >
   >

   ![screen_shot_2012-02-21at123055pm](assets/screen_shot_2012-02-21at123055pm.png)

1. Cliquez sur **Suivant**. Ici, vous affichez un aperçu des prospects pour vérifier qu’ils sont exacts.

   ![screen_shot_2012-02-21at123104pm](assets/screen_shot_2012-02-21at123104pm.png)

1. Cliquez sur **Suivant**. Sélectionnez la liste à laquelle vous souhaitez que les prospects appartiennent. Si vous ne souhaitez pas qu’ils appartiennent à une liste, supprimez les informations du champ. Par défaut, AEM crée un nom de liste qui inclut la date et l’heure. Cliquez sur **Importer**.

   ![screen_shot_2012-02-21at123123pm](assets/screen_shot_2012-02-21at123123pm.png)

   Le nouveau prospect apparaît dans le volet Prospects. Si vous cliquez sur l’entrée, toutes les informations saisies apparaissent dans le volet de droite. Une fois que vous avez créé un prospect, vous pouvez l’ajouter à une liste.

### Ajout de prospects à des listes {#adding-leads-to-lists}

Pour ajouter des prospects à des listes préexistantes :

1. Dans MCM, cliquez sur **Prospects** pour afficher tous les prospects disponibles.

1. Sélectionnez les prospects que vous souhaitez ajouter à une liste en cochant la case en regard de chacun. Vous pouvez ajouter autant de prospects que vous le souhaitez.

   ![screen_shot_2012-02-21at123835pm](assets/screen_shot_2012-02-21at123835pm.png)

1. Dans le menu **Outils**, sélectionnez **Ajouter à la liste...** La fenêtre **Ajouter à la liste** s’ouvre.

   ![screen_shot_2012-02-21at124019pm](assets/screen_shot_2012-02-21at124019pm.png)

1. Sélectionnez la liste à laquelle vous souhaitez ajouter les prospects et cliquez sur **OK**. Les prospects sont ajoutés aux listes appropriées.

### Afficher les informations sur les prospects {#viewing-lead-information}

Pour afficher les informations sur le prospect, dans le MCM, cochez la case en regard de son nom. Un volet s’ouvre à droite avec toutes les informations du prospect affichées, y compris l’affiliation à la liste.

![screen_shot_2012-02-21at124228pm](assets/screen_shot_2012-02-21at124228pm.png)

### Modifier des prospects existants {#modifying-existing-leads}

Pour modifier les informations sur les prospects existants :

1. Dans le MCM, cliquez sur **Prospects**. Dans la liste des prospects, cochez la case en regard du prospect que vous souhaitez modifier. Toutes les informations sur les prospects apparaissent dans le volet de droite.

   ![screen_shot_2012-02-21at124514pm](assets/screen_shot_2012-02-21at124514pm.png)

   >[!NOTE]
   >
   >Vous ne pouvez modifier qu’un seul prospect à la fois. Si vous devez modifier des prospects qui font partie de la même liste, vous pouvez modifier la liste à la place.

1. Cliquez sur **Modifier**. La fenêtre **Modifier le prospect** s’ouvre.

   ![screen_shot_2012-02-21at124609pm](assets/screen_shot_2012-02-21at124609pm.png)

1. Apportez les modifications nécessaires et cliquez sur **Enregistrer** pour enregistrer vos modifications.

   >[!NOTE]
   >
   >Pour changer l’avatar du prospect, accédez au profil de l’utilisateur ou l’utilisatrice. Vous pouvez charger le profil dans le cloud clickstream en appuyant sur CTRL+ALT+c, en cliquant sur **Charger**, puis en sélectionnant le profil.

### Supprimer des prospects existants {#deleting-existing-leads}

Pour supprimer des prospects existants dans le MCM, cochez la case en regard du prospect et cliquez sur **Supprimer**. Le prospect est supprimé de la liste des prospects et de toutes les listes associées.

>[!NOTE]
>
>Avant la suppression, AEM confirme que vous souhaitez supprimer le prospect existant. Une fois la suppression réalisée, elle ne peut pas être annulée.

## Utiliser les listes {#working-with-lists}

>[!NOTE]
>
>Adobe ne prévoit pas d’optimiser cette fonctionnalité (gestion des listes).
>Il est recommandé d’utiliser [Adobe Campaign et l’intégration dans AEM](/help/sites-administering/campaign.md).

Les listes vous permettent d’organiser vos prospects en groupes. Avec les listes, vous pouvez cibler vos campagnes marketing sur un groupe de personnes sélectionné. Vous pouvez par exemple envoyer une newsletter ciblée à une liste. Les listes sont visibles dans le MCM, soit dans le tableau de bord, soit en cliquant sur **Listes**. Tous deux vous fournissent le nom de la liste et le nombre de membres.

![screen_shot_2012-02-21at125021pm](assets/screen_shot_2012-02-21at125021pm.png)

Si vous cliquez sur **Listes**, vous pouvez également voir si la liste est membre d’une autre liste et afficher une description.

![screen_shot_2012-02-21at124828pm](assets/screen_shot_2012-02-21at124828pm.png)

### Créer des listes {#creating-new-lists}

1. Dans le tableau de bord MCM, cliquez sur **Nouvelle liste...** ou dans **Listes**, cliquez sur **Nouveau**... La fenêtre Créer une liste s’ouvre.

   ![screen_shot_2012-02-21at125147pm](assets/screen_shot_2012-02-21at125147pm.png)

1. Entrez un nom (obligatoire) et, si vous le souhaitez, une description, puis cliquez sur **Enregistrer**. La liste apparaît dans le volet **Listes**.

   ![screen_shot_2012-02-21at125320pm](assets/screen_shot_2012-02-21at125320pm.png)

### Modifier des listes existantes {#modifying-existing-lists}

1. Dans le MCM, cliquez sur **Listes**.

1. Dans la liste, cochez la case en regard de la liste que vous souhaitez modifier et cliquez sur **Modifier**. La fenêtre **Modifier la liste** s’ouvre.

   ![screen_shot_2012-02-21at125452pm](assets/screen_shot_2012-02-21at125452pm.png)

   >[!NOTE]
   >
   >Vous ne pouvez modifier qu’une liste à la fois.

1. Apportez les modifications nécessaires et cliquez sur **Enregistrer** pour enregistrer vos modifications.

### Supprimer des listes existantes {#deleting-existing-lists}

Pour supprimer des listes existantes, dans le MCM, cochez la case en regard de la liste concernée et cliquez sur **Supprimer**. La liste est supprimée. Les prospects affiliés à la liste ne sont pas supprimés : seule l’affiliation à la liste est supprimée.

>[!NOTE]
>
>Avant de procéder, AEM confirme que vous souhaitez supprimer les listes existantes. Une fois la suppression réalisée, elle ne peut pas être annulée.

### Fusionner des listes {#merging-lists}

Vous pouvez fusionner une liste existante avec une autre liste. Lorsque vous effectuez cette opération, la liste que vous fusionnez devient membre de l’autre liste. Elle existe toujours en tant qu’entité distincte et ne doit pas être supprimée.

Vous pouvez fusionner des listes si vous organisez la même conférence dans deux endroits différents et que vous souhaitez les fusionner en une liste des participants à toutes les conférences.

Pour fusionner des listes existantes :

1. Dans le MCM, cliquez sur **Listes**.

1. Sélectionnez la liste avec laquelle vous souhaitez fusionner une autre liste en cochant la case en regard de celle-ci.

1. Dans le menu **Outils**, sélectionnez **Fusionner la liste**.

   >[!NOTE]
   >
   >Vous ne pouvez fusionner qu’une liste à la fois.

1. Dans la fenêtre **Fusionner la liste**, sélectionnez la liste avec laquelle vous souhaitez fusionner et cliquez sur **OK**.

   ![screen_shot_2012-02-21at10259pm](assets/screen_shot_2012-02-21at10259pm.png)

   La liste que vous avez fusionnée devrait augmenter d’un membre. Pour vérifier que votre liste a été fusionnée, sélectionnez la liste que vous avez fusionnée et, dans le menu **Outils**, sélectionnez **Afficher les prospects**.

1. Répétez l’étape jusqu’à fusionner toutes les listes souhaitées.

   ![screen_shot_2012-02-21at10538pm](assets/screen_shot_2012-02-21at10538pm.png)

>[!NOTE]
>
>Supprimer une liste fusionnée de son abonnement revient à supprimer un prospect d’une liste. Ouvrez l’onglet **Listes**, sélectionnez la liste qui contient la liste fusionnée et supprimez l’abonnement en cliquant sur le cercle rouge à côté de la liste.

### Afficher des prospects dans des listes {#viewing-leads-in-lists}

À tout moment, vous pouvez voir les prospects qui appartiennent à une liste spécifique en parcourant les membres ou en les recherchant.

Pour afficher les prospects dans des listes :

1. Dans le MCM, cliquez sur **Listes**.

1. Cochez la case en regard de la liste dont vous souhaitez afficher les membres.

1. Dans le menu **Outils**, sélectionnez **Afficher les prospects**. AEM affiche les prospects membres de cette liste. Vous pouvez parcourir la liste ou rechercher des membres.

   >[!NOTE]
   >
   >De plus, vous pouvez supprimer des prospects d’une liste en les sélectionnant puis en cliquant sur **Supprimer l’abonnement**.

   ![screen_shot_2012-02-21at10828pm](assets/screen_shot_2012-02-21at10828pm.png)

1. Cliquez sur **Fermer** pour revenir au MCM.
