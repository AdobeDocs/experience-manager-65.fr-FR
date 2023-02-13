---
title: Utiliser un formulaire adaptatif dans l’espace de travail HTML
seo-title: Using an adaptive form in HTML Workspace
description: Utiliser un formulaire adaptatif dans l’espace de travail HTML
seo-description: Using an adaptive form in HTML Workspace
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '691'
ht-degree: 100%

---

# Utiliser un formulaire adaptatif dans l’espace de travail HTML{#using-an-adaptive-form-in-html-workspace}

AEM Forms sur JEE offre la possibilité d’utiliser un formulaire adaptatif dans l’espace de travail HTML.

Comme il est possible de sélectionner un XDP pendant la conception du processus, la possibilité de parcourir à partir d’un référentiel AEM de formulaire adaptatif existant a été ajoutée. Cette fonctionnalité donne au concepteur du processus la possibilité de configurer un formulaire adaptatif au point de départ ainsi que dans la tâche.

## Expérience de conception de processus {#process-design-experience}

Effectuez les opérations suivantes pour activer l’utilisation des formulaires adaptatifs dans la conception du processus :

* Dans Assign Task et Point de départ, vous pouvez rechercher une ressource de formulaire adaptatif dans le référentiel CRX lorsque vous affectez une ressource de formulaire à une tâche.
* Dans Assign Task ou dans la feuille de propriétés Workbench du Point de départ, vous pouvez masquer la barre d’outils supérieure/globale d’un formulaire adaptatif.
* Vous pouvez utiliser les nouveaux profils d’action pour les actions de rendu et d’envoi des formulaires adaptatifs.

### Exportation et importation d’applications LiveCycle {#livecycle-application-export-and-import}

Les formulaires adaptatifs étant situés dans le référentiel AEM, l’exportation d’applications LiveCycle contient uniquement les références des formulaires adaptatifs utilisés. Par conséquent, l’exportation et l’importation de l’application LiveCycle est un processus en deux étapes. L’application LiveCycle comprend des définitions de processus, etc. Un module distinct contenant les formulaires adaptatifs est exporté au format ZIP à partir d’AEM. Lors de l’importation, l’application LiveCycle est importée par Workbench et les formulaires adaptatifs sont importés par AEM.

## Expérience utilisateur de formulaire adaptatif dans Workspace HTML {#user-experience-of-adaptive-form-in-html-workspace}

Workspace HTML fournit quelques fonctions spécifiques aux formulaires adaptatifs en plus des fonctions disponibles pour les formulaires mobiles. L’utilisateur peut ajouter des pièces jointes, enregistrer, signer, envoyer et parcourir les formulaires adaptatifs dans Workspace HTML en ouvrant une tâche ou un point de départ. Voici les caractéristiques :

1. Pour joindre des fichiers, utilisez Pièces jointes de la tâche, comme dans Mobile Forms. Le bouton Tout type de fichier de pièce jointe du formulaire adaptatif est masqué.

1. Pour enregistrer un formulaire adaptatif, cliquez sur **Enregistrer**, comme dans Mobile Forms. Le bouton Tout type d’enregistrement du formulaire adaptatif est masqué.

1. Pour envoyer un formulaire adaptatif, utilisez le bouton **Envoyer** ou les actions d’itinéraire disponibles, comme dans Mobile Forms. Le bouton Tout type d’envoi du formulaire adaptatif est masqué.

1. **Visibilité de la barre d’outils globale des formulaires adaptatifs** : si le concepteur du processus masque la barre d’outils globale/du niveau supérieur, la barre d’outils et les boutons n’apparaissent pas sur les formulaires adaptatifs.

1. **Contrôles de navigation de l’espace de travail pour les formulaires adaptatifs** : les boutons Suivant/Précédent sont disponibles ainsi que les boutons Enregistrer, Envoyer et Acheminer l’action pour un formulaire adaptatif dans l’espace de travail HTML. Cliquez sur les boutons Suivant/Précédent pour parcourir les panneaux des formulaires adaptatifs dans Workspace HTML. Les boutons Suivant/Précédent offrent une navigation approfondie et sont similaires aux commandes de navigation de la vue mobile des formulaires adaptatifs.

1. **eSign et le composant Résumé du formulaire adaptatif** : le composant Résumé n’est pas opérationnel dans l’espace de travail HTML. En d’autres termes, si un formulaire adaptatif possède un composant Résumé, il n’est pas visible dans l’espace de travail. Au lieu de cliquer sur Envoi automatique dans le composant Esign, l’utilisateur de l’espace de travail clique sur Envoyer ou sur une action d’itinéraire dans Workspace HTML. Une fois le document signé, il s’affiche en tant que document signé aplati. Cliquez sur **Envoyer** ou sur une action d’itinéraire pour fermer/terminer la tâche ou sur Point de départ.\
   Le document signé est récupéré à partir du serveur de services eSign et le fichier XML de données est transféré vers l’étape suivante du processus.

## Cette procédure explique comment utiliser les formulaires adaptatifs dans la conception du processus {#steps-to-use-adaptive-forms-in-process-design}

1. Ouvrez Adobe Experience Manager Forms Workbench.

1. Accédez à **Fichier > Nouveau > Application** ou utilisez l’application existante pour créer une application.

   ![Création d’une nouvelle application](assets/create_new_appl.png)

   Création d’une nouvelle application

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
   >Pour en savoir plus sur la création d’un formulaire adaptatif, consultez la section [Création d’un formulaire adaptatif](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Pour plus dʼinformations sur la création de processus, consultez la section [Créer et gérer des processus](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
