---
title: Création d’expériences ciblées dans AEM Forms
seo-title: Création d’expériences ciblées dans AEM Forms
description: L’utilisation de Target dans AEM Forms permet de créer des expériences personnalisées pour les clients ciblés.
seo-description: L’utilisation de Target dans AEM Forms permet de créer des expériences personnalisées pour les clients ciblés.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30

---


# Création d’expériences ciblées dans AEM Forms {#create-targeted-experiences-in-aem-forms}

## Integrate Adobe Target with AEM Forms {#integrate-adobe-target-with-aem-forms}

Adobe Target intégré à AEM vous permet de créer des expériences personnalisées pour un public cible. Avec Adobe Target, vous pouvez créer des tests A/B, mesurer les réponses des utilisateurs et générer du contenu web personnalisé pour les utilisateurs ciblés. Vous pouvez intégrer Adobe Target à AEM Forms pour cibler les composants image des formulaires adaptatifs et des communications interactives.

Configurez Adobe Target dans AEM pour l’utiliser avec les formulaires adaptatifs et les communications interactives, reportez-vous à la page [Création d’une configuration Target dans AEM](/help/sites-administering/target.md) et [Ajout d’une structure](/help/sites-administering/target.md).

>[!NOTE]
>
>Le ciblage fonctionne lorsque le formulaire adaptatif ou la communication interactive est rendu à l’aide d’un nom d’hôte ou d’une adresse IP. Elle échoue lorsque le formulaire adaptatif ou la communication interactive est rendu à l’aide de localhost.

## Création d’une activité Target {#creating-a-target-activity}

1. Tap **Adobe Experience Manager > Personalization > Activities**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. In the Activities page, tap **Create > Create Brand**.
1. Vous êtes invité à choisir un modèle et à entrer des propriétés.

   Select a template, tap **Next.** Entrez le titre de votre marque dans la section Propriétés, puis appuyez sur **Créer.**
Votre identité visuelle est désormais répertoriée dans la page Activités.

1. Appuyez sur la marque dans la page Activités.
1. In Master Area of your brand, tap **Create** > **Create Activity**.

   Lorsque vous créez une activité, vous spécifiez ses détails, cible et paramètres.

   La section Détails inclut un nom, un moteur de ciblage et un objectif. Lorsque vous sélectionnez Adobe Target comme moteur de ciblage, l’option de configuration cloud de Target est activée. Choose your Target cloud configuration, choose Activity type, provide the objective of the activity, and tap **Next**. Interactive Communication ne prend en charge que le type d’activité de ciblage d’expérience.

   La section Cible vous permet d’ajouter une expérience de public et de la nommer. Click **Add Experience** to enable the **Select Audience** and **Name Experience** options. Tap **Select Audience** to see a list of audiences and their source. Choisissez un public dans la liste Nom du public. Tap **Add Experience** to name the experience, and tap **Next**.

   La section Objectifs et paramètres vous permet de planifier votre activité et de la classer par priorité. Set the start date, end date, and priority of the activity, goal metric, additional metric and tap **Save**.

   L’activité est désormais répertoriée dans votre page de marque.

   >[!NOTE]
   >
   >Vous pouvez ignorer l’erreur &quot;Votre activité a été enregistrée mais n’a pas été synchronisée avec Target. Raison : L’expérience suivante n’a aucune offre&quot;, si elle est rencontrée lors de l’enregistrement de l’activité.

1. Pour activer target, modifiez le fichier .jsp afin d’inclure les bibliothèques client utilisées par votre modèle de formulaires adaptatifs.

   For example, in the out-of-the-box implementation, click **Tools** >  **CRXDE Lite**.

   Dans la barre d’adresse de CRXDE Lite, saisissez /libs/fd/af/components/page/base/head.jsp pour modifier le fichier head.jsp.

   Cette implémentation utilise le modèle simpleEnrollment. Dans cette implémentation, modifiez le fichier head.jsp pour inclure les bibliothèques client suivantes :

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Pour activer la structure cible pour les formulaires adaptatifs, accédez au formulaire ou à la communication interactive, puis ouvrez-le en mode d’édition.

   To open a form or interactive communication in edit mode, tap **Select** and then tap **Open**.

   Vous pouvez également afficher quatre boutons lorsque vous déplacez le pointeur sur le formulaire ou l’icône de communication interactive sans le sélectionner. You can tap the **Edit** button that appears, to open the form in edit mode.

1. In the page toolbar, tap **Page Information** ![theme-options](assets/theme-options.png) > **Open Properties**.
1. Dans l’onglet Général, choisissez une configuration pour le champ **Adobe Target** . Tap **Save &amp; Close**.

## Application de l’activité créée à une image de formulaire adaptatif ou à une image de communication interactive {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Ouvrez le formulaire adaptatif et la communication interactive pour le modifier. Si vous ouvrez une communication interactive, ouvrez le canal Web.

1. Dans le mode de création de votre communication interactive ou de votre formulaire adaptatif, ajoutez une image à cibler.

   >[!NOTE]
   >
   >AEM Forms prend en charge le ciblage uniquement des composants d’image. Assurez-vous que le panneau qui héberge le composant d’image ne contient aucun autre composant et que le nombre de colonnes du panneau est défini sur 1.

1. Passez du mode **Modifier** au mode **Ciblage** . L’option permettant de changer de mode se trouve dans le coin supérieur droit.
1. Sélectionnez une **MARQUE**, sélectionnez **ACTIVITÉ** et appuyez sur **Démarrer le ciblage**. Le menu **Audiences** s’affiche sur le côté droit de l’éditeur.

   ![ciblage-menu](assets/targeting-menu.png)

1. Sélectionnez un public dans le menu **Audiences** et appuyez sur l’image à cibler. Un menu s&#39;affiche. Dans le menu, appuyez sur **Target**. Appuyez sur l’image et appuyez sur **Configurer**. Dans la fenêtre de propriétés, sélectionnez l’image à afficher pour le public sélectionné. Répétez l’étape pour toutes les audiences. Le ciblage d’expérience est activé pour l’image dans la communication interactive ou le formulaire adaptatif.

## Vérifier si l’activité créée est synchronisée avec le serveur cible {#check-if-the-created-activity-syncs-with-the-target-server}

Une activité utilisée pour le ciblage est synchronisée avec le serveur cible. Pour vérifier si votre activité est synchronisée avec le serveur cible, vérifiez l’état de votre activité dans votre page de marque.

Assurez-vous que l’état de l’activité est Synchronisé.

## Valider le comportement Cible {#validate-target-behavior}

Pour valider le comportement Cible :

* Use targeting with `wcmmode preview` in the author mode
* Utiliser le ciblage avec `wcmmode preview` et `wcmmode disabled` en mode de publication

## Contrôler le ciblage pour le composant image {#monitor-targeting-for-the-image-component}

Pour contrôler le ciblage pour les composants image sur votre formulaire, publiez vos images, activités et formulaire adaptatif.

## Problèmes en cours {#open-issues}

Expression de visibilité, la définition de la cible d’action échoue pour les images ciblées dans les formulaires adaptatifs.
