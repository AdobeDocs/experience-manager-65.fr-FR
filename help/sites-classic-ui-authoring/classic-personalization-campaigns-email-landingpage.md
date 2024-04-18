---
title: Création d’une page de destination efficace pour une newsletter
description: Une page de destination efficace pour newsletter vous permet d’obtenir plus de personnes inscrites à votre newsletter (ou à toute autre campagne de marketing par e-mail). Vous pouvez utiliser les informations que vous collectez à partir des abonnements à vos newsletters pour obtenir des prospects.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: c2fbf858-8815-426e-a2e5-f92bcf909ad0
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 100%

---

# Création d’une page de destination efficace pour une newsletter{#creating-an-effective-newsletter-landing-page}

Une page de destination efficace pour newsletter vous permet d’obtenir plus de personnes inscrites à votre newsletter (ou à toute autre campagne de marketing par e-mail). Vous pouvez utiliser les informations que vous collectez à partir des abonnements à vos newsletters pour obtenir des prospects.

Pour créer une page de destination efficace pour une newsletter, vous devez effectuer les opérations suivantes :

1. Créez une liste pour la newsletter afin que les utilisateurs et les utilisatrices puissent s’y abonner.
1. Créez le formulaire d’inscription. Pour ce faire, ajoutez une étape de workflow qui ajoute automatiquement la personne qui s’inscrit à la newsletter à votre liste de prospects.
1. Créez une page de confirmation qui remercie les utilisateurs et les utilisatrices pour leur inscription et leur accorde éventuellement une réduction.
1. Ajoutez des teasers.

>[!NOTE]
>
>Adobe ne prévoit pas d’optimiser cette fonctionnalité (Gestion des prospects et des listes).
>Il est conseillé d’utiliser [Adobe Campaign et l’intégration à AEM](/help/sites-administering/campaign.md).

## Créer une liste pour la newsletter {#creating-a-list-for-the-newsletter}

Créez une liste, par exemple, **Newsletter Geometrixx**, dans MCM pour la newsletter à laquelle les utilisateurs et les utilisatrices doivent s’abonner. La création de listes est décrite dans la section [Création de listes](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists). 

Voici un exemple de liste :

![mcm_listcreate](assets/mcm_listcreate.png)

## Créer un formulaire d’inscription {#create-a-sign-up-form}

Créez un formulaire d’inscription à la newsletter qui permet aux utilisateurs et aux utilisatrices de s’abonner aux balises. L’exemple de site web de Geometrixx fournit une page de newsletter dans la barre d’outils de Geometrixx où vous pouvez créer votre formulaire.

Pour créer votre propre formulaire de newsletter, reportez-vous aux informations sur la création de formulaires dans la [documentation sur Forms](/help/sites-authoring/default-components.md#form). La newsletter utilise les balises de la bibliothèque de balises. Pour ajouter des balises supplémentaires, reportez-vous à la section [Administration des balises](/help/sites-authoring/tags.md#tagadministration).

Les champs masqués de l’exemple suivant fournissent le minimum d’informations (e-mail). De plus, vous pourrez ajouter d’autres champs ultérieurement, mais cela aura une incidence sur le taux de conversion.

L’exemple suivant est un formulaire créé à l’adresse URL https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html.

1. Créez le formulaire.

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. Cliquez sur **Modifier** dans le composant de formulaire pour configurer le formulaire d’une page de remerciement (reportez-vous à la section [Création de pages de remerciement](#creating-a-thank-you-page)).

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. Définissez l’action de formulaire (ce qui se passe lorsque vous envoyez le formulaire) et configurez le groupe pour affecter les utilisateurs inscrits à la liste que vous avez créée précédemment (par exemple, geometrixx-newsletter).

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### Créer une page de remerciement {#creating-a-thank-you-page}

Lorsque les utilisateurs et les utilisatrices cliquent sur **S’abonner maintenant**, vous pouvez mettre en place une page de remerciement qui s’ouvre automatiquement. Créez la page de remerciement dans la page Newsletter Geometrixx. Après avoir créé le formulaire Newsletter, modifiez le composant Formulaire et ajoutez le chemin d’accès à la page de remerciement.

Envoyer une requête conduit l’utilisateur ou l’utilisatrice à une page de **remerciement** après laquelle il ou elle recevra un e-mail. Cette page de remerciement a été créée sous /content/geometrixx/en/toolbar/newsletter/thank_you.

![mcm_newsletter_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### Ajout de teasers {#adding-teasers}

Ajoutez des [teasers](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) pour cibler des audiences spécifiques. Par exemple, vous pouvez ajouter des teasers aux pages de remerciement et d’inscription à la newsletter.

Pour ajouter des teasers afin de créer une page de destination efficace pour newsletter :

1. Créez un paragraphe de teaser pour un cadeau d’inscription. Sélectionnez **First** comme stratégie et ajoutez un texte sur le cadeau offert.

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. Créez un paragraphe de teaser pour la page de remerciement. Sélectionnez **First** comme stratégie et ajoutez un texte qui informe l’utilisateur ou l’utilisatrice que son cadeau arrive.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. Créez une campagne avec les deux teasers : étiquetez l’un avec entreprise et laissez l’autre sans étiquette.

### Envoi de contenu aux personnes abonnées {#pushing-content-to-subscribers}

Envoyez les modifications apportées aux pages par le biais de la fonctionnalité Newsletter dans le MCM. Vous pouvez ensuite envoyer du contenu mis à jour aux personnes abonnées.

Voir [Envoi de newsletters](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters).
