---
title: Configurer votre campagne
description: La configuration d’une nouvelle campagne nécessite la création d’une marque qui contiendra vos campagnes, la création d’une campagne qui contiendra des expériences et enfin la définition des propriétés de votre nouvelle campagne.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b607a52-f065-4e35-8215-d54df7c8403d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2223'
ht-degree: 18%

---

# Configurer votre campagne{#setting-up-your-campaign}

La configuration d&#39;une nouvelle campagne comprend les étapes (génériques) suivantes :

1. [Créer une marque](#creating-a-new-brand) pour héberger vos campagnes.
1. Si nécessaire, vous pouvez [définir les propriétés de votre nouvelle marque ;](#defining-the-properties-for-your-new-brand).
1. [Créer une campagne](#creating-a-new-campaign) pour contenir des expériences ; par exemple, des pages de teaser ou une newsletter.
1. Si nécessaire, vous pouvez [définir les propriétés de votre nouvelle campagne ;](#defining-the-properties-for-your-new-campaign).

Ensuite, en fonction du type d’expérience que vous créez, vous devez [créer une expérience](#creating-a-new-experience). Les détails de l’expérience et les actions qui suivent sa création dépendent du type d’expérience que vous souhaitez créer :

* Lors de la création d’un teaser :

   1. [Création d’une expérience de teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaserexperience).
   1. [Ajout de contenu à votre teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttoyourteaser).
   1. [Création d’un point de contact pour votre teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) (ajoutez votre teaser à une page de contenu).

* Si vous créez une newsletter :

   1. [Création d’une expérience de newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletterexperience).
   1. [Ajoutez du contenu aux diapositives.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   1. [Personnalisez la newsletter.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   1. [Créer une page d’entrée de newsletter attrayante](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage).
   1. [Envoyer la newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters) aux abonnés ou aux prospects.

* Lors de la création d’une offre Adobe Target (anciennement Test&amp;Target) :

   1. [Création d’une expérience d’offre Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetofferexperience).
   1. [Intégrez-la à Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#integratewithadobetesttarget)

>[!NOTE]
>
>Voir [Segmentation](/help/sites-administering/campaign-segmentation.md) pour obtenir des instructions détaillées sur la définition de vos segments.

## Création d’une marque {#creating-a-new-brand}

1. Ouvrez le **MCM** et sélectionnez **Campagnes** dans le volet de gauche.

1. Sélectionner **Nouveau...** pour saisir la variable **Titre** et **Nom** et modèle à utiliser pour votre nouvelle marque :

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Cliquez sur **Créer**. Votre nouvelle marque s’affiche dans le MCM (avec une icône par défaut).

### Définition des propriétés de votre nouvelle marque {#defining-the-properties-for-your-new-brand}

1. De **Campagnes** dans le volet de gauche, sélectionnez l’icône de nouvelle marque dans le volet de droite, puis cliquez sur **Propriétés...**

   Vous pouvez saisir un **Titre**, **Description** et une image à utiliser comme icône.

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. Cliquez sur **OK** pour enregistrer.

### Création d’une campagne {#creating-a-new-campaign}

1. De **Campagnes**, sélectionnez votre nouvelle marque dans le volet de gauche ou double-cliquez sur l’icône dans le volet de droite.

   L’aperçu s’affiche (vide si la marque est nouvelle).

1. Cliquez sur **Nouveau...** et spécifiez la variable **Titre**, **Nom** et le modèle à utiliser pour votre nouvelle campagne.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Cliquez sur **Créer**. Votre nouvelle campagne s’affiche dans le MCM.

### Définition des propriétés de votre nouvelle campagne {#defining-the-properties-for-your-new-campaign}

Configurez les propriétés de campagne qui contrôlent le comportement :

* **Priorité :** La priorité de cette campagne par rapport aux autres campagnes. Si plusieurs campagnes sont en cours au même moment, la campagne présentant la priorité la plus élevée contrôle l’expérience des visiteurs.
* **Heure d’activation et de désactivation :** Ces propriétés contrôlent la période pendant laquelle la campagne contrôle l’expérience du visiteur. La propriété Heure d’activation contrôle l’heure à laquelle la campagne commence à contrôler l’expérience. La propriété Heure de désactivation contrôle le moment où les campagnes cessent de contrôler l’expérience.
* **Image :** L’image qui représente la campagne dans AEM.
* **Services Cloud :** les configurations des services cloud auxquels la campagne est intégrée (Voir [Intégration à Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md).)

* **ADOBE TARGET :** Propriétés qui configurent les campagnes intégrées à Adobe Target. (Voir [Intégration à Adobe Target](/help/sites-administering/target.md).)

1. De **Campagnes**, sélectionnez votre marque. Dans le volet de droite, sélectionnez votre campagne et cliquez sur **Propriétés**.

   Vous pouvez définir différentes propriétés, telles qu’un **Titre**, une **Description** et les **Services cloud** de votre choix.

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Cliquez sur **OK** pour enregistrer.

### Création d’une expérience {#creating-a-new-experience}

La procédure de création d’une expérience dépend du type d’expérience :

* [Création d’un teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaser)
* [Création d’une newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletter)
* [Création d’une offre Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetoffer)

>[!NOTE]
>
>Comme pour les versions précédentes, il est toujours possible de créer l’expérience sous la forme d’une page dans le **Sites web** (et toutes les pages de ce type créées dans les versions précédentes sont toujours entièrement prises en charge).
>
>Il est désormais recommandé d’utiliser MCM pour créer des expériences.

### Configuration de votre nouvelle expérience {#configuring-your-new-experience}

Maintenant que vous avez créé le squelette de base de votre expérience, vous devez poursuivre les actions suivantes, selon le type d’expérience :

* [Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) :

   * [Connectez la page de teaser aux segments de visiteurs.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#applyingasegmenttoyourteaser)
   * [Création d’un point de contact pour votre teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) (ajoutez votre teaser à une page de contenu).

* [Newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters):

   * [Ajoutez du contenu aux diapositives.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   * [Personnalisez la newsletter.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   * [Envoyer la newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters) aux abonnés ou aux prospects.
   * [Créer une page d’entrée de newsletter attrayante](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage).

* [Offre Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#testtargetoffers):

   * [Intégrez-la à Adobe Target](/help/sites-administering/target.md)

### Ajout d’un nouveau point de contact {#adding-a-new-touchpoint}

Si vous disposez d’expériences existantes, vous pouvez ajouter un point de contact directement à partir de la vue Calendrier de MCM :

1. Sélectionnez la vue Calendrier de votre campagne.

1. Cliquez sur **Ajouter un point de contact...** pour ouvrir la boîte de dialogue. Spécifiez l’expérience à ajouter :

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. Cliquez sur **OK** pour enregistrer.

## Utilisation des prospects {#working-with-leads}

>[!NOTE]
>
>Adobe ne prévoit pas d’optimiser cette fonctionnalité (gestion des prospects).
>Il est recommandé d’utiliser [Adobe Campaign et intégration à AEM](/help/sites-administering/campaign.md).

Dans AEM MCM, vous pouvez organiser et ajouter des pistes en les saisissant manuellement ou en important une liste de valeurs séparées par des virgules, par exemple une liste de diffusion. Les autres moyens de générer des pistes sont les abonnements à des newsletters ou les abonnements à des communautés (s’ils sont configurés, ils peuvent déclencher un workflow qui renseigne les pistes).

Les pistes sont généralement classées et mises dans une liste afin que vous puissiez plus tard exécuter des actions sur l’ensemble de la liste, par exemple envoyer un email personnalisé à une certaine liste.

Dans le tableau de bord, vous accédez à toutes les pistes en cliquant sur **Pistes** dans le volet de gauche. Vous pouvez également accéder aux pistes à partir du **Listes** volet.

![screen_shot_2012-02-21at114748am](assets/screen_shot_2012-02-21at114748am.png)

>[!NOTE]
>
>Pour ajouter ou modifier les avatars des utilisateurs, ouvrez le cloud de parcours de navigation (Ctrl+Alt+c), chargez le profil, puis cliquez sur **Modifier**.

### Créer de nouvelles pistes {#creating-new-leads}

Une fois les nouveaux prospects créés, assurez-vous de [les activer](#activating-or-deactivating-leads) pour pouvoir suivre leur activité sur l’instance de publication et personnaliser leur expérience.

Pour créer manuellement une piste :

1. Dans AEM, accédez au MCM. Dans le tableau de bord, cliquez sur **Pistes**.
1. Cliquez sur **Nouveau**. La variable **Créer** s’ouvre.

   ![screen_shot_2012-02-21at115008am](assets/screen_shot_2012-02-21at115008am.png)

1. Renseignez les informations dans les champs, le cas échéant. Cliquez sur le bouton **Adresse** .

   ![screen_shot_2012-02-21at115045am](assets/screen_shot_2012-02-21at115045am.png)

1. Saisissez les informations d’adresse, le cas échéant. Cliquez sur **Enregistrer** pour enregistrer le prospect. Si vous avez besoin d’ajouter des prospects supplémentaires, cliquez sur **Enregistrer et Nouveau**.

   La nouvelle piste s’affiche dans le volet Pistes . Lorsque vous cliquez sur l’entrée, toutes les informations saisies s’affichent dans le volet de droite. Après avoir créé une piste, vous pouvez l’ajouter à une liste.

   ![screen_shot_2012-02-21at120307pm](assets/screen_shot_2012-02-21at120307pm.png)

### Activation ou désactivation de pistes {#activating-or-deactivating-leads}

L’activation de pistes vous permet de suivre leur activité sur l’instance de publication et de personnaliser leur expérience. Lorsque vous ne souhaitez plus suivre leur activité, vous pouvez la désactiver.

Pour activer ou désactiver des pistes :

1. Dans AEM, accédez à MCM et cliquez sur **Leads**.

1. Sélectionnez les prospects à activer ou désactiver et cliquez sur **Activer** ou **Désactiver**.

   ![screen_shot_2012-02-21at120620pm](assets/screen_shot_2012-02-21at120620pm.png)

   À l’instar des pages AEM, le statut de publication est indiqué dans la colonne **Publié**.

   ![screen_shot_2012-02-21at122901pm](assets/screen_shot_2012-02-21at122901pm.png)

### Importer de nouvelles pistes {#importing-new-leads}

Lorsque vous importez de nouvelles pistes, vous pouvez les ajouter automatiquement à une liste existante ou créer une liste pour les inclure.

Pour importer des pistes à partir d’une liste séparée par des virgules :

1. Dans AEM, accédez à MCM et cliquez sur **Leads**.

   >[!NOTE]
   >
   >Vous pouvez également importer des pistes en effectuant l’une des opérations suivantes :
   >
   >* Dans le tableau de bord, cliquez sur **Importer des pistes** dans le **Listes** volet
   >* Cliquez sur **Listes** et dans le **Outils** menu, sélectionnez **Importer des pistes**.

1. Dans le menu **Outils**, sélectionnez **Importer** **les pistes**.

1. Saisissez les informations comme décrit dans la section Exemple de données. Les champs suivants peuvent être importés : email,familyName,givenName,gender,aboutMe,city,country,phoneNumber,postalCode,region,streetAddress

   >[!NOTE]
   >
   >La première ligne de la liste CSV est un libellé prédéfini qui doit être écrit exactement comme dans l’exemple suivant :
   >
   >
   >`email,givenName,familyName` - En cas d’utilisation du format `givenname`, par exemple, le système ne le reconnaîtra pas.
   >
   >

   ![screen_shot_2012-02-21at123055pm](assets/screen_shot_2012-02-21at123055pm.png)

1. Cliquez sur **Suivant**. Ici, vous affichez un aperçu des prospects pour vérifier qu’ils sont exacts.

   ![screen_shot_2012-02-21at123104pm](assets/screen_shot_2012-02-21at123104pm.png)

1. Cliquez sur **Suivant**. Sélectionnez la liste à laquelle vous souhaitez que les pistes appartiennent. Si vous ne souhaitez pas qu’ils appartiennent à une liste, supprimez les informations du champ. Par défaut, AEM crée un nom de liste incluant la date et l’heure. Cliquez sur **Importer**.

   ![screen_shot_2012-02-21at123123pm](assets/screen_shot_2012-02-21at123123pm.png)

   La nouvelle piste s’affiche dans le volet Pistes . Si vous cliquez sur l’entrée, toutes les informations saisies s’affichent dans le volet de droite. Après avoir créé une piste, vous pouvez l’ajouter à une liste.

### Ajout de pistes aux listes {#adding-leads-to-lists}

Pour ajouter des pistes à des listes préexistantes :

1. Dans le MCM, cliquez sur **Pistes** pour afficher toutes les pistes disponibles.

1. Sélectionnez les pistes à ajouter à une liste en cochant la case située en regard de celle-ci. Vous pouvez ajouter autant de pistes que vous le souhaitez.

   ![screen_shot_2012-02-21at123835pm](assets/screen_shot_2012-02-21at123835pm.png)

1. Dans le menu **Outils**, sélectionnez **Ajouter à la liste...** La fenêtre **Ajouter à la liste** s’ouvre.

   ![screen_shot_2012-02-21at124019pm](assets/screen_shot_2012-02-21at124019pm.png)

1. Sélectionnez la liste à laquelle vous souhaitez ajouter les pistes, puis cliquez sur **OK**. Les pistes sont ajoutées aux listes appropriées.

### Affichage des informations de piste {#viewing-lead-information}

Pour afficher les informations de piste, dans le MCM, cochez la case en regard de la piste. Un volet de droite s’ouvre, affichant toutes les informations de la piste, y compris l’affiliation à la liste.

![screen_shot_2012-02-21at124228pm](assets/screen_shot_2012-02-21at124228pm.png)

### Modification de pistes existantes {#modifying-existing-leads}

Pour modifier les informations de piste existantes :

1. Dans le MCM, cliquez sur **Pistes**. Dans la liste des pistes, cochez la case en regard de la piste à modifier. Toutes les informations de piste s’affichent dans le volet de droite.

   ![screen_shot_2012-02-21at124514pm](assets/screen_shot_2012-02-21at124514pm.png)

   >[!NOTE]
   >
   >Vous ne pouvez modifier qu’une seule piste à la fois. Si vous devez modifier des pistes qui font partie de la même liste, vous pouvez modifier la liste à la place.

1. Cliquez sur **Modifier**. La variable **Modifier la piste** s’ouvre.

   ![screen_shot_2012-02-21at124609pm](assets/screen_shot_2012-02-21at124609pm.png)

1. Apportez les modifications nécessaires, puis cliquez sur **Enregistrer** pour enregistrer vos modifications.

   >[!NOTE]
   >
   >Pour modifier l’avatar de piste, accédez au profil des utilisateurs. Vous pouvez charger le profil dans le cloud de parcours de navigation en appuyant sur CTRL+ALT+c, puis en cliquant sur **Chargement**, puis en sélectionnant le profil.

### Suppression de pistes existantes {#deleting-existing-leads}

Pour supprimer des pistes existantes dans le MCM, cochez la case en regard de la piste et cliquez sur **Supprimer**. La piste est supprimée de la liste de pistes et de toutes les listes associées.

>[!NOTE]
>
>Avant la suppression, AEM confirme que vous souhaitez supprimer la piste existante. Une fois supprimé, il ne peut plus être récupéré.

## Utilisation de listes {#working-with-lists}

>[!NOTE]
>
>Adobe ne prévoit pas d’optimiser cette fonctionnalité (gestion des listes).
>Il est recommandé d’utiliser [Adobe Campaign et intégration à AEM](/help/sites-administering/campaign.md).

Les listes vous permettent d’organiser vos prospects en groupes. Avec les listes, vous pouvez cibler vos campagnes marketing sur un groupe sélectionné de personnes, par exemple, vous pouvez envoyer une newsletter ciblée à une liste. Les listes sont visibles dans le MCM, soit dans le tableau de bord, soit en cliquant sur **Listes**. Ils vous fournissent tous deux le nom de la liste et le nombre de membres.

![screen_shot_2012-02-21at125021pm](assets/screen_shot_2012-02-21at125021pm.png)

Si vous cliquez sur **Listes**, vous pouvez également voir si la liste est membre d’une autre liste et afficher une description.

![screen_shot_2012-02-21at124828pm](assets/screen_shot_2012-02-21at124828pm.png)

### Créer de nouvelles listes {#creating-new-lists}

1. Dans le tableau de bord MCM, cliquez sur **Nouvelle liste ...** ou **Listes**, cliquez sur **Nouveau** .. La fenêtre Créer une liste s’affiche.

   ![screen_shot_2012-02-21at125147pm](assets/screen_shot_2012-02-21at125147pm.png)

1. Saisissez un nom (obligatoire) et, si vous le souhaitez, une description, puis cliquez sur **Enregistrer**. La liste apparaît dans la **Listes** volet.

   ![screen_shot_2012-02-21at125320pm](assets/screen_shot_2012-02-21at125320pm.png)

### Modification de listes existantes {#modifying-existing-lists}

1. Dans le MCM, cliquez sur **Listes**.

1. Dans la liste, cochez la case en regard de la liste à modifier, puis cliquez sur **Modifier**. La variable **Modifier la liste** s’ouvre.

   ![screen_shot_2012-02-21at125452pm](assets/screen_shot_2012-02-21at125452pm.png)

   >[!NOTE]
   >
   >Vous ne pouvez modifier qu’une seule liste à la fois.

1. Apportez les modifications nécessaires, puis cliquez sur **Enregistrer** pour enregistrer vos modifications.

### Suppression de listes existantes {#deleting-existing-lists}

Pour supprimer des listes existantes, dans le MCM, cochez la case en regard de la liste et cliquez sur **Supprimer**. La liste est supprimée. Les pistes qui étaient affiliées à la liste ne sont pas supprimées : seule l’appartenance à la liste est supprimée.

>[!NOTE]
>
>Avant la suppression, AEM confirme que vous souhaitez supprimer les listes existantes. Une fois supprimé, il ne peut plus être récupéré.

### Fusion de listes {#merging-lists}

Vous pouvez fusionner une liste existante avec une autre liste. Dans ce cas, la liste que vous fusionnez devient membre de l’autre liste. Il existe toujours en tant qu’entité distincte et ne doit pas être supprimé.

Vous pouvez fusionner des listes si vous avez la même conférence à deux endroits différents et que vous souhaitez les fusionner dans une liste de participants de toutes les conférences.

Pour fusionner des listes existantes :

1. Dans le MCM, cliquez sur **Listes**.

1. Sélectionnez la liste avec laquelle vous souhaitez fusionner une autre liste en cochant la case en regard de celle-ci.

1. Dans le **Outils** menu, sélectionnez **Liste de fusion**.

   >[!NOTE]
   >
   >Vous ne pouvez fusionner qu’une seule liste à la fois.

1. Dans le **Liste de fusion** , sélectionnez la liste à fusionner, puis cliquez sur **OK**.

   ![screen_shot_2012-02-21at10259pm](assets/screen_shot_2012-02-21at10259pm.png)

   La liste que vous avez fusionnée doit augmenter d’un membre. Pour vous assurer que votre liste a été fusionnée, sélectionnez la liste que vous avez fusionnée et dans le **Outils** menu, sélectionnez **Afficher les pistes**.

1. Répétez l’étape jusqu’à ce que vous ayez fusionné toutes les listes de votre choix.

   ![screen_shot_2012-02-21at10538pm](assets/screen_shot_2012-02-21at10538pm.png)

>[!NOTE]
>
>La suppression d’une liste fusionnée de son appartenance est identique à la suppression d’une piste d’une liste. Ouvrez le **Listes** , sélectionnez la liste qui contient la liste fusionnée, puis supprimez l’appartenance en cliquant sur le cercle rouge en regard de la liste.

### Affichage de pistes dans des listes {#viewing-leads-in-lists}

À tout moment, vous pouvez afficher les pistes qui appartiennent à une liste spécifique en naviguant ou en recherchant des membres.

Pour afficher les pistes dans les listes :

1. Dans le MCM, cliquez sur **Listes**.

1. Cochez la case en regard de la liste pour laquelle vous souhaitez afficher les membres.

1. Dans le **Outils** menu, sélectionnez **Afficher les pistes**. AEM affiche les pistes qui sont membres de cette liste. Vous pouvez parcourir la liste ou rechercher des membres.

   >[!NOTE]
   >
   >En outre, vous pouvez supprimer des pistes d’une liste en les sélectionnant, puis en cliquant sur **Supprimer l’appartenance**.

   ![screen_shot_2012-02-21at10828pm](assets/screen_shot_2012-02-21at10828pm.png)

1. Cliquez sur **Fermer** pour revenir au MCM.
