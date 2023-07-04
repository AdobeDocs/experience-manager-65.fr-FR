---
title: Participation aux workflows
description: Les workflows incluent généralement des étapes qui nécessitent qu’une personne effectue une activité sur une page ou une ressource. Le workflow sélectionne un utilisateur, une utilisatrice ou un groupe pour exécuter l’activité et affecte une tâche à cette personne ou à ce groupe.
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: ht
source-wordcount: '543'
ht-degree: 100%

---

# Participation aux workflows{#participating-in-workflows}

Les workflows incluent généralement des étapes qui nécessitent qu’une personne effectue une activité sur une page ou une ressource. Le workflow sélectionne un utilisateur, une utilisatrice ou un groupe pour exécuter l’activité et affecte une tâche à cette personne ou à ce groupe.

## Traitement des éléments de travail {#processing-your-work-items}

Vous pouvez effectuer les actions suivantes pour traiter un élément de travail :

* **Terminé**

   Vous pouvez terminer un élément pour permettre au workflow de passer à l’étape suivante.

* **Déléguer**

   Si une étape vous a été affectée, mais que vous ne pouvez pas effectuer d’action pour une raison quelconque, vous pouvez la déléguer à un autre utilisateur, une autre utilisatrice ou à un autre groupe.

   Les utilisateurs et les utilisatrices pouvant faire l’objet d’une délégation dépendent de la personne à qui l’élément de travail a été affecté :

   * Si l’élément de travail a été affecté à un groupe, les membres du groupe sont disponibles.
   * Si l’élément de travail a été attribué à un groupe puis délégué à un utilisateur, les membres du groupe et le groupe sont disponibles.
   * Si l’élément de travail a été attribué à un utilisateur unique, l’élément de travail ne peut pas être délégué.

* **Revenir en arrière**

   Si vous découvrez qu’une étape, ou une série d’étapes, doit être répétée, vous pouvez revenir à une étape antérieure. Cela vous permet de sélectionner une étape qui s’est produite plus tôt dans le workflow pour la traiter à nouveau. Le workflow revient à l’étape que vous spécifiez, puis continue à partir de là.

## Participation à un workflow {#participating-in-a-workflow}

### Notifications d’actions de workflow affectées {#notifications-of-assigned-workflow-actions}

Lorsqu’une tâche vous est attribuée (par exemple, **Approuver le contenu**), diverses alertes et/ou notifications s’affichent :

* La colonne **Statut** de la console Sites web indique quand une page se trouve dans un workflow :

   ![workflowstatus-1](assets/workflowstatus-1.png)

* Lorsque vous ou un groupe auquel vous appartenez vous voyez attribuer un élément de travail dans le cadre d’un workflow, l’élément de travail apparaît dans votre boîte de réception Workflow AEM.

   ![workflowinbox](assets/workflowinbox.png)

### Réalisation d’une étape de participant {#completing-a-participant-step}

Une fois que vous avez exécuté l’action indiquée, vous pouvez terminer l’élément de travail, ce qui permet au workflow de continuer. Utilisez la procédure suivante pour terminer l’élément de travail :

1. Sélectionnez l’étape du workflow et cliquez sur le bouton **Terminer** dans la barre de navigation supérieure.
1. Dans la boîte de dialogue qui s’affiche, sélectionnez l’option **Étape suivante** ; c’est-à-dire l’étape à exécuter ensuite. Une liste déroulante affiche toutes les destinations appropriées. Un **Commentaire** peut également être saisi.

   ![workflowcomplete](assets/workflowcomplete.png)

   Le nombre d’étapes répertoriées dépend de la conception du modèle de workflow.

1. Cliquez sur **OK** pour confirmer l’action.

### Délégation d’une étape de participant {#delegating-a-participant-step}

Pour déléguer un élément de travail, procédez comme suit.

1. Cliquez sur le bouton **Déléguer** dans la barre de navigation supérieure.
1. Dans la boîte de dialogue, utilisez la liste déroulante pour sélectionner la variable **Utilisateur** auquel déléguer l’élément de travail. Vous pouvez également ajouter un **Commentaire**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. Cliquez sur **OK** pour confirmer l’action.

### Revenir d’une étape de participant en arrière {#performing-step-back-on-a-participant-step}

Procédez comme suit pour revenir en arrière.

1. Cliquez sur le bouton Revenir en arrière dans la barre de navigation supérieure.
1. Dans la boîte de dialogue qui s’affiche, sélectionnez l’étape précédente ; en d’autres termes, l’étape à exécuter ensuite, même s’il s’agit d’une étape qui se produit plus tôt dans le workflow. Une liste déroulante affiche toutes les destinations appropriées.

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. Cliquez sur OK pour confirmer l’action.
