---
title: Utiliser un formulaire adaptatif dans l’espace de travail HTML
description: Découvrez comment utiliser un formulaire adaptatif dans l’espace de travail HTML qui permet aux personnes de terrain d’accéder au formulaire sur leurs appareils.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 100%

---

# Utilisation d’un formulaire adaptatif dans l’espace de travail HTML{#using-an-adaptive-form-in-html-workspace}

AEM Forms sur JEE offre la possibilité d’utiliser un formulaire adaptatif dans l’espace de travail HTML.

Comme il est possible de sélectionner un XDP pendant la conception du processus, la possibilité de parcourir à partir d’un référentiel AEM de formulaire adaptatif existant a été ajoutée. Cette fonctionnalité donne au concepteur de processus la possibilité de configurer un formulaire adaptatif au point de départ ainsi que dans la tâche.

## Expérience de conception de processus {#process-design-experience}

Pour activer l’utilisation des formulaires adaptatifs dans la conception de processus, procédez comme suit :

* Dans Attribuer une tâche et Point de départ, vous pouvez accéder à une ressource de formulaire adaptatif dans le référentiel CRX lors de l’attribution d’une ressource de formulaire à une tâche.
* Dans la feuille de propriétés Attribuer une tâche/Point de départ Workbench, vous pouvez masquer la barre d’outils supérieure/globale d’un formulaire adaptatif.
* Vous pouvez utiliser de nouveaux profils d’action pour les actions de rendu et d’envoi dans les formulaires adaptatifs.

### Exportation et importation d’applications LiveCycle {#livecycle-application-export-and-import}

Comme les formulaires adaptatifs se trouvent dans le référentiel AEM, l’exportation d’applications LiveCycle contient uniquement les références des formulaires adaptatifs utilisés. Par conséquent, l’exportation et l’importation de l’application LiveCycle est un processus en deux étapes. L’application de LiveCycle comprend des définitions de processus, etc. Un package distinct contenant des formulaires adaptatifs est exporté sous la forme d’un fichier ZIP à partir d’AEM. Lors de l’importation, l’application LiveCycle est importée via Workbench et les formulaires adaptatifs sont importés via AEM.

## Expérience utilisateur du formulaire adaptatif dans l’espace de travail HTML {#user-experience-of-adaptive-form-in-html-workspace}

L’espace de travail HTML fournit des contrôles spécifiques aux formulaires adaptatifs en plus des contrôles disponibles pour les formulaires mobiles. Un utilisateur ou une utilisatrice peut ajouter des pièces jointes, enregistrer, signer, envoyer et parcourir les formulaires adaptatifs dans l’espace de travail HTML lorsque l’utilisateur ou utilisatrice ouvre une tâche ou un point de départ. Procédez comme suit :

1. Pour joindre des fichiers, utilisez Pièces jointes de la tâche, comme dans Mobile Forms. Le bouton Tout type de fichier de pièce jointe du formulaire adaptatif est masqué.

1. Pour enregistrer un formulaire adaptatif, cliquez sur **Enregistrer**, comme dans Mobile Forms. Le bouton Tout type d’enregistrement du formulaire adaptatif est masqué.

1. Pour envoyer un formulaire adaptatif, utilisez le bouton **Envoyer** ou les actions d’itinéraire disponibles, comme dans Mobile Forms. Le bouton Tout type d’envoi du formulaire adaptatif est masqué.

1. **Visibilité de la barre d’outils globale des formulaires adaptatifs** : si le concepteur du processus masque la barre d’outils globale/supérieure, la barre d’outils et les boutons n’apparaissent pas sur les formulaires adaptatifs.

1. **Contrôles de navigation de l’espace de travail pour les formulaires adaptatifs** : les boutons Suivant/Précédent sont disponibles ainsi que les boutons Enregistrer, Envoyer et Acheminer l’action pour un formulaire adaptatif dans l’espace de travail HTML. Cliquez sur les boutons Suivant/Précédent pour parcourir les panneaux des formulaires adaptatifs dans l’espace de travail HTML. Les boutons Suivant/Précédent offrent une navigation approfondie et sont similaires aux commandes de navigation de la vue mobile des formulaires adaptatifs.

1. **eSign et le composant Résumé du formulaire adaptatif** : le composant Résumé n’est pas opérationnel dans l’espace de travail HTML. En d’autres termes, si un formulaire adaptatif comporte un composant Résumé, il n’est pas visible dans l’espace de travail. Au lieu de l’envoi automatique dans le composant E-sign, l’utilisateur ou l’utilisatrice de l’espace de travail clique sur Envoyer ou sur une action d’acheminement dans l’espace de travail HTML. Une fois le document signé, il est visible sous la forme d’un document signé aplati. Cliquez sur **Envoyer** ou une action d’acheminement permettant de fermer/terminer la tâche ou le point de départ.\
   Le document signé est récupéré à partir du serveur de services eSign et le fichier XML de données est transféré vers l’étape suivante du processus.

## Cette procédure explique comment utiliser les formulaires adaptatifs dans la conception du processus {#steps-to-use-adaptive-forms-in-process-design}

1. Ouvrez Adobe Experience Manager Forms Workbench.

1. Accédez à **Fichier > Nouveau > Application** ou utilisez l’application existante pour créer une application.

   ![Création d’une nouvelle application](assets/create_new_appl.png)

   Création d’une application

1. Créez un processus ou utilisez un processus existant dans l’application.

   ![Création d’un nouveau processus](assets/create_new_process.png)

   Création d’un processus

1. Créez un point de départ ou affectez une tâche et double-cliquez dessus.
1. Dans la section **[!UICONTROL Présentation et Données]**, sélectionnez **[!UICONTROL Utilisez un actif CRX]** et cliquez sur les points de suspension situés avant l’actif.

   ![Utilisation d’un actif CRX](assets/use_crx_asset.png)

   Utilisation d’un actif CRX

1. Sélectionnez le formulaire adaptatif créé via l’interface utilisateur de gestion des ressources, puis cliquez sur **[!UICONTROL OK]**.

   ![Sélection d’un formulaire adaptatif](assets/selecting_form.png)

   Sélection d’un formulaire adaptatif

   >[!NOTE]
   >
   >Pour en savoir plus sur la création d’un formulaire adaptatif, consultez [Création d’un formulaire adaptatif](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Pour plus dʼinformations sur la création de processus, consultez la section [Créer et gérer des processus](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
