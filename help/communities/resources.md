---
title: 'Console Ressources d’activation '
seo-title: 'Console Ressources d’activation '
description: La console Ressources permet aux gestionnaires d'activation de créer, gérer et affecter des ressources aux membres d'un site de la communauté d'activation.
seo-description: La console Ressources permet aux gestionnaires d'activation de créer, gérer et affecter des ressources aux membres d'un site de la communauté d'activation.
uuid: 52445b39-c339-4b39-8004-eb36de99bced
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1ef15e76-fe7c-4ced-a20d-c0a9385e3ee4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Console Ressources d’activation{#enablement-resources-console} 

Pour les communautés AEM, c’est dans la console Ressources que les gestionnaires [d’](users.md) activation créent, gèrent et attribuent des ressources aux membres d’un site de communauté d’activation.

## Conditions requises {#requirements}

Avant d’ajouter des ressources d’activation pour un site de la communauté, les instances AEM doivent être correctement configurées, notamment :

* SCORM
* FFmpeg

Pour plus d’informations, voir [Configuration de l’activation](enablement.md).

>[!CAUTION]
>
>Si SCORM est installé après la création du site de la communauté, toutes les ressources d’activation présentes avant l’installation de SCORM doivent être recréées.

>[!NOTE]
>
>Avec la version d’ [AEM 6.3](deploy-communities.md#latestfeaturepack) et des packages de fonctionnalités Communautés équivalents [AEM 6.2 FP3](deploy-communities.md#latestfeaturepack) et [AEM 6.1 FP7](https://docs.adobe.com/content/docs/en/aem/6-1/deploy/communities.html#Latest Feature Pack), la fonction d’activation ne nécessite plus de base de données [MySQL.](mysql.md)

## Terminologie {#terminology}

### Ressource {#resource}

Les ressources sont essentielles à une communauté [d&#39;](overview.md#enablement-community)activation. Ce sont les matériaux affectés aux membres qui leur permettent d&#39;améliorer leurs compétences.

Caractéristiques d&#39;une ressource :

* Peut être de type
   * Image (JPG, PNG, GIF, BMP)
   * Vidéo (MP4)
   * Flash (SWF)
   * Document (PDF)
   * Quiz (SCORM)
* Peut être référencé à partir d’un ou de plusieurs chemins d’apprentissage

### Cursus de formation {#learning-path}

Un parcours d’apprentissage est un ensemble logique de ressources d’activation regroupées pour faciliter l’affectation aux membres.

### Groupe de membres {#members-group}

Lors de la création d’un site communautaire, le nom donné au site pour l’URL est utilisé dans la création des groupes [d’utilisateurs spécifiques au](users.md) site configurés avec diverses autorisations pour divers rôles. Tous ces groupes créés automatiquement comportent un préfixe `Community *<site-name>*`.

Un de ces groupes d’utilisateurs est `Community *<site-name>* Members` le groupe, qui identifie les utilisateurs enregistrés dans l’environnement de publication comme membres de la communauté. Voir le didacticiel [Prise en main des communautés AEM pour l’activation](getting-started-enablement.md) pour obtenir un exemple.

Pour les communautés [d’](overview.md#egagementcommunity)engagement, il est raisonnable d’autoriser les visiteurs du site à s’inscrire ou à utiliser la connexion sociale, auquel moment ils sont automatiquement ajoutés au groupe de membres.

Pour les communautés [d’](overview.md#enablement-community)activation, il est recommandé de rendre le site privé, ce qui implique qu’un administrateur ajoute des utilisateurs au groupe de membres.

## Accès aux ressources d’activation d’un site communautaire {#accessing-a-community-site-s-enablement-resources}

### Accédez aux Ressources des communautés {#navigate-to-communities-resources}

Dans l’environnement de création, pour accéder à la console Ressources

* A partir de la navigation globale : **[!UICONTROL Navigation > Communautés > Ressources]**

![chlimage_1-163](assets/chlimage_1-163.png)

### Sélectionner un site de la communauté {#select-a-community-site}

La console Ressources des communautés affiche tous les sites de la communauté.

Les ressources d’activation sont créées pour un site communautaire spécifique après avoir sélectionné le site dans la console Ressources.

Une fois qu’un site communautaire spécifique est sélectionné, toutes les ressources d’activation et tous les chemins d’apprentissage existants sont accessibles pour la gestion et la modification, et de nouvelles ressources d’activation et de nouveaux chemins d’apprentissage peuvent être créés.

![chlimage_1-164](assets/chlimage_1-164.png)

#### Recherche {#search-features}

![chlimage_1-165](assets/chlimage_1-165.png)

Sélectionnez l’icône de basculement du panneau latéral pour rechercher une ressource d’activation ou un chemin d’apprentissage. Lorsqu’il est sélectionné, un panneau de recherche s’ouvre sur le côté gauche de la console et fournit une zone de texte dans laquelle les termes de recherche peuvent être saisis.

![chlimage_1-166](assets/chlimage_1-166.png)

#### Selection Mode {#selection-mode}

Pour sélectionner plusieurs ressources d’activation, sélectionnez la première en passant la souris sur la carte et en sélectionnant l’icône en forme de coche. Une fois sélectionnée, la sélection d’une autre carte l’ajoute au groupe de sélection. Si vous sélectionnez une seconde fois, la carte est désélectionnée.

![chlimage_1-167](assets/chlimage_1-167.png)

## Créer une ressource {#create-a-resource}

![chlimage_1-168](assets/chlimage_1-168.png)

Pour ajouter une nouvelle ressource d&#39;activation au site de la communauté

* Select the `Create` icon
* Dans le sous-menu qui s’affiche, sélectionnez `Resource`

Cette opération lance un processus détaillé de

* Description de la ressource (nom, image de carte et texte)
* Sélection du contenu de la ressource
* Sélection d’une image de couverture pour la ressource
* Identification des contacts de ressources
* Affectation de ressources aux membres

Lorsque la ressource fait partie d’un cours, un parcours d’apprentissage, les membres ne devraient être affectés qu’au chemin d’apprentissage. Les affectations peuvent être ajoutées une fois la ressource d&#39;activation créée.

### 1 Basic Info {#basic-info}

![chlimage_1-169](assets/chlimage_1-169.png)

* **[!UICONTROL Ajouter image]**

   (*facultatif*) Image à afficher sur la carte pour la ressource d&#39;activation dans la page des affectations du membre, ainsi que dans la console Ressources. L’image est sélectionnée dans le système de fichiers local du serveur. Si aucune image n’est fournie, une miniature est générée pour la ressource téléchargée.

   ***Remarque***: la taille d’image recommandée n’est pas de 480 x 480 pixels. En raison de la conception adaptée des cartes aux différentes dimensions du navigateur, la taille d’affichage varie de 220 x 165 pixels à 400 x 165 pixels.

* **[!UICONTROL Nom du site]**

   (*Lecture seule*) Site communautaire auquel la ressource est ajoutée.

* **[!UICONTROL Resource Name&amp;ast;]**

   (*obligatoire*) nom d’affichage de la ressource. Un nom de noeud valide est créé à partir du nom d’affichage.

* **[!UICONTROL Balises]**

   (*facultatif*) Vous pouvez choisir une ou plusieurs balises qui associent la ressource d’activation à un ou plusieurs catalogues. See [Tagging Enablement Resources](tag-resources.md).

* **[!UICONTROL Afficher dans le catalogue]**

   Lorsque cette option est désactivée, la ressource d’activation n’apparaît dans aucun catalogue. Si cette option est cochée, la ressource d’activation s’affiche dans tous les catalogues, sauf si elle est [pré-filtrée](catalog-developer-essentials.md#pre-filters) ou si les filtres de membre de l’interface utilisateur sont activés. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Description]**

   (*facultatif*) Description à afficher pour la ressource d&#39;activation.

* **[!UICONTROL Petite ressource]**

   (*facultatif*) Sélectionné à partir des ressources AEM. Image miniature représentant la ressource dans l’environnement de publication, par exemple dans un catalogue.

* **[!UICONTROL Grande ressource]**

   (*facultatif*) Sélectionné à partir des ressources AEM. Grande image représentant la ressource dans l’environnement de publication, par exemple sur la page principale d’une ressource.

* **[!UICONTROL Ressource de fragment de contenu]**

   (*facultatif*) Sélectionné à partir des ressources AEM. Fragment de contenu qui peut être référencé dans l’environnement de publication, mais qui n’est pas utilisé par défaut.

* Sélectionnez **[!UICONTROL Suivant]**

### 2 Add Content {#add-content}

![chlimage_1-170](assets/chlimage_1-170.png)

Bien qu&#39;il semble que plusieurs ressources d&#39;activation puissent être sélectionnées, une seule est autorisée.

Sélectionnez la `'+' icon`, dans le coin supérieur droit, pour commencer le processus de sélection de la ressource en identifiant la source.

![chlimage_1-171](assets/chlimage_1-171.png)

* **[!UICONTROL Télécharger à partir de mes fichiers]** locaux Le téléchargement depuis le système de fichiers local utilisera l’explorateur de fichiers natif pour sélectionner et télécharger un fichier. Les types de fichier pris en charge sont SCORM.zip (HTML5 ou SWF), MP4, SWF, PDF et les types d’image (JPG, PNG, GIF, BMP). Le nom de fichier devient le nom du fichier, qui est ajouté à la bibliothèque de fichiers.

* **[!UICONTROL Parcourir la bibliothèque]** de fichiers Sélectionner dans la bibliothèque de fichiers. La sélection est limitée à celles qui sont visibles sur le site communautaire.

* **[!UICONTROL Ajouter une URL externe]**

   Entrez un lien vers le contenu d’apprentissage.

   Dans la boîte de dialogue qui s’ouvre, saisissez :

   * **[!UICONTROL Titre]**

      Nom du fichier pour la ressource d’activation.

   * **[!UICONTROL URL]**

      URL d’un fichier.

* **[!UICONTROL Ajouter une URL Adobe Connect]**

   Entrez un lien vers une session Adobe Connect.

   Dans la boîte de dialogue qui s’ouvre, saisissez :

   * **[!UICONTROL Titre]**

      Nom du fichier pour la ressource d’activation.

   * **[!UICONTROL URL]**

      URL d’une session Adobe Connect.

* **[!UICONTROL Définir une ressource externe]**

   Entrez l&#39;emplacement où le matériau doit être présenté. Les valeurs de l’état et du score de réussite sont saisies manuellement (voir [Rapports](reports.md)). Une image de couverture téléchargée peut être utilisée pour fournir des informations supplémentaires.

   Dans la boîte de dialogue qui s’ouvre, saisissez :

   * **[!UICONTROL Titre]**

      Nom du fichier pour la ressource d’activation.

   * **[!UICONTROL Emplacement]**

      Emplacement d’un site physique, tel qu’une salle de classe.

#### Exemple de ressource vidéo ajoutée {#example-of-an-added-video-resource}

![chlimage_1-172](assets/chlimage_1-172.png)

* **[!UICONTROL Image de couverture des ressources]**

   L&#39;image de couverture est une image à afficher lors de la première consultation de la ressource d&#39;activation. Par exemple, l’image de couverture s’affiche lorsqu’une ressource vidéo n’est pas encore lue. Si aucune image personnalisée n’est téléchargée, une image par défaut est affichée. Pour les ressources vidéo, il peut être possible de [générer une miniature](enablement.md#ffmpeg), mais uniquement lorsqu’elle est téléchargée et non lorsque la vidéo est référencée comme URL. Pour les ressources d’emplacement, l’image peut être utilisée pour fournir des informations supplémentaires.

   La taille recommandée pour l’image de couverture est de 640 x 360 px.

* Sélectionnez **[!UICONTROL Suivant]**

### 3 Settings {#settings}

![chlimage_1-173](assets/chlimage_1-173.png)

>[!NOTE]
>
>Les apprenants ne doivent pas être inscrits directement dans les ressources d’activation qui doivent être référencées à partir d’un chemin d’apprentissage. Les apprenants ne doivent être inscrits qu&#39;au cursus d&#39;apprentissage.
>
>Si un membre est inscrit à la fois dans une ressource et dans un chemin d’apprentissage qui fait référence à cette ressource, ses affectations indiqueront à la fois la ressource unique et la ressource dans le chemin d’apprentissage.

* **[!UICONTROL Paramètres des réseaux sociaux]**

   Ces paramètres permettent de déterminer si les apprenants sont en mesure de fournir des informations concernant la ressource d’activation. Les paramètres [de](sites-console.md#moderation) modération sont ceux du site de la communauté parent.

   * **[!UICONTROL Autoriser les commentaires]**

      Si cette option est cochée, les membres sont autorisés à commenter la ressource. Cette option est cochée par défaut.

   * **[!UICONTROL Autoriser les évaluations]**

      Si cette option est cochée, les membres sont autorisés à évaluer la ressource. Cette option est cochée par défaut.

   * **[!UICONTROL Autoriser l&#39;accès anonyme]**

      Si cette option est cochée, les visiteurs anonymes du site sont autorisés à afficher la ressource dans un catalogue lorsque le site communautaire autorise également l’accès anonyme. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Échéance]**
   *(Facultatif)* Une date à laquelle l’affectation doit être terminée peut être sélectionnée.

* **[!UICONTROL Auteur de la ressource]**
   *(Facultatif)* Auteur de la ressource d’activation. Utilisez le menu déroulant pour effectuer une sélection parmi les utilisateurs membres du groupe [de](#members-group)membres.

* **[!UICONTROL Resource Contact&amp;ast;]**
   *(Obligatoire)* Personne avec laquelle le membre peut communiquer au sujet de la ressource d&#39;activation. Utilisez le menu déroulant pour effectuer une sélection parmi les utilisateurs membres du groupe [de](#members-group)membres.

* **[!UICONTROL Expert de la ressource]**
   *(Facultatif)* Une personne avec qui le membre peut contacter qui possède une expertise concernant la ressource d&#39;activation. Utilisez le menu déroulant pour effectuer une sélection parmi les utilisateurs membres du groupe [de](#members-group)membres.

### 4 Assignments {#assignments}

![chlimage_1-174](assets/chlimage_1-174.png)

* **[!UICONTROL Ajouter des personnes]** Utilisez le menu déroulant pour sélectionner parmi les [membres](#members-group) - les utilisateurs et les groupes d’utilisateurs (en caractères gras) - qui doivent être inscrits comme apprenants. Lorsque les membres se connectent au site de la communauté, les ressources d’activation (et les chemins d’apprentissage) dans lesquels ils sont inscrits s’affichent sur leur page [Affectations](functions.md#assignments-function) .

* Sélectionnez **[!UICONTROL Créer]**.

![chlimage_1-175](assets/chlimage_1-175.png)

La création réussie de la ressource d&#39;activation revient à la console Ressources avec la ressource nouvellement créée sélectionnée. A partir de cette console, il est possible de [gérer la ressource](#managing-a-resource).

## Create a Learning Path {#create-a-learning-path}

![chlimage_1-176](assets/chlimage_1-176.png)

Pour ajouter un nouveau chemin d’apprentissage au site de la communauté

* Select the `Create` icon
* Dans le sous-menu qui s’affiche, sélectionnez `Learning Path`

Cette opération lance un processus détaillé de

* Identification du chemin d’apprentissage
* Fournir une image de carte représentant le chemin d’apprentissage des apprenants
* Référence aux ressources d’activation à inclure dans le chemin d’apprentissage
* Ordre facultatif des ressources
* Identification facultative des chemins d’apprentissage prérequis
* Identification d’un contact de chemin d’apprentissage
* Inscription de membres

Pour les ressources d’activation incluses dans un parcours d’apprentissage, les affectations ne doivent être faites que pour le parcours d’apprentissage et non pour les ressources individuelles.

### Informations de base {#basic-info-1}

![chlimage_1-177](assets/chlimage_1-177.png)

* **[!UICONTROL Ajouter image]**

   (*facultatif*) Image à afficher sur la carte pour le chemin d’apprentissage dans la page des affectations du membre ainsi que dans la console Ressources. L’image est sélectionnée dans le système de fichiers local du serveur. Si aucune image n’est fournie, une miniature est générée pour la ressource téléchargée.

   ***Remarque***: la taille d’image recommandée n’est plus simplement de 480 x 480 pixels. En raison de la conception adaptée des cartes aux différentes dimensions du navigateur, la taille d’affichage varie de 220 x 165 pixels à 400 x 165 pixels.

* **[!UICONTROL Nom du site]**

   (*Lecture seule*) Site communautaire auquel la ressource est ajoutée.

* **[!UICONTROL Nom du cursus de formation]**

   (*obligatoire*) nom d’affichage du chemin d’apprentissage. Un nom de noeud valide est créé à partir du nom d’affichage.

* **[!UICONTROL Balises]**

   (*facultatif*) Il est possible de choisir une ou plusieurs balises qui associent le chemin d’apprentissage à un ou plusieurs catalogues. See [Tagging Enablement Resources](tag-resources.md).

* **[!UICONTROL Afficher dans le catalogue]**

   Lorsque cette option est désactivée, le chemin d’apprentissage n’apparaît dans aucun catalogue. Si cette option est cochée, le chemin d’apprentissage s’affiche dans tous les catalogues, sauf si le paramètre est [pré-filtré](catalog-developer-essentials.md#pre-filters) ou si le membre filtre l’interface utilisateur. L’affichage du chemin d’apprentissage dans un catalogue permet indirectement à READ d’accéder à toutes ses ressources contenues. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Description]**

   (*facultatif*) Description à afficher pour la ressource d&#39;activation.

* **[!UICONTROL Petite ressource]**

   (*facultatif*) Sélectionné à partir des ressources AEM. Image miniature représentant la ressource dans l’environnement de publication, par exemple dans un catalogue.

* **[!UICONTROL Grande ressource]**

   (*facultatif*) Sélectionné à partir des ressources AEM. Grande image représentant la ressource dans l’environnement de publication, par exemple sur la page principale d’une ressource.

* **[!UICONTROL Ressource de fragment de contenu]**

   (*facultatif*) Sélectionné à partir des ressources AEM. Fragment de contenu qui peut être référencé dans l’environnement de publication, mais qui n’est pas utilisé par défaut.

* Sélectionnez **[!UICONTROL Suivant]**

### Ajouter des conditions préalables {#add-prerequisites}

![chlimage_1-178](assets/chlimage_1-178.png)

* **[!UICONTROL Chemins]** d’apprentissage prérequis (*facultatifs*) Lorsque d’autres chemins d’apprentissage publiés sont sélectionnés, ils doivent être terminés avant qu’un apprenant puisse sélectionner ce chemin d’apprentissage.

* Sélectionnez **[!UICONTROL Suivant]**

### Ajouter des ressources {#add-resources}

![chlimage_1-179](assets/chlimage_1-179.png)

* **[!UICONTROL Mettre en place l’ordre du cursus de formation]**

   (*facultatif*) si la valeur On est définie, l’ordre dans lequel les ressources d’activation sont ajoutées est l’ordre dans lequel les apprenants sont tenus de suivre le parcours d’apprentissage. La valeur par défaut est Désactivé.

* **[!UICONTROL Ressources]**

   Une ou plusieurs ressources choisies parmi les *ressources d&#39;activation publiées créées pour le site communautaire actuel.

>[!NOTE]
>
>Vous pouvez uniquement sélectionner les ressources disponibles au même niveau que le chemin d’apprentissage. Par exemple, pour un parcours d’apprentissage créé dans un groupe, seules les ressources au niveau du groupe sont disponibles ; pour un parcours d’apprentissage créé dans un site communautaire, les ressources de ce site sont disponibles pour être ajoutées au chemin d’apprentissage.

* Sélectionnez **[!UICONTROL Suivant]**.

### Paramètres {#settings-1}

![chlimage_1-180](assets/chlimage_1-180.png)

* **[!UICONTROL Ajouter des inscriptions]**

   Utilisez le menu déroulant pour sélectionner parmi les membres et les groupes de membres (en caractères gras) qui sont membres du groupe [de](#members-group)membres du site communautaire. Il n’est pas nécessaire d’ajouter des affectations lors de la première création du chemin d’apprentissage. Les propriétés du chemin d’apprentissage peuvent être modifiées pour ajouter des apprenants ultérieurement.

* **[!UICONTROL Contact&amp;amp du chemin d&#39;apprentissage;ast;]**

   *(Obligatoire)* Personne avec laquelle le membre peut communiquer au sujet du cheminement d&#39;apprentissage. Utilisez le menu déroulant pour sélectionner les utilisateurs qui appartiennent au groupe [des](#members-group)membres du site de la communauté.

* Sélectionnez **[!UICONTROL Créer]**

>[!NOTE]
>
>Les ressources d’activation référencées à partir du chemin d’apprentissage ne doivent pas répertorier les mêmes personnes (apprenants).
>
>Si un membre est inscrit à la fois dans une ressource d’activation et dans un chemin d’apprentissage qui fait référence à cette ressource, ses affectations indiqueront à la fois la ressource unique et la ressource dans le chemin d’apprentissage.

## Gestion d’une ressource {#managing-a-resource}

Pour gérer une ressource d&#39;activation unique

* Dans la console Ressources
* Sélectionnez le site de la communauté qui contient la ressource
* Sélectionner la ressource

Pour la ressource d&#39;activation sélectionnée, il est possible de :

* Propriétés d’affichage (par défaut)
* Modifier les propriétés
* Supprimer
* Publier
* Annuler la publication

Pour télécharger une nouvelle version de la ressource d’activation, il est recommandé de créer une nouvelle ressource, puis de désinscrire les membres de l’ancienne version et de les inscrire à la nouvelle version.

### Modifier la ressource {#edit-resource}

![chlimage_1-181](assets/chlimage_1-181.png)

En sélectionnant l&#39;icône représentant un crayon, les étapes de création d&#39;une ressource d&#39;activation sont mises à disposition afin que toutes les informations fournies puissent être modifiées.

Si la seule modification consiste à modifier les affectations à l’étape Paramètres, l’enregistrement des modifications entraîne la publication des modifications. Si d’autres modifications sont effectuées, la ressource doit être publiée explicitement après l’enregistrement.

### Supprimer la ressource {#delete-resource}

![chlimage_1-182](assets/chlimage_1-182.png)

En sélectionnant l&#39;icône de la corbeille, la ressource d&#39;activation sera `Delete`exécutée après confirmation.

### Publication {#publish}

![chlimage_1-183](assets/chlimage_1-183.png)

Pour que les apprenants puissent voir une ressource d’activation affectée, elle doit être publiée :

* Sélectionnez l’icône de l’univers pour `Publish`
* Dans la boîte de dialogue qui s’affiche, sélectionnez **[!UICONTROL Publier]** à nouveau.
* Sélectionner **[!UICONTROL Fermer]**

Bien que la boîte de dialogue indique que l’action est mise en file d’attente, elle est souvent publiée immédiatement.

### Annuler la publication {#unpublish}

![chlimage_1-184](assets/chlimage_1-184.png)

Pour rendre temporairement les ressources d’activation inaccessibles aux membres de l’environnement de publication sans les supprimer, utilisez l’icône du monde pour `Unpublish`la ressource.

### Rapport {#report}

![chlimage_1-185](assets/chlimage_1-185.png)

L’icône Rapport permet d’accéder aux rapports générés lorsque les apprenants interagissent avec les ressources d’activation qui leur sont affectées dans l’environnement de publication. Le rapport varie selon le type de ressource.

Pour tous les chemins d’apprentissage, il est possible d’afficher un rapport en fonction des ressources ou des apprenants ( `User Report`).

![chlimage_1-186](assets/chlimage_1-186.png)

Ce rapport est spécifique à la ressource d’activation actuelle ou au chemin d’apprentissage. La profondeur des rapports fournis dépend du niveau de licence et d’activation d’ [Adobe Analytics](analytics.md) pour le site de la communauté. Les rapports [Calendrier](#timeline), Engagement [des](#viewer-engagement)visionneuses et [Engagement par périphérique](#engagement-by-device) sont importés d’Adobe Analytics en fonction de l’intervalle d’ [interrogation.](analytics.md#report-importer)

Pour toutes les ressources d’activation, qu’Adobe Analytics soit activé ou non, il existe des rapports sur l’état [et le](#assignee-status) classement [des](#ratings) personnes concernées, ainsi qu’un tableau récapitulatif [des](#report-summary) rapports.

![chlimage_1-187](assets/chlimage_1-187.png)

#### Chronologie {#timeline}

Le rapport Journal d’Analytics montre quand des événements se produisent au fil du temps pour cette ressource d’activation :

* **Vues**

   Une vue est lorsque l’utilisateur visite la page des détails de la ressource.

* **Lectures**

   Une lecture se produit lorsque alLearner interagit avec la ressource, par exemple en lisant une vidéo ou en ouvrant un PDF.

* **Evaluations**

   Une évaluation est lorsque l’utilisateur affecte une évaluation à une ressource.

* **Commentaires**

   Un commentaire est le moment où alLearner ajoute un commentaire

L’axe vertical est le nombre d’événements.

L’axe horizontal est l’heure du calendrier.

[Adobe Analytics requis](sites-console.md#analytics).

#### Engagement de la visionneuse {#viewer-engagement}

Le rapport Engagement des visionneuses Analytics montre, pour les ressources vidéo, le nombre d’apprenants qui ont consulté la ressource et, s’ils n’ont pas lu la ressource jusqu’à la fin, à quel moment les apprenants ont arrêté de la lire.

L’axe vertical est le nombre d’apprenants qui ont consulté cette ressource.

L&#39;axe horizontal est la durée de cette ressource.

[ID d’entreprise Marketing Cloud requis](sites-console.md#enablement).

#### Engagement par périphérique {#engagement-by-device}

Le rapport Engagement Analytics par périphérique, pour les ressources vidéo, décrit le pourcentage de vues lues depuis le bureau et depuis les périphériques mobiles.

[ID d’entreprise Marketing Cloud requis](sites-console.md#enablement).

#### État des cessionnaires {#assignee-status}

Le rapport État du signataire, basé sur le nombre d’apprenants, décrit le nombre d’entre eux

* **Non démarré**
* **En cours**
* **Terminé**

#### Evaluations {#ratings}

Le rapport Notations est basé sur le nombre d’apprenants qui ont évalué la ressource d’activation, en indiquant le nombre de chaque évaluation, suivi d’un résumé du nombre total d’évaluations et de la note moyenne.

#### Résumé du rapport {#report-summary}

Pour une ressource d’activation, le résumé du rapport est un tableau répertoriant

* Chaque apprenant qui a interagi avec la ressource
   * Leur statut
   * Si la ressource leur a été affectée
      * Par opposition à la recherche de la ressource dans un catalogue
   * Nombre de commentaires publiés
   * La note donnée, le cas échéant

Pour un rapport de ressources de cheminement de formation, le résumé du rapport est un tableau répertoriant

* Chaque ressource incluse dans le parcours d’apprentissage
   * État de publication
   * Nombre de vues
   * Nombre de lectures
   * Note moyenne
   * Format
   * Taille
   * Nom du site de la communauté

Pour un rapport Utilisateur de cheminement de formation, le résumé du rapport est un tableau répertoriant

* Chaque apprenant affecté au chemin d’apprentissage
   * Nombre de ressources terminées
   * Leur statut

Il est possible d’ajuster l’affichage du tableau en sélectionnant des colonnes à l’aide du `Show / hide columns` sélecteur.

#### Download Report as CSV {#download-report-as-csv}

Le tableau Résumé des rapports peut être téléchargé au format CSV à l’aide d’un bouton en haut de la console.

* pour une ressource d&#39;activation : `Download Resource Report as CSV` , bouton
* pour un parcours d’apprentissage : `Download Learning Path Report as CSV` , bouton

Le résumé complet des rapports est téléchargé indépendamment des colonnes sélectionnées pour l’affichage.
