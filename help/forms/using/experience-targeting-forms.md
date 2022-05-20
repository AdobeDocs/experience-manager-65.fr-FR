---
title: Création d’expériences ciblées dans AEM Forms
seo-title: Create targeted experiences in AEM Forms
description: L’utilisation de Target dans AEM Forms permet de créer des expériences personnalisées pour les clients ciblés.
seo-description: Use Target in AEM Forms to create customized experiences for targeted customers.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '838'
ht-degree: 100%

---

# Création d’expériences ciblées dans AEM Forms {#create-targeted-experiences-in-aem-forms}

## Intégrer Adobe Target à AEM Forms {#integrate-adobe-target-with-aem-forms}

Adobe Target intégré à AEM vous permet de créer des expériences personnalisées pour un public cible. Avec Adobe Target, vous pouvez créer des tests A/B, mesurer les réponses des utilisateurs et générer du contenu web personnalisé pour les utilisateurs ciblés. Vous pouvez intégrer Adobe Target à AEM Forms pour cibler les composants image des formulaires adaptatifs et des communications interactives.

Configurez Adobe Target dans AEM pour l’utiliser avec les formulaires adaptatifs et les communications interactives. Voir [Créer une configuration Target dans AEM](/help/sites-administering/target.md) et [Ajouter un framework](/help/sites-administering/target.md).

>[!NOTE]
>
>Le ciblage fonctionne lorsque votre formulaire adaptatif ou communication interactive est rendu(e) en utilisant un nom d’hôte ou une adresse IP. Il échoue lorsque le formulaire adaptatif est rendu à l’aide de l’hôte local.

## Création d’une activité Target {#creating-a-target-activity}

1. Appuyez sur **Adobe Experience Manager > Personnalisation > Activités**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. Dans la page Activités, appuyez sur **Créer > Créer une marque**.
1. Vous êtes invité à choisir un modèle et à entrer des propriétés.

   Sélectionnez un modèle, puis appuyez sur **Suivant.** Saisissez le titre de votre marque dans la section Propriétés, puis appuyez sur **Créer.**
Votre identité visuelle est désormais répertoriée dans la page Activités.

1. Appuyez sur la marque dans la page Activités.
1. Dans la zone principale de votre marque, appuyez sur **Créer** > **Créer une activité**.

   Lorsque vous créez une activité, vous spécifiez ses détails, cible et paramètres.

   La section Détails inclut un nom, un moteur de ciblage et un objectif. Lorsque vous sélectionnez Adobe Target comme moteur de ciblage, l’option de configuration cloud de Target est activée. Sélectionnez la configuration cloud de Target, le type d’activité, puis indiquez l’objectif de l’activité et appuyez sur **Suivant**. La communication interactive ne prend en charge que le type d’activité de ciblage d’expérience.

   La section Cible vous permet d’ajouter une expérience de public et de la nommer. Cliquez sur **Ajouter une expérience** pour activer les options **Sélectionner un public** et **Nommer l’expérience**. Appuyez sur **Sélectionner un public** pour voir une liste de publics et leur source. Choisissez un public dans la liste Nom du public. Appuyez sur **Ajouter une expérience** pour nommer l’expérience, puis sur **Suivant**.

   La section Objectifs et paramètres vous permet de planifier votre activité et de la classer par priorité. Définissez la date de début, la date de fin et la priorité de l’activité, puis appuyez sur **Enregistrer**.

   L’activité est désormais répertoriée dans votre page de marque.

   >[!NOTE]
   >
   >Vous pouvez ignorer l’erreur « Votre activité a été enregistrée mais elle n’a pas été synchronisée avec Target. Motif : l’expérience suivante ne comporte aucune offre », si elle survient lors de l’enregistrement de l’activité.

1. Pour activer la cible, modifiez le fichier .jsp et incluez des bibliothèques client que votre modèle de formulaires adaptatifs utilise.

   Par exemple, dans l’implémentation prête à l’emploi, cliquez sur **Outils** > **CRXDE Lite**.

   Dans la barre d’adresse CRXDE Lite, saisissez /libs/fd/af/components/page/base/head.jsp pour modifier le fichier head.jsp.

   Cet implémentation utilise le modèle simpleEnrollment. Dans cette implémentation, modifiez le fichier head.jsp et incluez les bibliothèques client suivantes :

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Pour activer le framework cible pour les formulaires adaptatifs, accédez à votre formulaire et ouvrez-le en mode d’édition.

   Pour ouvrir un formulaire en mode d’édition, appuyez sur **Sélectionner**, puis sur **Ouvrir**.

   Quatre boutons apparaissent également lorsque vous placez le curseur sur l’icône du formulaire ou de la communication interactive sans faire de sélection. Vous pouvez appuyer sur le bouton **Modifier** qui s’affiche, afin d’ouvrir le formulaire en mode d’édition.

1. Dans la barre d’outils, appuyez sur **Informations sur la page** ![options de thème](assets/theme-options.png) > **Ouvrir les propriétés**.
1. Dans l’onglet Général, sélectionnez une configuration du champ **Adobe Target**. Appuyez sur **Enregistrer et fermer**.

## Appliquer une activité créée à une image de formulaire adaptatif ou à une image de communication interactive {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Ouvrez le formulaire adaptatif et la communication interactive à modifier. Si vous ouvrez une communication interactive, ouvrez le canal web.

1. Dans le mode de création de votre communication interactive ou de votre formulaire adaptatif, ajoutez une image à cibler.

   >[!NOTE]
   >
   >AEM Forms prend uniquement en charge le ciblage des composants d’image. Assurez-vous que le panneau qui héberge le composant d’image ne contient aucun autre composant et que le nombre de colonnes du panneau est défini sur 1.

1. Basculez de **Modifier** au mode **Ciblage**. L’option permettant de changer de mode se trouve dans le coin supérieur droit.
1. Sélectionnez une **MARQUE**, une **ACTIVITÉ**, puis appuyez sur **Commencer le ciblage**. Le menu **Publics** s’affiche sur le côté droit de l’éditeur.

   ![Menu de ciblage](assets/targeting-menu.png)

1. Sélectionnez un public dans le menu **Publics** et appuyez sur l’image à cibler. Un menu s’affiche. Dans le menu, appuyez sur **Cible**. Appuyez sur l’image, puis sur **Configurer**. Dans la fenêtre des propriétés, sélectionnez l’image à afficher pour le public sélectionné. Répétez l’étape pour toutes les audiences. Le ciblage d’expérience est activé pour l’image dans la communication interactive ou le formulaire adaptatif.

## Vérifier si l’activité créée est synchronisée avec le serveur cible {#check-if-the-created-activity-syncs-with-the-target-server}

Une activité utilisée pour le ciblage est synchronisée avec le serveur cible. Pour vérifier si votre activité est synchronisée avec le serveur cible, vérifiez l’état de votre activité dans votre page de marque.

Assurez-vous que l’état de l’activité est Synchronisé.

## Valider le comportement Cible {#validate-target-behavior}

Pour valider le comportement Cible :

* Utiliser le ciblage avec `wcmmode preview` en mode création
* Utiliser le ciblage avec `wcmmode preview` et `wcmmode disabled` en mode de publication

## Contrôler le ciblage pour le composant image {#monitor-targeting-for-the-image-component}

Pour contrôler le ciblage pour les composants image sur votre formulaire, publiez vos images, activités et formulaire adaptatif.

## Problèmes en cours {#open-issues}

Expression de visibilité, la définition de la cible d’action échoue pour les images ciblées dans les formulaires adaptatifs.
