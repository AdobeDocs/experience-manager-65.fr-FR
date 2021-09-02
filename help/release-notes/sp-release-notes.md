---
title: '[!DNL Experience Manager] Notes de mise à jour du Service Pack 6.5'
description: Notes de mise à jour spécifiques à [!DNL Adobe Experience Manager] Service Pack 10 6.5
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: d107a31ff109be6ae848eef5d3102f63983fd120
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] Notes de mise à jour du Service Pack 6.5 {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.10.0 |
| Type | Version du Service Pack |
| Date  | 26 août 2021 |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## Éléments inclus dans [!DNL Adobe Experience Manager] 6.5.10.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] La version 6.5.10.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la version 6.5 d’avril 2019. Le Service Pack est installé sur [!DNL Adobe Experience Manager] 6.5.

Les fonctionnalités et améliorations clés introduites dans [!DNL Adobe Experience Manager] 6.5.10.0 sont les suivantes :

* **Amélioration des  [!DNL Content Fragment] modèles et de l’éditeur** : Vous pouvez désormais créer des modèles complexes et personnalisés pour du contenu structuré à l’aide de  [!DNL Content Fragment] modèles imbriqués. Les structures de contenu sont modulaires en éléments de base modélisés en sous-fragments. Les fragments de niveau supérieur référencent ces sous-fragments. D’autres améliorations de type de données telles que les règles de validation avancées améliorent davantage la flexibilité de la modélisation de contenu avec [!DNL Content Fragments]. L’éditeur [!DNL Experience Manager] [!DNL Content Fragment] prend en charge les structures de fragments imbriqués dans une session d’éditeur commune, avec des améliorations telles que l’arborescence de structure et la navigation par chemin de navigation à onglets dans les hiérarchies de fragments.

* **API GraphQL pour[!DNL Content Fragments]**: La nouvelle API GraphQL est la méthode standard pour diffuser du contenu structuré au format JSON. Les requêtes GraphQL permettent aux clients de demander uniquement les éléments de contenu appropriés pour effectuer le rendu d’une expérience. Une telle sélection élimine la sur-diffusion du contenu (possibilité avec les API HTTP REST) qui nécessite une analyse du contenu côté client. Les schémas GraphQL sont dérivés de modèles [!DNL Content Fragment] et les réponses de l’API sont effectuées au format JSON. Dans [!DNL Experience Manager] sous la forme [!DNL Cloud Service], les requêtes [GraphQL persistent](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) et traitent les demandes de GET compatibles avec le cache. Cela n’est pas encore possible dans [!DNL Experience Manager] 6.5.10.0.

* **Gestion des hiérarchies et aperçu** futur : Les utilisateurs disposent désormais d’une interface pour accéder aux structures de contenu de leurs  [!DNL Experience Manager] lancements, notamment la possibilité d’ajouter et de supprimer des pages dans un lancement. Cette fonctionnalité offre une plus grande flexibilité de [!DNL Experience Manager] lancements pour créer des versions de contenu destinées à une publication ultérieure. [Les ](/help/sites-authoring/working-with-page-versions.md#timewarp) fonctionnalités de distorsion du temps permettent aux utilisateurs de prévisualiser les lancements comme des états de contenu futurs.

* **Ressources connectées** :  [!DNL Experience Manager] étend la  [!DNL Connected Assets] fonctionnalité à l’utilisation des  [!DNL Dynamic Media] images dans les composants principaux applicables. Voir [Utilisation des ressources connectées](/help/assets/use-assets-across-connected-assets-instances.md).

* **Options de partage de lien pour télécharger des ressources ou des rendus** : Lors du partage de ressources et de collections en tant que lien, les utilisateurs peuvent choisir d’autoriser le téléchargement des ressources d’origine ou de leurs rendus, ou les deux à l’aide du lien partagé. En outre, les utilisateurs qui téléchargent les ressources partagées avec eux via un lien ont la possibilité de télécharger uniquement les ressources d’origine, uniquement les rendus, ou les deux.

* **Limiter les sous-ressources générées** : Les administrateurs peuvent limiter le nombre de sous-ressources  [!DNL Experience Manager] générées pour les ressources composites telles que les fichiers PDF, PowerPoint, InDesign et Keynote. Voir [Gestion des ressources composites](/help/assets/managing-linked-subassets.md#generate-subassets).

* **Prise en charge** Camera Raw : Un nouveau  [!DNL Camera Raw] package prend en charge  [!DNL Adobe Camera Raw] la version 10.4. Voir  [Traiter les images à l’aide de [!DNL Camera Raw]](/help/assets/camera-raw.md).

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la  1.22.8.

* **Amélioration de l’accessibilité**:

   * [!DNL Dynamic Media] offre de nombreuses améliorations de l’accessibilité pour les visionneuses. Voir [[!DNL Dynamic Media] mises à jour](#dynamic-media-65100).

   * Platform fournit quelques améliorations de l’accessibilité. Voir [Mises à jour de la plateforme](#platform-65100).

* **Améliorations de l’expérience utilisateur** :

   * [!DNL Experience Manager] affiche directement une liste de tous les modèles de contenu sous un dossier sans que les auteurs de contenu aient à parcourir la structure de fichiers. La fonctionnalité nécessite désormais moins de clics et améliore l’efficacité de création.

   * Le champ de chemin dans l’éditeur [!DNL Sites] permet aux auteurs de faire glisser des ressources à partir de [!DNL Content Finder].

* Ajout de la prise en charge de l’API `GuideBridge#getGuidePath` dans [!DNL AEM Forms].

* Vous pouvez désormais utiliser le service de conversion automatique de formulaire pour [convertir les PDF Forms en français, en allemand et en espagnol](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#language-specific-meta-model) en formulaires adaptatifs.

* **Messages d’erreur dans le navigateur Propriétés** : ajout de messages d’erreur pour chaque propriété dans le navigateur Propriétés des formulaires adaptatifs. Ces messages aident à comprendre les valeurs autorisées pour un champ.

* **Prise en charge de l’utilisation de l’option littérale pour définir la valeur d’une variable** de type JSON : Vous pouvez utiliser l’option littérale pour définir la valeur d’une variable de type JSON à l’étape de définition de la variable d’un workflow AEM. L’option de littéral permet de spécifier un fichier JSON sous la forme d’une chaîne.

* **Mises à jour de la plateforme** :  [!DNL Adobe Experience Manager Forms] sur JEE a ajouté la prise en charge des plateformes suivantes :
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

Pour obtenir la liste de toutes les fonctionnalités et améliorations introduites dans [!DNL Experience Manager] 6.5.10.0, voir [les nouveautés de [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md).

Voici la liste des correctifs fournis dans la version [!DNL Experience Manager] 6.5.10.0.

### [!DNL Sites] {#sites-65100}

* La sélection se déplace vers un autre champ lors de la saisie dans le champ **[!UICONTROL Valeur par défaut]** sous l’onglet **[!UICONTROL Propriétés]** de l’éditeur de fragments de contenu (NPR-36992).

* Lors du filtrage des modèles [!DNL Content Fragment] sous un chemin spécifié, la recherche [!DNL Experience Manager] renvoie tous les noeuds avec `cq:Template` au lieu de renvoyer des chemins et des noeuds uniquement pour le modèle [!DNL Content Fragment] (SITES-1453).
* [!DNL Content Fragments] return  `null` comme état des dossiers (SITES-1157).
* [!DNL Experience Manager] ne permet pas aux utilisateurs de désactiver et d’activer les  [!DNL Content Fragment] modèles (SITES-1088).
* Lorsqu’un utilisateur déplace, renomme ou supprime des [!DNL Content Fragments] ou des ressources multimédias, les [!DNL Content Fragments] référencées ne sont pas automatiquement mises à jour (SITES-196).
* Le collage de composants d’une page à une autre génère des erreurs JavaScript (NPR-37030).
* Lorsque les propriétés de page sont affichées rapidement, les propriétés de page d’une autre page sont ouvertes (NPR-37025).
* Le fragment de contenu permet au fragment de contenu de se référencer lui-même. Le sélecteur ne prend pas en charge l’opération (NPR-36993).
* Après la mise à niveau vers le Service Pack 9, certains utilisateurs ne peuvent pas déplacer les dossiers dans Experience Manager et voir des erreurs dans les journaux (SITES-1481).
* Lors de l’ajustement de la largeur du composant dans le conteneur de mises en page en mode d’édition, un scintillement est observé (NPR-36961).
* Lors de la promotion d’un lancement, les modifications du lancement promu sont déployées deux fois sur les autres lancements. Si un utilisateur fait la promotion du double lancement déployé, le contenu doublé est reflété sur la page source (NPR-36893).
* [!DNL Experience Manager] ajoute une bordure grise à certaines images PNG avec transparence si vous ajoutez les images à une page à l’aide du composant principal Image ou si vous redimensionnez à l’aide du composant Image de base (NPR-36879).
* [!DNL Experience Manager Sites] L’interface utilisateur d’administration avec un grand nombre de modèles ralentit la navigation (NPR-36870).
* La mise à niveau vers le Service Pack 9 empêche la création de quelques composants. Ce problème ne permet pas aux utilisateurs [!DNL Sites] de créer des pages (NPR-36857).
* La méthode `ContextHubImpl` crée une `ResourceResolver` qui n’est pas fermée. Elle génère des messages d’avertissement sur `ResourceResolver` , et le service renvoie parfois des résultats inattendus (NPR-36853).
* Lors de la synchronisation d’une seule Live Copy à partir des propriétés de page de plan directeur, toutes les autres Live Copies sont également synchronisées (NPR-36829, NPR-36522).
* Lorsque seul le type MIME XLS est utilisé, la fonction de téléchargement de fichier ne fonctionne pas comme prévu (NPR-36785).
* Les nouvelles balises avec majuscules et majuscules ne sont pas affichées dans le champ de balise dans [!DNL Content Fragments] (NPR-36742).
* L’option Un seul élément de texte lors de l’ajout d’un [!DNL Content Fragment] entraîne l’absence de texte et crée une mise en forme impaire liée aux listes et aux listes imbriquées (NPR-36565).
* Lorsqu’un auteur annote un composant sur une page, le supprime et annule l’opération de suppression, une erreur se produit lors de la tentative d’affichage des données de la chronologie de la page dans la console Sites (NPR-36528).
* Propriétés de page L’option [!UICONTROL Enregistrer et fermer] de l’éditeur en bloc enregistre les modifications mais ne ferme pas l’éditeur (NPR-36527).
* Lorsqu’un utilisateur tente de faire glisser un nouveau composant Texte sur une page, le composant disparaît immédiatement (NPR-36442).
* Lorsqu’un utilisateur saisit une balise à la demande qui comprend de l’espace (la balise qui n’existe pas sur le système) et appuie sur Entrée, la balise s’affiche sous le champ . Cependant, lorsque la balise [!DNL Content Fragment] est enregistrée et rouverte, la balise à la demande n’apparaît pas (NPR-36441).
* Le modèle ne peut pas être supprimé lorsque l’instance est accessible via Dispatcher (NPR-36385).
* Lorsqu’une page est déplacée, une actualisation manuelle du navigateur est nécessaire pour effectuer le rendu des modifications (NPR-36381).
* Lorsque vous sélectionnez un composant, vous pouvez le couper ou le copier en utilisant les combinaisons Ctrl+X ou Ctrl+C (et Commande+X ou Commande+C sous Mac). Lorsque vous cliquez sur un autre composant, vous pouvez coller avec la barre d’outils, mais pas avec le clavier (Ctrl+V ou Commande+V) (NPR-36379).
* Lorsqu’un utilisateur tente de couper des composants à l’aide de l’icône ciseaux pour les déplacer ailleurs, une erreur de console se produit. De plus, lorsque vous collez un seul composant, il est déplacé (NPR-36378).
* [!DNL Experience Manager] a une requête sans index sur la gestion de contenu web ou les notifications, elle ralentit les performances (NPR-36303).
* Lorsqu’un auteur restaure l’héritage sur le composant hérité supprimé, l’option disponible consiste à synchroniser tout le contenu de la page. Les auteurs de contenu doivent synchroniser la page entière même si l’héritage n’est restauré que sur un seul composant. Une synchronisation complète peut entraîner la synchronisation du contenu indésirable (NPR-34456, CQ-4310183).
* L’utilisation en direct d’un composant sur l’instance d’auteur n’affiche pas toutes les occurrences. Certains composants sont utilisés dans plus de 1 000 pages, mais le rapport n’affiche qu’environ 40 pages (CQ-4323724).
* Lorsqu’il existe une structure de site comportant de nombreuses sous-pages, le chargement des sous-pages en mode Colonne prend plus de temps dans Experience Manager 6.5.8 que dans Experience Manager 6.4.8.2 (CQ-4322766).
* Décochez la case &quot;Tout&quot; ne fonctionne pas sur l’option &quot;Page de déploiement&quot; (NPR-37070).
* Lors de l’ouverture d’une version de composant v3 existante d’une page, la boîte de dialogue Propriétés de la page ne s’ouvre pas et un `NullPointerException` est consigné (SITES-1830).

### [!DNL Assets] {#assets-65100}

Les problèmes suivants ont été corrigés dans [!DNL Assets] :

* La valeur de la propriété `jcr:title` n’est pas mise à jour sur l’instance de publication après le déplacement d’un dossier. Le fait de renommer et de republier un dossier dans l’instance de création ne met pas à jour la valeur de propriété `jcr:title` de la même instance dans l’instance de publication (NPR-36369).

* Si plusieurs ressources sont sélectionnées et qu’un ou plusieurs champs de métadonnées sont modifiés, l’opération d’enregistrement échoue avec le code d’erreur 500 dans le navigateur Safari (NPR-36413).

* L’importation de métadonnées en bloc échoue en raison d’un format de date incorrect (NPR-36428).

* Lorsqu’une sélection est effectuée sur la page [!UICONTROL Propriétés] pour mettre à jour les métadonnées, l’interface tarde à répondre lorsque de nombreuses options sont fournies par le schéma (NPR-36430).

* Le filtre de recherche utilisant le prédicat [!UICONTROL État d’expiration] ne fonctionne pas (NPR-36436).

* Le menu contextuel de divers champs des propriétés [!UICONTROL Métadonnées de dossier] n’affiche pas les dernières valeurs sélectionnées (NPR-36937, CQ-4314429).

* Lors de la recherche de fichiers et de dossiers, si l’utilisateur applique un filtre et sélectionne [!UICONTROL Fichiers et dossiers], seuls les fichiers sont affichés, mais pas le dossier (CQ-4319543, NPR-36627).

* Les options de la barre d’outils sont différentes lorsque la même collection est sélectionnée dans un dossier et lorsqu’elle est sélectionnée à partir d’un résultat de recherche (NPR-36620).

* L’option [!UICONTROL Publication rapide] n’est pas disponible sur la page des résultats de recherche (NPR-36904, CQ-4317748).

* Lorsque les utilisateurs créent une Live Copy d’une ressource sans spécifier son extension, après téléchargement le fichier Live Copy n’est pas utilisable (NPR-36903, CQ-4326305).

* Lorsqu’un utilisateur est ajouté en tant que propriétaire d’un dossier enfant, il obtient l’autorisation du propriétaire de son dossier parent également, et donc des autres dossiers enfants du parent. En outre, l’utilisateur n’est pas supprimé en tant que propriétaire du dossier parent lors de sa tentative de suppression. (NPR-36801, CQ-4323737).

* [!DNL Experience Manager] génère une exception de mémoire insuffisante lorsque vous tentez de créer des sous-ressources pour des ressources composites, telles qu’une présentation PowerPoint (NPR-36668).

* Lorsque les utilisateurs déplacent une ressource déjà utilisée dans une page de sites publiée, la page de sites est de nouveau publiée même si l’option de publication n’est pas sélectionnée (NPR-36636, CQ-4323500).

* Lors de l’utilisation de la fonction de détection de type MIME Apache Tika, les ressources chargées à l’aide de la méthode `AssetManager.createAsset` laissent un fichier temporaire nommé `apache-tika-*.tmp` dans le répertoire temporaire. Ce fichier temporaire utilise tout l’espace disque disponible (NPR-36545).

* Toutes les ressources protégées par DRM sont téléchargées et la sélection de l’utilisateur pour télécharger une ressource spécifique n’est pas suivie (CQ-4327422).

* Impossible de faire glisser des ressources vers `pathfield` dans l’interface utilisateur (NPR-36849).

* Lorsque vous sélectionnez une ressource en mode Colonne, le panneau Détails de la ressource disparaît (NPR-36667).

### [!DNL Dynamic Media] {#dynamic-media-65100}

**Amélioration de l’accessibilité**

Les améliorations d’accessibilité suivantes sont disponibles dans [!DNL Dynamic Media Viewers].

* Les lecteurs d’écran narrent désormais le texte de l’espace réservé à rechercher et ajoutent l’adresse électronique comme champ obligatoire sur le partage de ressources sous forme de boîte de dialogue de lien, et annoncent également l’ [!UICONTROL info-bulle ] de ce champ (CQ-4327761).

* Les lecteurs d’écran indiquent désormais correctement les noms et les fins de différents champs dans l’ [!UICONTROL éditeur de paramètres d’image prédéfinis] lors de l’accès aux champs de l’interface utilisateur à l’aide du clavier (CQ-4325677).

* La sélection du clavier se déplace désormais correctement vers l’onglet de recherche de la boîte de dialogue [!UICONTROL Paramètres prédéfinis de la visionneuse] à partir du sélecteur de ressources de l’option [!UICONTROL Type de média enrichi] (CQ-4324736).

* Lorsque vous naviguez en mode formulaires à l’aide des touches du clavier, les lecteurs d’écran indiquent les libellés correspondant aux options d’incrémentation et de décrémentation sur l’onglet [!UICONTROL Créer] des [!UICONTROL Paramètres d’image prédéfinis] (CQ-4323900).

* Les lecteurs d’écran annoncent maintenant l’option [!UICONTROL Rechercher et ajouter l’adresse électronique] dans la boîte de dialogue Partager des ressources sous forme de lien (CQ-4323352).

* La sélection du clavier est conservée dans la barre d’outils lors de la navigation dans des ressources à l’aide des touches du clavier (CQ-4322037).

* Les lecteurs d’écran narrent maintenant les informations de champ [!UICONTROL Modifier] nouvellement ajoutées après avoir sélectionné l’option [!UICONTROL Ajouter un recadrage] dans la page [!UICONTROL Recadrage d’image réactive] de [!UICONTROL Modifier le profil de traitement d’image] (CQ-4290734).

* Sur les pages [!UICONTROL Modifier le paramètre d’image prédéfini] et [!UICONTROL Créer une vidéo interactive], les lecteurs d’écran annoncent désormais correctement l’en-tête de la page lors de la navigation dans les pages à l’aide des raccourcis clavier de titre (CQ-4290730)(CQ-4290701).

* Les lecteurs d’écran peuvent désormais reconnaître les différentes régions de l’écran (par exemple, la région du panneau de droite, le panneau de gauche, la barre d’outils d’action, le repère de la barre d’outils de la visionneuse et le repère d’image agrandie) à l’aide des raccourcis clavier de repère et de région lors de la navigation dans les pages suivantes.

   * [!UICONTROL Éditeur de paramètres prédéfinis de la visionneuse]  (CQ-4290729)

   * [!UICONTROL Éditeur de visionneuse d’images]  (CQ-4290710)

   * [!UICONTROL Création d’une vidéo interactive]  (CQ-4290702).

* Les lecteurs d’écran annoncent maintenant le nom de l’option de partage dans le cadre vidéo, lorsque vous naviguez à l’aide de la touche fléchée vers le bas (CQ-4290728).

* Les lecteurs d’écran indiquent désormais les noms de différentes options dans les onglets [!UICONTROL Sprite] et [!UICONTROL Arrière-plan] de l’onglet [!UICONTROL Apparence] dans [!UICONTROL Éditeur de paramètres prédéfinis de la visionneuse] (CQ-4290727).

* Les champs obligatoires, comme le champ pour modifier [!UICONTROL Largeur], dans l’onglet [!UICONTROL De base] de la page [!UICONTROL Modifier le codage vidéo] ont désormais un symbole d’astérisque (*) (CQ-4290725).

* Les lecteurs d’écran annoncent maintenant le libellé des options sur la page [!UICONTROL Profils d’image] (CQ-4290723).

* Les utilisateurs de Windows peuvent désormais naviguer hors de l’éditeur CSS développé sur [!UICONTROL Éditeur de paramètres prédéfinis de visionneuse] lorsque l’accent est mis sur l’éditeur CSS (CQ-4290720).

* Sous l’onglet [!UICONTROL Simple] de [!UICONTROL Modifier le paramètre d’image prédéfini] lors de la navigation en mode Formulaire, les lecteurs d’écran narrent désormais les libellés des différents champs et options de modification (CQ-4290717).

* Les lecteurs d’écran indiquent désormais le rôle et l’état (sélectionné ou non) des options de l’interface utilisateur dans le volet de navigation de gauche de la page de détails des ressources (CQ-4290709).

* Les lecteurs d’écran indiquent désormais correctement l’état (sélectionné ou non) et le lien pour les bascules d’image dans l’onglet [!UICONTROL Contenu] de la page [!UICONTROL Créer une vidéo interactive] (CQ-4290707).

* Les lecteurs d’écran indiquent désormais correctement le nom, le rôle et l’état des différents segments dans l’échelle de la chronologie vidéo lors de la navigation à l’aide de la touche fléchée vers le bas sur la page [!UICONTROL Créer une vidéo interactive] (CQ-4290706).

* Les lecteurs d’écran indiquent désormais le nom, le rôle et l’état par défaut (sélectionné ou non) et la propriété lors de la navigation dans les options de la page [!UICONTROL Créer une vidéo interactive] (CQ-4290704).

* Les lecteurs d’écran indiquent maintenant le nom, le rôle et l’état par défaut des options dans [!UICONTROL Toutes les ressources] et [!UICONTROL Toutes les collections] lors de la navigation dans la page [!UICONTROL Publier] (CQ-4290705).

* Lorsque vous téléchargez un format vidéo non pris en charge (autre que MP4) sur la page [!UICONTROL Créer une vidéo interactive] , Experience Manager affiche et affiche des messages d’erreur (CQ-4290700).

* Le contraste des nombres (temps en secondes) dans l’échelle de la chronologie sur la page [!UICONTROL Créer une vidéo interactive] répond désormais au rapport de luminosité minimal requis, de sorte que les utilisateurs avec une perception limitée des couleurs peuvent facilement lire (CQ-4290699).

* Les lecteurs d’écran indiquent maintenant le libellé du champ [!UICONTROL Nom du produit] lors de la navigation dans la page [!UICONTROL Créer une vidéo interactive] (CQ-4290697).

**Problèmes résolus**

Les correctifs suivants sont disponibles dans [!DNL Dynamic Media].

* Téléchargement de vidéos vers [!DNL Experience Manager] affichage `Process failed` après l’activation du mode d’exécution `dynamicmedia_scene7` et la synchronisation est désactivée (CQ-4327791).

### Plate-forme {#platform-65100}

Les améliorations suivantes ont été apportées à ce Service Pack :

* Lorsqu’un utilisateur sélectionne un élément dans la vue Arborescence, les lecteurs d’écran annoncent la sélection et les options de la barre d’outils affichées en haut (NPR-36504).
* Certains noms de texte et de contrôle sont plus faciles à lire pour les utilisateurs ayant des problèmes de vision, car le rapport de luminosité respecte le ratio minimal requis de 4,5:1 (NPR-36503).
* Lorsqu’un utilisateur utilise les commandes de calendrier, le lecteur d’écran indique la date descriptive, le mois et le jour de la semaine. Lorsqu’un utilisateur utilise la touche de raccourci du calendrier, le lecteur d’écran indique le changement de date, de mois et d’année (NPR-36498).
* Prise en charge de l’exécution de code JavaScript personnalisé `Clientlibs` à l’aide des fonctionnalités ECMAScript 6 sans respecter le mode strict. Plus précisément, l’indicateur `emitUseStrict` est ajouté à la balise `GCCScriptProcessor` (NPR-36411).

Les correctifs suivants font partie de ce Service Pack :

* Les contrôles d’intégrité personnalisés s’exécutent plus fréquemment que prévu (NPR-36985).
* La méthode `Resourceresolver map` renvoie un résultat incorrect pour les pages d’alias (NPR-36767).
* [!DNL Experience Manager] Le démarrage est retardé en raison des workflows de chargement (NPR-36615).

### Intégrations {#integrations-65100}

* Experience Manager ne répond plus lorsque le Principal noeud MongoDB passe à un autre noeud (NPR-36566).
* [!DNL Sling content distribution] échoue lors de l’opération de suppression des membres de la collection (NPR-36521, CQ-4323578).

### Interface utilisateur {#user-interface-65100}

* Le panneau latéral **[!UICONTROL Références]** n’affiche pas les références de ressources et de site (GRANITE-35078, GRANITE-34892).

### Projets de traduction {#translation-65100}

* Des sous-pages supplémentaires dans une copie de langue d’un projet à plusieurs traductions sont supprimées (NPR-36622).

### Workflow {#workflow-65100}

* Si le serveur reçoit un message d’absence du bureau, il signale des alertes de mémoire et cesse de répondre (NPR-36768).

### [!DNL Communities] {#communities-65100}

* Les pages du site de la communauté s’ouvrent dans l’état `LoggedIn` pour les utilisateurs invités anonymes (NPR-36908).

* S’il y a plusieurs pages dans la page **[!UICONTROL Communauté]** > **[!UICONTROL Idées]** > **[!UICONTROL Commentaires]**, la navigation de la page ne fonctionne pas (NPR-36541).

<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65100}

*
-->

### [!DNL Forms] {#forms-65100}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] publie les packages de modules complémentaires une semaine après la date de publication prévue du Service Pack [!DNL Experience Manager].


**Formulaires adaptatifs**

* Si les validations effectuées sur les valeurs de champ dans un formulaire adaptatif sont réussies, [!DNL AEM Forms] ne parvient pas à appeler le modèle de données de formulaire (CQ-4325491).

* Lorsque vous ajoutez un dictionnaire de langue à un projet de traduction, puis ouvrez le projet, [!DNL AEM Forms] affiche un message d’erreur (CQ-4324933) :

   ```TXT
   Uncaught TypeError: Cannot read property 'PROJECT_LISTING_PATH' of undefined
   at openButtonClickHandler (clientlibs.js:245)
   at HTMLButtonElement.onclick (clientlibs.js:258)
   ```

* Problèmes de performance après l’installation de [!DNL AEM Forms] Service Pack 7 (CQ-4326828).

**Correspondence Management**

* Retardez l&#39;affichage des caractères dans l&#39;onglet [!UICONTROL Données] ainsi que dans l&#39;aperçu de la lettre HTML (NPR-37020).

* Lorsque vous modifiez un fragment de document texte, les nouveaux mots s’affichent sous forme de balises HTML après l’enregistrement du fragment (NPR-36837).

* Impossible d’afficher les lettres enregistrées en tant que brouillons (NPR-36816).

* Lorsque vous modifiez un fragment de document texte, puis affichez l’aperçu de la lettre, AEM Forms affiche la langue de l’expression dans l’aperçu de lettre HTML (CQ-4322331).

* Problèmes lors du rendu des données avec un modèle de lettre en libre-service (NPR-37161).


**Communications interactives**

* Un caractère d’onglet duplique entre deux mots chaque fois que vous imprimez l’aperçu d’une communication interactive après la modification d’un fragment de document texte (NPR-37021).

* [!DNL AEM Forms] affiche une erreur lorsque vous enregistrez un fragment de document texte qui dépasse la limite de taille maximale (NPR-36874).

* Lorsque vous ajoutez une image à une communication interactive, un bloc vide supplémentaire s’affiche après l’image (NPR-36659).

* Lorsque vous sélectionnez tout le texte d’un éditeur, vous ne pouvez pas remplacer le texte de police par Arial (NPR-36646).

* Lorsque vous créez une URL dans un éditeur et que vous prévisualisez les modifications, un arrière-plan noir s’affiche à la place du texte de l’URL (NPR-36640).

* Lorsque vous copiez et collez du texte dans un éditeur, des problèmes se produisent lors de la modification de la police en Arial pour les puces disponibles dans le document (NPR-36628).

* Problèmes de mise en retrait des puces dans l’éditeur de texte (NPR-36513).

**Designer**

* Le Reader d’écran ne parvient pas à lire les données de champ flottant placées dans le libellé de texte sur la page de Principal ou sur les pages de sous-formulaire dans un PDF dynamique (CQ-4321587).

**Services de document**

* Lorsque vous convertissez des fichiers XDP en fichiers PDF, puis assemblez le PDF résultant, les générations PDF échouent et affichent le message d’erreur suivant :

   ```TXT
   Caused by: com.adobe.fd.assembler.client.AssemblerException$ClientException: Document is in a disposed state!
   ```

**Processus des formulaires**

* Impossible d’envoyer un formulaire à un processus Workbench après la mise à niveau vers AEM Forms Service Pack 8 (CQ-4325846).

**Formulaires HTML5**

* Lorsque vous définissez la valeur de la propriété `mfAllowAttachments` sur `True` dans le référentiel CRX DE, la balise `dataXml` est corrompue lors de l’envoi du formulaire HTML5 (NPR-37035).

* Lorsque vous effectuez le rendu d’un XDP au format HTML à l’aide de `dataXml`, [!DNL AEM Forms] affiche une erreur `Page Unresponsive` (NPR-36631).

### Commerce {#commerce-65100}

* La valeur du champ **[!UICONTROL Publié par]** affichée est incorrecte dans le mode Colonne (NPR-36902).
* Lorsqu’un catalogue est déployé, les nouveaux produits sont incorrectement marqués comme produits modifiés (NPR-36666).
* Lorsque vous recréez un produit supprimé, la page du produit n’est pas recréée (NPR-36665).
* Les pages modifiées sont mises à jour, mais les produits liés correspondants ne sont pas mis à jour lors du déploiement du catalogue (CQ-4321409, NPR-36422).
* Les workflows **[!UICONTROL Publier ultérieurement]** et **[!UICONTROL Annuler la publication ultérieurement]** ne fonctionnent pas (CQ-4327679).

Pour plus d’informations sur les mises à jour de sécurité, voir [[!DNL Experience Manager] page des bulletins de sécurité](https://helpx.adobe.com/security/products/experience-manager.html).

## Installation de la version 6.5.10.0 {#install}

**Configuration des exigences et informations supplémentaires**

* Experience Manager 6.5.10.0 nécessite Experience Manager 6.5. Voir la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées.
* Le téléchargement du Service Pack est disponible sur l’Adobe [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Sur un déploiement avec MongoDB et plusieurs instances, installez Experience Manager 6.5.10.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.

>[!NOTE]
>
>Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Adobe Experience Manager] 6.5.10.0.

### Installation du Service Pack {#install-service-pack}

Pour installer le Service Pack sur une instance [!DNL Adobe Experience Manager] 6.5, procédez comme suit :

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou une nouvelle sauvegarde de votre instance [!DNL Experience Manager].

1. Téléchargez le Service Pack à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip).

1. Ouvrez Package Manager et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package. Pour en savoir plus, voir [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du Service Pack, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Voir [Entrepôt de données Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois pendant l’installation du Service Pack. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans le navigateur [!DNL Safari], mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Il existe deux manières d’installer automatiquement [!DNL Experience Manager] 6.5.10.0 sur une instance de travail :

A. Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.

B. Utilisez l’API [HTTP du gestionnaire de modules](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` pour que les packages imbriqués soient installés.

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0 ne prend pas en charge l’installation de Bootstrap.

**Validation de l’installation**

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.10.0)` sous [!UICONTROL Produits installés].

1. Tous les lots OSGi sont **[!UICONTROL PRINCIPAL]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utiliser la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.3 ou ultérieure (Utiliser la console web : `/system/console/bundles`).

Pour connaître les plates-formes certifiées pour fonctionner avec cette version, voir les [exigences techniques](/help/sites-deploying/technical-requirements.md).

### Installation du module complémentaire Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignorez si vous n’utilisez pas Experience Manager Forms. Les correctifs dans Experience Manager Forms sont fournis par le biais d’un module complémentaire distinct une semaine après la publication du Service Pack [!DNL Experience Manager] planifiée.

1. Vérifiez que vous avez installé le Service Pack Adobe Experience Manager.
1. Téléchargez le module complémentaire Forms correspondant répertorié dans les [versions AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) pour votre système d’exploitation.
1. Installez le module complémentaire Forms comme décrit dans [Installation des modules complémentaires AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 comprend une nouvelle version du [module de compatibilité AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). Si vous utilisez une ancienne version du module de compatibilité AEM Forms et que vous effectuez une mise à jour vers Experience Manager 6.5.10.0, installez la dernière version du module après installation du module complémentaire Forms.

### Installation d’Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’Adobe Experience Manager Forms on JEE sont fournis via un programme d’installation distinct.

Pour plus d’informations sur l’installation du programme d’installation cumulatif pour Experience Manager Forms on JEE et la configuration après le déploiement, consultez les [notes de mise à jour](jee-patch-installer-65.md).

>[!NOTE]
>
>Après avoir installé le programme d’installation cumulatif pour Experience Manager Forms on JEE, installez le dernier module complémentaire Forms, supprimez le module complémentaire Forms du dossier `crx-repository\install` et redémarrez le serveur.


### UberJar {#uber-jar}

UberJar pour Experience Manager 6.5.10.0 est disponible dans le [référentiel central Maven](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/).

Pour utiliser UberJar dans un projet Maven, voir [Comment utiliser UberJar](/help/sites-developing/ht-projects-maven.md) et inclure la dépendance suivante dans le POM de votre projet :

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.10</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Maven Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier`, avec `apis` comme valeur, pour la balise `dependency`.

## Fonctionnalités obsolètes {#removed-deprecated-features}

Vous trouverez ci-dessous une liste des fonctionnalités marquées comme obsolètes avec la version [!DNL Experience Manager] 6.5.7.0. Les fonctionnalités sont marquées comme obsolètes initialement et supprimées ultérieurement dans une version ultérieure. Une autre option est fournie.

Vérifiez si vous utilisez une fonctionnalité ou une fonctionnalité dans un déploiement. En outre, envisagez de modifier la mise en oeuvre afin d’utiliser une autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’écran de souscription d’AEM Cloud Services ]**est obsolète car l’intégration [!DNL Experience Manager] et [!DNL Adobe Target] est mise à jour dans Experience Manager 6.5. L’intégration prend en charge l’API Adobe Target Standard.**[!UICONTROL  L’API utilise l’authentification via Adobe IMS et [!DNL Adobe I/O] et prend en charge le rôle croissant d’Adobe Launch pour instrumenter les [!DNL Experience Manager] pages à des fins d’analyse et de personnalisation. L’assistant de souscription n’a aucune utilité sur le plan fonctionnel. | Configurez les connexions système, l’authentification IMS par Adobe et les intégrations [!DNL Adobe I/O] via les services cloud [!DNL Experience Manager] respectifs. |
| Connecteurs | Adobe JCR Connector for Microsoft® SharePoint 2010 et Microsoft® SharePoint 2013 est obsolète pour Experience Manager 6.5. | N/A |

## Problèmes connus {#known-issues}

* (Pour JBoss sous Microsoft Windows uniquement) Pour continuer à utiliser le service Create PDF sur [!DNL AEM Forms on JEE], téléchargez [omniORB_4.1.1_x86_win32_vc10.zip](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/omniORB_4.1.1_x86_win32_vc10.zip) à partir de Distribution logicielle, extrayez et copiez le dossier disponible dans le fichier Zip à l’emplacement suivant :
   `[AEM Forms Installation]\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\CommonNatives\lib`

* [!DNL Microsoft Windows Server 2019] ne prenant pas en charge [!DNL MySQL 5.7] et [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] ne prend pas en charge les installations clé en main pour [!DNL AEM Forms 6.5.10.0].

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de la version 6.5 vers la version 6.5.10.0, vous pouvez afficher les exceptions `RRD4JReporter` dans le fichier `error.log`. Pour résoudre le problème, redémarrez l’instance.

* Si vous installez [!DNL Experience Manager] 6.5 Service Pack 10 ou un Service Pack précédent sur [!DNL Experience Manager] 6.5, la copie d’exécution du modèle de workflow personnalisé de vos ressources (créée dans `/var/workflow/models/dam`) est supprimée.
Pour récupérer votre copie d’exécution, Adobe recommande de synchroniser la copie d’heure de conception du modèle de workflow personnalisé avec sa copie d’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie de [!DNL Assets] et publier un dossier imbriqué sur [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] tant que le dossier racine n’a pas été republié.

* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation de Experience Manager 6.5.x.x :
   * &quot;Lorsque l’intégration d’Adobe Target est configurée dans Experience Manager à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Dynamic Media n’est pas visible lors de la prévisualisation de la ressource via la visionneuse de bannières Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Délai d’attente avant que la modification du reg ne soit terminée sans enregistrement.

## Lots OSGi et packages de contenu inclus {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans [!DNL Experience Manager] 6.5.10.0 :

* [Liste des lots OSGi inclus dans Experience Manager 6.5.10.0](assets/65100_bundles.txt)

* [Liste des packages de contenu inclus dans Experience Manager 6.5.10.0](assets/65100_packages.txt)

## Sites web à accès limité {#restricted-sites}

Ces sites web ne sont disponibles que pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* Voir [Comment contacter l’assistance clientèle d’Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notes de mise à jour de la version 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] page produit](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentation 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)

