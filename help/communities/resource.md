---
title: Création et affectation de ressources d’activation
seo-title: Création et affectation de ressources d’activation
description: Ajouter ressources d'activation
seo-description: Ajouter ressources d'activation
uuid: da940242-0c9b-4ad8-8880-61fd41461c3b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8fe97181-600e-42ac-af25-d5d4db248740
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# Création et affectation de ressources d’activation {#create-and-assign-enablement-resources}

## Ajouter une ressource d&#39;activation {#add-an-enablement-resource}

Pour ajouter une ressource d’activation au nouveau site de la communauté :

* Connectez-vous en tant qu’administrateur système sur l’instance d’auteur :
   * For example, [http://localhost:4502/](http://localhost:4503/)
* Dans la navigation globale, sélectionnez **[!UICONTROL Communautés]** > **[!UICONTROL Ressources.]**

   ![chlimage_1-199](assets/chlimage_1-199.png)

   ![chlimage_1-200](assets/chlimage_1-200.png)
* Sélectionnez le site de la communauté sur lequel les ressources d&#39;activation sont ajoutées :
   * Sélectionnez **[!UICONTROL Activer le didacticiel]**.
* From the menu, select **[!UICONTROL Create]**.
* Sélectionnez **[!UICONTROL Ressource]**.

![chlimage_1-201](assets/chlimage_1-201.png)

### Informations de base {#basic-info}

Renseignez les informations de base de la ressource :

* **[!UICONTROL Nom du site]**

   Définissez sur le nom du site de la communauté sélectionnée : Didacticiel d&#39;activation

* **[!UICONTROL Resource Name&amp;ast;]**

   Leçon de ski 1

* **[!UICONTROL Balises]**

   Didacticiel : Sports / Ski

* **[!UICONTROL Afficher dans le catalogue]**

   Définissez-la sur **Activé**.

* **[!UICONTROL Description]**

   Glisser sur la neige pour les débutants.

* **[!UICONTROL Ajouter image]**

   Ajouter une image pour représenter la Ressource au membre dans son Affectations .

   ![chlimage_1-202](assets/chlimage_1-202.png)

* Sélectionnez **[!UICONTROL Suivant]**

### Ajouter du contenu {#add-content}

Bien qu’il semble que plusieurs ressources puissent être sélectionnées, une seule est autorisée.

Sélectionnez la ressource `'+' icon`, dans le coin supérieur droit, pour commencer le processus de sélection de la ressource en identifiant la source.

![chlimage_1-203](assets/chlimage_1-203.png) ![chlimage_1-204](assets/chlimage_1-204.png)

Téléchargez une ressource. Si une ressource vidéo, téléchargez une image personnalisée à afficher avant la lecture du vidéo ou autorisez la génération d’une miniature à partir de la vidéo (cela peut prendre quelques minutes, il n’est pas nécessaire d’attendre).

![chlimage_1-205](assets/chlimage_1-205.png)

* Sélectionnez **[!UICONTROL Suivant]**.

### Paramètres {#settings}

* **[!UICONTROL Paramètres des réseaux sociaux]**

   Laissez les paramètres par défaut pour expérimenter les commentaires et l’évaluation des ressources d’activation par les apprenants.

* **[!UICONTROL Échéance]**

   *(Facultatif)* Une date à laquelle l’affectation doit être terminée peut être sélectionnée.

* **[!UICONTROL Auteur de la ressource]**

   *(Facultatif)* Laissez ce champ vide.

* **[!UICONTROL Resource Contact&amp;ast;]**

   *(Obligatoire)* Utilisez le menu déroulant pour sélectionner un membre `Quinn Harper`.

* **[!UICONTROL Expert de la ressource]**

   *(Facultatif)* Laissez ce champ vide.

   **Remarque**: Si les utilisateurs ou les groupes ne sont pas visibles, vérifiez qu’ils ont été ajoutés au `Community Enable Members` groupe et *enregistrés* sur l’instance de publication.

   ![chlimage_1-206](assets/chlimage_1-206.png)

* Sélectionnez **[!UICONTROL Suivant]**

### Affectations {#assignments}

* **[!UICONTROL Ajouter des cessionnaires]**

   Ne pas définir, car cette ressource d&#39;activation sera ajoutée à un chemin d&#39;apprentissage. Si un apprenant est affecté à la ressource d&#39;activation individuelle ainsi qu&#39;à un chemin d&#39;apprentissage contenant la ressource d&#39;activation, il est affecté deux fois à la ressource d&#39;activation.

   ![chlimage_1-207](assets/chlimage_1-207.png)

* Sélectionnez **[!UICONTROL Créer]**

   ![chlimage_1-208](assets/chlimage_1-208.png)

La création réussie de la ressource revient à la console Ressources lorsque la ressource nouvellement créée est sélectionnée. A partir de cette console, il est possible de publier, d’ajouter des apprenants et de modifier d’autres paramètres.

Pour télécharger une nouvelle version de la ressource d&#39;activation, il est recommandé de créer une nouvelle ressource, puis de désinscrire les membres de l&#39;ancienne version et de les inscrire dans la nouvelle version.

### Publication de la ressource {#publish-the-resource}

Pour que les inscrits puissent voir les ressources affectées, elles doivent être publiées :

* Sélectionner l’ `Publish` icône mondiale

  est confirmé par un message de réussite :

![chlimage_1-209](assets/chlimage_1-209.png)

## Ajouter une deuxième ressource d&#39;activation {#add-a-second-enablement-resource}

Répétez les étapes ci-dessus pour créer et publier une seconde ressource d’activation associée à partir de laquelle un chemin d’apprentissage sera créé.

![chlimage_1-210](assets/chlimage_1-210.png)

**Publiez** la deuxième ressource.

Revenez à la liste des ressources du didacticiel d&#39;activation.

*Conseil : Si les deux ressources ne sont pas visibles, actualisez la page.*

![chlimage_1-211](assets/chlimage_1-211.png)

## Ajouter un cursus de formation {#add-a-learning-path}

Un parcours d’apprentissage est un regroupement logique de ressources d’activation qui forment un cours.

* Dans la console Ressources, sélectionnez `+ Create`
* Select **[!UICONTROL Learning Path]**

![chlimage_1-212](assets/chlimage_1-212.png)

Ajouter les informations **[!UICONTROL de base]**:

* **[!UICONTROL Nom du cursus de formation]**

   Leçons de ski

* **[!UICONTROL Balises]**

   Didacticiel : Ski

* **[!UICONTROL Afficher dans le catalogue]**

   Ne pas cocher

* **[!UICONTROL Téléchargement d’une image]**

   Pour représenter le chemin d’apprentissage dans la console Ressources.

   ![chlimage_1-213](assets/chlimage_1-213.png)

* Sélectionnez **[!UICONTROL Suivant]**.

Ignorez le panneau suivant, car il n’existe aucun chemin d’apprentissage prérequis à ajouter.

* Sélectionnez **[!UICONTROL Suivant]**

Dans le panneau Ajouter ressources :

* Sélectionnez `+ Add Resources` les 2 ressources de ski lessions à ajouter au parcours d&#39;apprentissage.

   Remarque : Seules les ressources **publiées** pourront être sélectionnées.

>[!NOTE]
>
>Vous pouvez uniquement sélectionner les ressources disponibles au même niveau que le chemin d’apprentissage. Par exemple, pour un parcours d’apprentissage créé dans un groupe, seules les ressources au niveau du groupe sont disponibles ; pour un parcours d’apprentissage créé dans un site communautaire, les ressources de ce site sont disponibles pour être ajoutées au chemin d’apprentissage.


* Sélectionnez **[!UICONTROL Envoyer]**.

   ![chlimage_1-214](assets/chlimage_1-214.png)

   ![chlimage_1-215](assets/chlimage_1-215.png)

* Sélectionnez **[!UICONTROL Suivant]**

   ![chlimage_1-216](assets/chlimage_1-216.png)

* **[!UICONTROL Ajouter des cessionnaires]**

   Utilisez le menu déroulant pour sélectionner le `Community Ski Class` groupe, qui doit inclure des membres `Riley Taylor` et `Sidney Croft.`

* **[!UICONTROL Contact&amp;amp du chemin d&#39;apprentissage;ast;]**

   *(Obligatoire)* Utilisez le menu déroulant pour sélectionner un membre `Quinn Harper`.

* Sélectionnez **[!UICONTROL Créer]**.

   ![chlimage_1-217](assets/chlimage_1-217.png)

La création réussie du chemin d’apprentissage revient à la console Ressources avec le nouveau chemin d’apprentissage sélectionné. A partir de cette console, il est possible de publier, d’ajouter des apprenants et de modifier d’autres paramètres.

**Publiez** le chemin d’apprentissage.

