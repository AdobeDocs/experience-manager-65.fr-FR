---
title: Utilisation des modèles de courrier électronique personnalisés dans une étape Affecter une tâche
seo-title: Utilisation des modèles de courrier électronique personnalisés dans une étape Affecter une tâche
description: 'Modèles de courrier électronique personnalisés pour les notifications électroniques de processus de formulaires '
seo-description: 'Modèles de courrier électronique personnalisés pour les notifications électroniques de processus de formulaires '
uuid: ba453d54-813f-4a4f-a82e-1a6a28b6939c
topic-tags: publish
discoiquuid: 2ad4b7b5-2162-4599-af3f-9476f1256de6
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# Utilisation des modèles de courrier électronique personnalisés dans une étape Affecter une tâche{#use-custom-email-templates-in-an-assign-task-step}

Vous pouvez utiliser l’étape Affecter une tâche pour créer et affecter des tâches à un utilisateur ou à un groupe. Lorsqu’une tâche est affectée à un utilisateur ou à un groupe, une notification électronique est envoyée à l’utilisateur défini ou à chaque membre du groupe défini. Une notification électronique contient généralement le lien de la tâche affectée et des informations relatives à la tâche. L’image suivante affiche un exemple de notification électronique :

![Notification électronique avec modèle prêt à l’emploi](do-not-localize/default_email_template_new.png)

Vous pouvez personnaliser l’apparence et utiliser des métadonnées personnalisées dans une notification électronique. AEM Forms fournit un modèle prêt à l’emploi pour les notifications électroniques. Vous pouvez personnaliser le modèle prêt à l’emploi ou créer un nouveau modèle à partir de zéro.

Les modèles de notification électronique sont basés sur les [courriers électroniques HTML](https://en.wikipedia.org/wiki/HTML_email). Ces courriers électroniques s’adaptent à différents clients de messagerie et tailles d’écran. De plus, le style de courrier électronique est défini dans le modèle.

L’image suivante affiche une notification électronique personnalisée :

![Notification électronique à l’aide du modèle personnalisé](do-not-localize/customized-email.png)

## Personnalisation du modèle existant {#customize-the-existing-template}

AEM Forms fournit un modèle prêt à l’emploi pour les notifications électroniques. Le modèle fournit la description du titre, l’expiration, la priorité, le nom du processus et le lien de la tâche affectée. Vous pouvez personnaliser le modèle afin de modifier l’aspect. Effectuez les étapes suivantes pour personnaliser le modèle :

1. Connectez-vous à CRXDE avec le compte administrateur.

1. Accédez à /libs/fd/dashboard/templates/email.

1. Ouvrez le fichier htmlEmailTemplate.txt. Il contient le modèle par défaut.

1. Remplacez le contenu du fichier htmlEmailTemplate.txt par un contenu personnalisé.

   Un modèle de notification électronique est un [courrier électronique HTML](https://en.wikipedia.org/wiki/HTML_email). Vous pouvez remplacer le code HTML existant par votre code personnalisé pour modifier l’aspect du modèle.

1. Enregistrez le fichier. Désormais, le modèle personnalisé est opérationnel.

## Création d’un modèle de courrier électronique {#create-an-email-template}

AEM Forms fournit un modèle prêt à l’emploi pour les notifications électroniques. Le modèle fournit la description du titre, l’expiration, la priorité, le nom du processus et le lien de la tâche affectée. Vous pouvez également ajouter un modèle de courrier électronique personnalisé (votre propre modèle) pour les étapes Affecter une tâche. Effectuez les étapes suivantes pour ajouter un modèle de courrier électronique personnalisé :

1. Connectez-vous à CRXDE avec le compte administrateur.

1. Accédez à /libs/fd/dashboard/templates/email.

1. Créez un fichier .txt. Par exemple, EmailOnTaskAssign.txt.

1. Ajoutez le code HTML personnalisé au fichier.

   Un modèle de notification électronique est un [courrier électronique HTML](https://en.wikipedia.org/wiki/HTML_email). Vous pouvez ajouter du code HTML personnalisé au fichier pour créer un nouveau modèle.

1. Enregistrez le fichier. Le modèle est prêt à être utilisé dans l’étape Affecter une tâche.

## Utilisation d’un modèle de courrier électronique dans une étape Affecter une tâche {#use-an-email-template-in-an-assign-task-step}

L’étape Affecter une tâche prête à l’emploi est configurée pour utiliser le modèle par défaut, htmlEmailTemplate.txt. Vous pouvez choisir d’utiliser un modèle personnalisé. Pour modifier le modèle :

1. Ouvrez l’étape Affecter une tâche.

1. Accédez à Personne désignée > Modèle de courrier électronique HTML.

1. Sélectionnez le modèle de courrier électronique HTML nouvellement créé.

1. Cliquez sur OK. Le modèle est modifié.

Une notification électronique utilise également des [métadonnées](../../forms/using/use-metadata-in-email-notifications.md). Par exemple, l’échéance, la priorité, le nom de processus, etc. Vous pouvez également configurer le modèle pour utiliser des [métadonnées personnalisées](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification).
