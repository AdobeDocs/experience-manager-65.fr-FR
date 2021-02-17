---
title: Créer et affecter des ressources d'activation
seo-title: Créer et affecter des ressources d'activation
description: Ressources d'activation des Ajoutes
seo-description: Ressources d'activation des Ajoutes
uuid: da940242-0c9b-4ad8-8880-61fd41461c3b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8fe97181-600e-42ac-af25-d5d4db248740
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 7%

---


# Créer et affecter des ressources d&#39;activation {#create-and-assign-enablement-resources}

## Ajouter une ressource d&#39;activation {#add-an-enablement-resource}

Pour ajouter une ressource d’activation au nouveau site de la communauté :

* Connectez-vous en tant qu’administrateur système sur l’instance d’auteur :
   * Par exemple, [http://localhost:4502/](http://localhost:4503/)
* Dans la navigation globale, sélectionnez **[!UICONTROL Communautés]** > **[!UICONTROL Ressources]**

   ![resources](assets/resources.png)

   ![activation-ressource](assets/enablement-resource.png)
* Sélectionnez le site de la communauté sur lequel les ressources d&#39;activation sont ajoutées :
   * Sélectionnez **[!UICONTROL Didacticiel d’activation]**.
* Dans le menu, sélectionnez **[!UICONTROL Créer]**.
* Sélectionnez **[!UICONTROL Ressource]**.

![create-resource](assets/create-enablement-resource.png)

### Informations de base {#basic-info}

Renseignez les informations de base de la ressource :

* **[!UICONTROL Nom du site]**

   Définissez sur le nom du site communautaire sélectionné : Didacticiel d’activation

* **[!UICONTROL Nom et diffusion de la ressource ;]**

   Leçon de ski 1

* **[!UICONTROL Balises]**

   Didacticiel : Sports / Ski

* **[!UICONTROL Afficher dans le catalogue]**

   Définissez-la sur **On**.

* **[!UICONTROL Description]**

   Faire glisser sur la neige pour les débutants.

* **[!UICONTROL Ajouter image]**

   Ajoutez une image pour représenter la Ressource au membre dans sa vue Affectations.

   ![basic-info](assets/basic-info.png)

* Sélectionnez **[!UICONTROL Suivant]**

### Ajouter du contenu {#add-content}

Bien qu&#39;il semble que plusieurs ressources puissent être sélectionnées, une seule est autorisée.

Sélectionnez `'+' icon`, dans le coin supérieur droit, pour commencer le processus de sélection de la ressource en identifiant la source.

![ajouter du contenu](assets/add-content.png)

![upload-resource](assets/upload-resource.png)

Téléchargez une ressource. Si une ressource vidéo, téléchargez une image personnalisée à afficher avant la lecture des débuts de la vidéo ou autorisez la génération d’une miniature à partir de la vidéo (cela peut prendre quelques minutes - il n’est pas nécessaire d’attendre).

![upload-video](assets/upload-video.png)

* Sélectionnez **[!UICONTROL Suivant]**.

### Paramètres {#settings}

* **[!UICONTROL Paramètres des réseaux sociaux]**

   Laissez les paramètres par défaut pour expérimenter les commentaires et l’évaluation des ressources d’activation par les apprenants.

* **[!UICONTROL Échéance]**

   *(Facultatif)* Une date de fin de l&#39;affectation peut être sélectionnée.

* **[!UICONTROL Auteur de la ressource]**

   *(Facultatif)* Laissez ce champ vide.

* **[!UICONTROL Contact&amp;ast de la ressource ;]**

   *(Obligatoire)* Utilisez le menu déroulant pour sélectionner un membre  `Quinn Harper`.

* **[!UICONTROL Expert de la ressource]**

   *(Facultatif)* Laissez ce champ vide.

   **Remarque** : Si les utilisateurs ou les groupes ne sont pas visibles, vérifiez qu’ils ont été ajoutés au  `Community Enable Members` groupe et  ** enregistrés sur l’instance de publication.

   ![activation-paramètres](assets/enablement-settings.png)

* Sélectionnez **[!UICONTROL Suivant]**

### Affectations {#assignments}

* **[!UICONTROL Ajouter des cessionnaires]**

   Ne pas définir car cette ressource d&#39;activation sera ajoutée à un chemin d&#39;apprentissage. Si un apprenant est affecté à la ressource d&#39;activation individuelle ainsi qu&#39;à un fichier learningPath contenant la ressource d&#39;activation, l&#39;apprenant est affecté à la ressource d&#39;activation deux fois.

   ![ajouts-affectations](assets/add-assignments.png)

* Sélectionnez **[!UICONTROL Créer]**

   ![create-resource](assets/create-resource.png)

La création réussie de la Ressource retourne à la console Ressources avec la Ressource nouvellement créée sélectionnée. A partir de cette console, il est possible de publier, d’ajouter des apprenants et de modifier d’autres paramètres.

Pour télécharger une nouvelle version de la ressource d&#39;activation, il est recommandé de créer une nouvelle ressource, puis d&#39;annuler l&#39;inscription des membres de l&#39;ancienne version et de les inscrire dans la nouvelle version.

### Publier la ressource {#publish-the-resource}

Pour que les inscrits puissent voir les ressources affectées, elles doivent être publiées :

* Sélectionner l&#39;icône `Publish` monde

L’Activation est confirmée par un message de réussite :

![publier-ressource](assets/publish-resource.png)

## Ajouter une deuxième ressource d&#39;activation {#add-a-second-enablement-resource}

Répétez les étapes ci-dessus pour créer et publier une seconde ressource d’activation associée à partir de laquelle un chemin d’apprentissage sera créé.

![ressource ajoutée](assets/add-resource.png)

**** Publier la seconde ressource.

Revenez à la liste des ressources du didacticiel d&#39;activation.

*Conseil : Si les deux ressources ne sont pas visibles, actualisez la page.*

![ressource actualisée](assets/refresh-resource.png)

## Ajouter un parcours de formation {#add-a-learning-path}

Un parcours d&#39;apprentissage est un regroupement logique de ressources d&#39;activation qui forment un cours.

* Dans la console Ressources, sélectionnez `+ Create`
* Sélectionner **[!UICONTROL Chemin d&#39;apprentissage]**

![add-learning-path](assets/add-learning-path.png)

Ajoutez **[!UICONTROL Informations de base]** :

* **[!UICONTROL Nom du cursus de formation]**

   Leçons de ski

* **[!UICONTROL Balises]**

   Didacticiel : Ski

* **[!UICONTROL Afficher dans le catalogue]**

   Ne pas activer

* **[!UICONTROL Téléchargement d’une image]**

   Pour représenter le chemin d’apprentissage dans la console Ressources.

   ![learning-path-basic](assets/learningpath-basic.png)

* Sélectionnez **[!UICONTROL Suivant]**.

Ignorez le panneau suivant, car il n’existe aucun chemin d’apprentissage prérequis à ajouter.

* Sélectionnez **[!UICONTROL Suivant]**

Dans le panneau Ajouter les ressources :

* Sélectionnez `+ Add Resources` pour sélectionner les 2 ressources de ski lessions à ajouter au parcours d&#39;apprentissage.

   Remarque : Seules les ressources **publiées** seront sélectionnables.

>[!NOTE]
>
>Vous pouvez uniquement sélectionner les ressources disponibles au même niveau que le chemin d’apprentissage. Par exemple, pour un parcours d’apprentissage créé dans un groupe, seules les ressources au niveau du groupe sont disponibles ; pour un parcours d&#39;apprentissage créé dans un site communautaire, les ressources de ce site sont disponibles pour l&#39;ajout au chemin d&#39;apprentissage.

* Sélectionnez **[!UICONTROL Envoyer]**.

   ![apprentissagePath](assets/learningpath-add.png)

   ![create-learning-path](assets/create-learningpath.png)

* Sélectionnez **[!UICONTROL Suivant]**

   ![apprentissage-path-settings](assets/learningpath-settings.png)

* **[!UICONTROL Ajouter des cessionnaires]**

   Utilisez le menu déroulant pour sélectionner le groupe `Community Ski Class`, qui doit inclure les membres `Riley Taylor` et `Sidney Croft.`.

* **[!UICONTROL Contact&amp;ast du parcours d&#39;apprentissage ;]**

   *(Obligatoire)* Utilisez le menu déroulant pour sélectionner un membre  `Quinn Harper`.

* Sélectionnez **[!UICONTROL Créer]**.

   ![apprentissage_path-info](assets/learningpath-info.png)

La création réussie du chemin d’apprentissage revient à la console Ressources avec le nouveau chemin d’apprentissage sélectionné. A partir de cette console, il est possible de publier, d’ajouter des apprenants et de modifier d’autres paramètres.

**** Publiez le chemin d’apprentissage.

