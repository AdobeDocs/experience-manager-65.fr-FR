---
title: Utilisation des modèles de courrier électronique personnalisés dans une étape Affecter une tâche
description: Modèles de courrier électronique personnalisés pour les notifications par courrier électronique de processus de formulaires
topic-tags: publish
docset: aem65
exl-id: d4035c91-ee8d-4f12-bdac-e3912be732d7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 38%

---

# Utilisation des modèles de courrier électronique personnalisés dans une étape Affecter une tâche{#use-custom-email-templates-in-an-assign-task-step}

Vous pouvez utiliser l’étape Affecter une tâche pour créer et affecter des tâches à un utilisateur ou à un groupe. Lorsqu’une tâche est assignée à un utilisateur ou à un groupe, une notification est envoyée par e-mail à l’utilisateur défini ou à chaque membre du groupe défini. Une notification électronique type contient le lien de la tâche affectée et des informations relatives à la tâche. L’image suivante présente un exemple de notification électronique :

![Notification électronique avec modèle prêt à l’emploi](do-not-localize/default_email_template_new.png)

Vous pouvez personnaliser l’apparence et utiliser des métadonnées personnalisées dans une notification électronique. AEM Forms fournit un modèle prêt à l’emploi pour les notifications électroniques. Vous pouvez personnaliser le modèle prêt à l’emploi ou créer un modèle entièrement nouveau.

Les modèles de notification électronique reposent sur la variable [Email HTML](https://en.wikipedia.org/wiki/HTML_email). Ces emails s’adaptent à différents clients de messagerie et tailles d’écran. De plus, le style de l&#39;email est défini dans le modèle.

L’image suivante affiche une notification électronique personnalisée :

![Notification électronique à l’aide du modèle personnalisé](do-not-localize/customized-email.png)

## Personnaliser le modèle existant {#customize-the-existing-template}

AEM Forms fournit un modèle prêt à l’emploi pour les notifications par courrier électronique. Le modèle fournit la description du titre, l’échéance, la priorité, le nom du workflow et le lien de la tâche affectée. Vous pouvez personnaliser le modèle pour modifier l’aspect. Effectuez les étapes suivantes pour personnaliser le modèle :

1. Connectez-vous à CRXDE avec le compte administrateur.

1. Accédez à /libs/fd/dashboard/templates/email.

1. Ouvrez le fichier htmlEmailTemplate.txt. Il contient le modèle par défaut.

1. Remplacez le contenu du fichier htmlEmailTemplate.txt par un contenu personnalisé.

   Un modèle de notification électronique est un [courrier électronique HTML](https://en.wikipedia.org/wiki/HTML_email). Vous pouvez remplacer le code HTML existant par votre code personnalisé pour modifier l’aspect du modèle.

1. Enregistrez le fichier. Désormais, le modèle personnalisé est opérationnel.

## Création d’un modèle de courrier électronique {#create-an-email-template}

AEM Forms fournit un modèle prêt à l’emploi pour les notifications par courrier électronique. Le modèle fournit la description du titre, l’échéance, la priorité, le nom du workflow et le lien de la tâche affectée. Vous pouvez également ajouter un modèle de courrier électronique personnalisé (votre propre modèle) pour les étapes Affecter une tâche. Effectuez les étapes suivantes pour ajouter un modèle de courrier électronique personnalisé :

1. Connectez-vous à CRXDE avec le compte administrateur.

1. Accédez à /libs/fd/dashboard/templates/email.

1. Créez un fichier .txt. Par exemple, EmailOnTaskAssign.txt.

1. Ajoutez le code HTML personnalisé au fichier.

   Un modèle de notification électronique est un [courrier électronique HTML](https://en.wikipedia.org/wiki/HTML_email). Vous pouvez ajouter du code de HTML personnalisé au fichier pour créer un modèle.

1. Enregistrez le fichier. Le modèle est prêt à être utilisé dans l’étape Affecter une tâche.

## Utilisation d’un modèle de courrier électronique dans une étape Affecter une tâche {#use-an-email-template-in-an-assign-task-step}

L’étape Affecter une tâche prête à l’emploi est configurée pour utiliser le modèle par défaut, htmlEmailTemplate.txt. Vous pouvez choisir d’utiliser un modèle personnalisé. Pour modifier le modèle :

1. Ouvrez l’étape Affecter une tâche.

1. Accédez à Personne désignée > Modèle de courrier électronique HTML.

1. Sélectionnez le modèle de courrier électronique HTML nouvellement créé.

1. Cliquez sur OK. Le modèle est modifié.

Une notification électronique utilise également [metadata](../../forms/using/use-metadata-in-email-notifications.md). Par exemple, date d’échéance, priorité, nom du workflow, etc. Vous pouvez également configurer le modèle pour utiliser des [métadonnées personnalisées](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification).
