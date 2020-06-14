---
title: Notes de mise à jour d’Adobe Experience Manager 6.5 Previous Service Pack
description: Notes de mise à jour spécifiques à Adobe Experience Manager 6.5 Service Pack 3 et versions antérieures.
contentOwner: AK
translation-type: tm+mt
source-git-commit: d7276f332bece4f736d92e5723d79ffc2d27e900
workflow-type: tm+mt
source-wordcount: '8093'
ht-degree: 36%

---


# Correctifs et packs de fonctionnalités inclus dans les packs de service précédents {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0 est une mise à jour importante qui comprend de nouvelles fonctionnalités, les améliorations et les performances des clients clés, la stabilité et les améliorations de sécurité, publiée depuis la version 6.5 d’ **avril 2019**. Il peut être installé sur Adobe Experience Manager 6.5.

Voici quelques-unes des principales fonctionnalités et améliorations introduites dans Adobe Experience Manager 6.5.4.0 :

* Adobe Experience Manager Assets est désormais configuré avec Brand Portal via Adobe I/O Console.

* Une nouvelle étape [Générer une sortie](../forms/using/aem-forms-workflow-step-reference.md) imprimable est désormais disponible pour les workflows Adobe Experience Manager Forms.

* [Prise en charge](../forms/using/resize-using-layout-mode.md) de plusieurs colonnes pour le mode de mise en page des formulaires adaptatifs et des communications interactives.

* Prise en charge du texte [](../forms/using/designing-form-template.md) enrichi dans les formulaires HTML5.

* [Améliorations](new-features-latest-service-pack.md#accessibility-enhancements) de l’accessibilité dans les ressources d’Experience Manager.

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.10.8.

* Vous pouvez désormais synchroniser des sous-arborescences de contenu sélectif en mode *Contenu* dynamique - Scene7 plutôt que de toutes les sous-arborescences disponibles dans `content/dam`.

* L’intégration du modèle de données de formulaire avec le service Web SOAP prend désormais en charge les groupes de choix ou les attributs sur les éléments.

* L’entrée ou la sortie SOAP et les structures de données complexes prennent désormais en charge la substitution de groupe dynamique.

Pour obtenir une liste complète des fonctionnalités et des points saillants présentés dans les derniers Service Packs, reportez-vous à la page [Nouveautés des Service Packs](new-features-latest-service-pack.md)Adobe Experience Manager 6.5.

### Sites {#sites-fixes}

* Lorsqu’une URL de pages de sites Adobe Experience Manager contient un deux-points (`:`) ou un symbole de pourcentage (`%`), le navigateur cesse de répondre et les pics d’utilisation du processeur (NPR-32369, NPR-31918).

* Lorsqu’une page Sites Experience Manager est ouverte pour modification et qu’un composant est copié, l’action de collage reste indisponible pour certains espaces réservés (NPR-32317).

* Lorsque l’assistant Gérer la publication est ouvert, un fragment d’expérience lié à un composant principal n’est pas affiché dans les listes des références publiées (NPR-32233).

* Le rendu d’un aperçu de la copie en direct dans l’interface utilisateur tactile prend beaucoup plus de temps que celui de l’interface utilisateur classique (NPR-32149).

* Lorsque l’heure du serveur et l’heure de la machine se trouvent dans des fuseaux horaires différents, l’heure de publication planifiée affiche l’heure du serveur dans l’interface utilisateur tactile, tandis que dans l’interface utilisateur classique, l’heure de la machine s’affiche (NPR-32077).

* Les sites Experience Manager ne parviennent pas à ouvrir une page avec un suffixe dans l’URL (NPR-32072).

* Lorsqu’un utilisateur modifie un fragment de contenu, une variante supprimée du fragment de contenu est restaurée (NPR-32062).

* Les utilisateurs sont autorisés à enregistrer un fragment de contenu sans fournir aucune information dans les champs requis (NPR-31988).

* kernel.js et ui.js ne sont ni préappliqués ni mis en cache. Cela allonge le temps de rendu des pages (NPR-31891).

* Lorsque PageEventAuditListener est activé, la longueur de la file d&#39;attente de validation augmente. Elle influe sur les performances de nombreuses opérations telles que la publication en masse, la navigation, le mouvement des actifs en vrac (NPR-31890).

* Lorsque vous faites glisser des fragments d’expérience, un temps de réponse élevé est observé (NPR-31878).

* Lorsque vous sélectionnez l’option Faire glisser le composant ici dans l’espace réservé d’une grille réactive, une requête GET est envoyée et la requête génère une erreur HTTP 403 (NPR-31845).

* Lorsque vous déplacez le contenu dans le même dossier, l’option de déplacement de page est désactivée (NPR-31840).

* En mode de structure des modèles modifiables, la liste des composants autorisés dans le conteneur de mise en page affiche des résultats incorrects. Seuls les composants contenant une boîte de dialogue de conception s’affichent dans le conteneur de mise en page (NPR-31816).

* Lorsqu’une page dispose d’autorisations en lecture seule pour un utilisateur, l’option Ouvrir les propriétés est visible dans sites.html mais pas dans editor.html (NPR-31770).

* Lorsqu’un utilisateur clique sur le bouton Créer, l’option de page n’est pas disponible (NPR-31756).

* Impossible de synchroniser la campagne dans la campagne Adobe contenant le composant d&#39;importateur de conception prête à l&#39;emploi (prêtes à l&#39;emploi) (NPR-31728).

* Lorsque vous essayez de changer une liste à puces en liste numérotée, seuls les deux premiers éléments de la liste sont modifiés (NPR-31636).

* Lorsqu’une page n’est pas créée et que le noeud enfant est sélectionné, la boîte de dialogue de sélection affiche toujours le noeud initial. Lorsque la page est créée et que l’utilisateur clique sur Parcourir, la page est redirigée vers le noeud racine au lieu du noeud créé (NPR-31618).

* La boîte de dialogue de configuration de la vue ne fonctionne pas correctement pour la fonction de personnalisation de la boîte de réception (NPR-32503 et NPR-32492).

* Un message d’erreur s’affiche lors de l’affichage des informations de processus à l’aide de la boîte de réception (CQ-4282168).

### Ressources {#assets-6540-enhancements}

* Le bouton permettant de déclencher le processus sur la page de collecte des ressources est désactivé (NPR-32471).

* Un dossier sans nom est créé dans SPS (Scene7 Publishing System) lors du déplacement d’un fichier d’un dossier à un autre dans Experience Manager avec la configuration de Contenu multimédia dynamique Scene7 (NPR-32440).

* L&#39;action de déplacement de tous les actifs (à l&#39;aide de Sélectionner tout, puis de déplacer) vers un dossier contenant les actifs publiés échoue avec une erreur (NPR-32366).

* La génération de rendu pour les ressources dont ${extension} a échoué (NPR-32294).

* Les URL d’historique des versions s’affichent sous le champ Référencé par sur la page de propriétés des ressources (NPR-31889).

* Impossible d&#39;ouvrir le fichier ZIP téléchargé à partir de DAM à l&#39;aide de WinZip (NPR-32293).

* Les autorisations d’origine d’un dossier sont mises à jour lorsque les paramètres du dossier sont ouverts pour modifier le titre du dossier ou l’image miniature, puis enregistrés (NPR-32292).

* L&#39;icône de calendrier pour l&#39;activation planifiée ne s&#39;affiche pas dans la colonne État (dans l&#39;interface utilisateur classique de la liste des ressources DAM) pour les ressources dont l&#39;activation est planifiée pour une date et une heure ultérieures (NPR-32291).

* La création d’extraits de code à l’aide de modèles de fragments de code génère des erreurs lors de la recherche de collections au cours du processus de création d’extraits de code (NPR-32290).

* Plusieurs requêtes de recherche sont déclenchées lorsque plusieurs balises sont sélectionnées à partir du filtre de recherche (NPR-32143).

* L’interface utilisateur Ressources d’Experience Manager affiche les noms de fichier tronqués lorsque des fichiers contenant plus de 50 caractères sont téléchargés (NPR-32054).

* Toutes les cases à cocher du panneau Filtre sont désactivées lorsque les première et deuxième cases à cocher sont désactivées, lorsque les cases de niveau 2 de l’arborescence des cases à cocher de Adobe Stock ont été sélectionnées (NPR-31919).

* La recherche de fichiers et de dossiers à l&#39;aide des facettes Omnisearch fait exception (NPR-31872).

* La mise en surbrillance des champs pour la sélection obligatoire des champs dans l’éditeur de métadonnées n’est pas supprimée, même après la sélection du champ requis, lorsque les règles de dépendance sont définies dans le schéma de métadonnées correspondant (NPR-31834).

* Les noms complets des balises de niveau feuille (issus de la hiérarchie des balises) ne s’affichent pas dans la page Propriétés de la ressource (NPR-31820).

* L’utilisation de la commande Précédent de la page Propriétés de la ressource sur le navigateur Safari génère une erreur (NPR-31753).

* La page de résultats de la recherche tactile dans l&#39;interface utilisateur (effectuée via Omnisearch) défile automatiquement vers le haut et perd la position de défilement de l&#39;utilisateur (NPR-31307).

* La page des détails des ressources des fichiers PDF n’affiche pas les boutons d’action, à l’exception des boutons Collecte et Ajouter le rendu dans Experience Manager s’exécutant en mode d’exécution Contenu multimédia dynamique Scene7 (CQ-4286705).

* Le traitement des fichiers prend trop de temps lors du transfert par lot de Scene7 (CQ-4286445).

* Le bouton Enregistrer n’importe pas la visionneuse à distance lorsque l’utilisateur n’a apporté aucune modification à l’éditeur de visionneuses dans le client de média dynamique (CQ-4285690).

* La miniature de fichier 3D n’est pas instructive lorsqu’un modèle 3D pris en charge est imbriqué dans Experience Manager (CQ-4283701).

* L’état non traité du paramètre prédéfini de visionneuse de vidéos de recadrage dynamique s’affiche deux fois sur la bannière en regard du nom du paramètre prédéfini (CQ-4283517).

* Une hauteur de conteneur incorrecte d’un modèle 3D téléchargé prévisualisé dans la visionneuse 3D est observée sur la page de détails de la ressource (CQ-4283309).

* L’éditeur de carrousel ne s’ouvre pas dans IE 11 en mode hybride Contenu multimédia dynamique Experience Manager (CQ-4255590).

* La sélection du clavier est bloquée dans la liste déroulante Courriel dans la boîte de dialogue Télécharger, dans les navigateurs Chrome et Safari (NPR-32067).

* La case à cocher Synchroniser tout le contenu n’est pas activée par défaut lors de la tentative d’ajout de la configuration de DM cloud sur Experience Manager (CQ-4288533).

### Interface utilisateur de la fondation {#foundation-ui-6540}

* Le contrôle de la souris passe au champ de filtre précédent au lieu de rester dans le champ de filtre existant lors de la recherche de fichiers à l’aide du panneau Filtre (NPR-32538).

* Balisage de plateforme : La recherche de balises en saisissant des balises dans les champs de balise affiche des balises en dehors des limites racines et ne respecte pas la propriété `rootPath` des champs de balise (NPR-31895).

* Interface utilisateur de la plate-forme : Le navigateur de chemins est rompu si un chemin non valide est ajouté dans le champ de texte (NPR-31884).

* La notification est masquée derrière un menu collant lors de la sélection de la page (NPR-31628).

### Plate-forme {#platform-sling-6540}

* (HTL) Les traits de soulignement remplacent les deux-points dans la section de chemin de l’URL (NPR-32231).

### Projets {#projects-6540}

* Le bouton Créer n’est pas visible pour l’utilisateur, même s’il est autorisé à créer un projet dans le sous-dossier (NPR-31832).

### Traduction de projets {#projects-translation-6540}

* La création du projet de traduction rompt l’interface utilisateur lorsque l’option Rogner les espaces est activée dans `Apache Sling JSP Script Handler` (NPR-32154).

* Une erreur survient dans l’interface utilisateur et l’exception de point Null dans les journaux d’erreurs lorsqu’une balise, à traduire, est ajoutée à un projet de traduction (NPR-31896).

### Intégrations {#integrations-6540}

* La génération d’URL de bibliothèque de lancement repose uniquement sur `path` les valeurs et les valeurs de l’API de lancement et n’est pas basée sur `library_name` `library_path` la valeur (NPR-31550).

* Un message d’erreur s’affiche lors du traitement des éléments liés à LiveFyre (FYR-12420).

* ReportSuitesServlet est vulnérable au SSRF (NPR-32156).

### Editeur de modèle WCM {#wcm-template-editor-6540}

* En mode de structure des modèles modifiables, la liste des composants autorisés dans le conteneur de mise en page n’affiche pas le composant de bouton de lien (CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* Une erreur s’est produite lors de la sélection d’une incrustation, puis de la sélection de composants de grille réactive Faites glisser les composants ici (CQ-4283342).

### Campaign Targeting {#campaign-targeting-6540}

* La configuration du cloud de Cible échoue avec l’erreur d’obtention de la demande de mbox (CQ-4279880).

### Brand Portal {#assets-brand-portal-6540}

* Brand Portal users are not able to publish contribution folder assets to [!DNL Assets] on upgrading to Adobe I/O on Experience Manager 6.5.4 (CQDOC-15655). For an immediate fix on Experience Manager 6.5.4, it is recommended to [download the hotfix](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) and install on your author instance.

* Les valeurs des fenêtres contextuelles de schéma de métadonnées ne sont pas visibles dans les propriétés des ressources (CQ-4283287).

* Le sous-schéma de métadonnées n’affiche pas les onglets basés sur le mimétype dans les propriétés de la ressource (CQ-4283288).

* L’annulation de la publication d’un schéma de métadonnées renvoie un message d’erreur bien que le schéma soit supprimé du serveur principal.

* L’image de Prévisualisation ne s’affiche pas pour un fichier publié (CQ-4285886).

* L’utilisateur ne peut pas publier ou annuler la publication de fichiers dont le nom contient un guillemet simple (CQ-4272686).

* Les termes et conditions ne s’affichent pas lors du téléchargement de plusieurs ressources (CQ-4281224).

* Des vulnérabilités mineures de sécurité ont été corrigées.

### Communities {#communities-6540}

* Le formulaire Créer un membre s’affiche en tant que page vierge (NPR-31997).

* L’utilisateur ne peut pas vue le rapport Analytics sur l’instance d’auteur (NPR-30913).

### Chêne - Indexation et Requêtes {#oak-indexing-6540}

* MS Word et MS Excel documents, contenant une image JPEG, lors de l&#39;analyse avec l&#39;analyseur Tika échouent à analyser et une erreur de classe introuvable est observée (NPR-31952).

### Formulaires {#forms-6540}

>[!NOTE]
>
>Le Service Pack d’Experience Manager n’inclut pas de correctifs pour Experience Manager Forms. Les correctifs sont fournis à l’aide d’un module complémentaire Forms distinct.  En outre, un programme d’installation cumulatif est publié, qui comprend des correctifs pour Adobe Experience Manager Forms sur JEE. Pour plus d’informations, voir [Installation du module complémentaire](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) Experience Manager Forms et [Installation d’Experience Manager Forms sur JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Correspondence Management : Les lettres affichent des caractères supplémentaires après envoi aux workflows de post-traitement (NPR-32626).

* Correspondence Management : Les lettres affichent une balise d’emplacement de liste déroulante en tant que composant de texte après envoi aux workflows de post-processus (NPR-32539).

* Correspondence Management : Les valeurs par défaut définies dans le modèle de lettre ne s’affichent pas en mode Prévisualisation (NPR-32511).

* Mobile Forms : Le bouton d’envoi s’affiche avec une taille développée lors du rendu d’un formulaire XDP dans une version HTML (NPR-32514).

* Document Services : Problèmes d&#39;accès aux URL pour les lettres et d&#39;autres pages après l&#39;application du Service Pack 2 (NPR-32508, NPR-32509).

* Document Services : Si le nombre de transactions sur un serveur dépasse une limite spécifique, la conversion HTML vers PDF échoue et les paramètres de type de fichier sont supprimés du [!DNL Forms] serveur (NPR-32204).

* Formulaires adaptatifs : L’outil d’accessibilité du navigateur signale des échecs dans les formulaires adaptatifs conformément aux directives WCAG2 Level AA (NPR-32312, NPR-32309, CQ-4285439).

* Formulaires adaptatifs : L’outil d’accessibilité du navigateur Chrome signale une erreur de bonne pratique (NPR-32310).

* Formulaires adaptatifs : Problèmes de traduction lors de la configuration d’un formulaire adaptatif incorporé à une page Sites Experience Manager (NPR-32168).

* Workbench : Un message d’erreur s’affiche lors de l’utilisation du service Get PDF Properties for PDF Utilities (NPR-32150).

* Sécurité du Document : Un fichier PDF protégé ne parvient pas à s&#39;ouvrir hors connexion avec l&#39;option DisableGlobalOfflineSynchronizationData définie sur True (NPR-32078).

* Designer : Si l’option de balisage est activée, la bordure du sous-formulaire disparaît dans la sortie PDF générée (NPR-32547, NPR-31983, NPR-31950).

* Designer : S’il existe des cellules fusionnées dans un tableau, le test d’accessibilité échoue pour le fichier PDF de sortie converti à partir d’un formulaire XDP à l’aide du service de sortie (CQ-4285372).

* Foundation JEE : Si un serveur Experience Manager Forms est déconnecté d’une grappe, des problèmes de mise en cache l’empêchent de se reconnecter au serveur (NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] La version 6.5.3.0 est une version importante qui comprend des améliorations et correctifs concernant les performances, la stabilité, la sécurité et les clients clés depuis la version 6.5 publiée en **avril 2019**. It can be installed on top of [!DNL Adobe Experience Manager] 6.5.

Les principaux points forts de cette version du Service Pack incluent les éléments suivants :

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.10.6.

* [!DNL Experience Manager Assets] prend désormais en charge les archives ZIP créées à l’aide de l’algorithme Deflate64.

* Une nouvelle colonne pour la date créée, qui peut être triée, a été ajoutée dans la vue de liste DAM et dans les résultats de la recherche de ressources dans la vue de liste.

* Le tri des ressources en fonction de la colonne Nom a été activé dans la vue de Liste.

* [!DNL Dynamic Media] prend désormais en charge les ressources vidéo de recadrage dynamique. Smart Crop est une fonction pilotée par l’apprentissage automatique qui recadre une vidéo tout en déplaçant le cadre pour suivre le point focal de la scène.

* [!DNL Dynamic Media] prend en charge l’imagerie intelligente.

* Capacité à [définir les préférences d’absence du bureau](../forms/using/configure-out-of-office-settings.md) dans [!DNL Experience Manager] les workflows.

* Possibilité de [partager des éléments](../forms/using/configure-shared-queues-osgi.md) de boîte de réception ou de boîte de réception avec d’autres utilisateurs dans [!DNL Experience Manager] des workflows.

* Capacité à [générer des communications interactives en mode](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Batch.

* Mise à jour de la version de jQuery fournie dans ContextHub à 3.4.1.

### Ressources {#assets-6530-enhancements}

**Améliorations apportées au produit**

* [!DNL Experience Manager Assets] prend désormais en charge les archives ZIP créées à l’aide de l’algorithme Deflate64 (NPR-27573).

* Une nouvelle colonne pour la date créée, qui peut être triée, est ajoutée dans la vue de liste DAM et sur les résultats de la recherche de ressources dans la vue de liste (NPR-31312).

* Dans la vue de liste, les utilisateurs peuvent trier la liste des ressources à l’aide de la colonne [!UICONTROL Nom] (NPR-31299).

* Les fichiers GLB, GLTF, OBJ et STL peuvent être prévisualisés dans la page Détails [!UICONTROL des] ressources dans DAM (CQ-4282277).

* `ReplicationOnModifyListener` Le événement est déclenché pour les noeuds de blocs pendant le téléchargement du bloc dans [!DNL Dynamic Media] (CQ-4281279).

* [!DNL Dynamic Media] prend désormais en charge les ressources vidéo de recadrage dynamique. Smart Crop est une fonction pilotée par l’apprentissage automatique qui recadre une vidéo tout en déplaçant le cadre pour suivre le point focal de la scène (CQ-4278995).

* [!DNL Dynamic Media] prend en charge l’imagerie intelligente (CQ-4222249).

* La vue de recherche ou de navigation est définie comme vue par défaut dans le sélecteur Foundation si les paramètres de requête sont transmis dans la requête (NPR-31601).

**Correctifs**

* Les métadonnées de certains documents PDF ne sont pas mises à jour et enregistrées au format PDF lorsque leur titre est modifié (NPR-31629).

* Le partage de ressources ne fonctionne pas pour une ressource dont le nom de fichier contient un caractère plus (`+`) (NPR-31547).

* Les modifications dans le formulaire de recherche par défaut Actifs Admin Search Rail ne fonctionnent pas comme prévu (NPR-31502).

* Les suggestions ne s&#39;affichent pas lors de l&#39;utilisation d&#39;Omnisearch sur la vue de ressources pour la recherche de ressources (NPR-31496).

* Les références de ressources dans les collections ne sont pas mises à jour lorsque les ressources référencées sont déplacées vers un autre emplacement, dans les cas où les mêmes ressources sont référencées par différentes collections par différents utilisateurs (NPR-31486).

* Les balises IPTC Duplicata sont ajoutées aux métadonnées de fichier (NPR-31328).

* Le nombre de résultats de la recherche n&#39;est pas mis à jour correctement lorsqu&#39;une recherche est déclenchée à partir du rail de filtre (NPR-31316).

* Toutes les cases à cocher sont désactivées lorsque vous désélectionnez les cases de second niveau dans le filtre Type de fichier et le texte de la barre de recherche n&#39;est pas synchronisé avec les propriétés sélectionnées ou désélectionnées (NPR-31287).

* Tous les membres (utilisateurs/groupes) ne peuvent pas être supprimés de la section Membres d&#39;un dossier ; lors de la tentative de suppression de tous les utilisateurs, l&#39;utilisateur connecté est ajouté à la liste (NPR-31171).

* Les fichiers dont le nom de fichier contient le symbole plus (`+`) ne peuvent pas être supprimés (NPR-31162).

* Le menu déroulant Créer, qui est visible dans le menu supérieur lors de la sélection d&#39;un dossier, n&#39;affiche pas &quot;Dossier&quot; comme option de création (NPR-30877).

* La sélection de dossier Créer > FichierTélécharger l’élément d’action est manquante lorsque l’ACL pour Refuser `jcr:removeChildNodes` et `jcr:removeNode` le chemin d’accès sont appliqués à un utilisateur (NPR-30840).

* Les workflows DAM sont obsolètes lorsque certains fichiers mp4 sont téléchargés, ce qui entraîne l’obsolescence de tous les workflows restants (NPR-30662).

* Une erreur de mémoire insuffisante est observée lorsqu’un fichier PDF volumineux (de plusieurs gigaoctets) est téléchargé vers DAM et que ses sous-ressources sont traitées (NPR-30614).

* Le mouvement en masse des ressources échoue et affiche un message d’avertissement (NPR-30610).

* Les noms des fichiers sont changés en minuscules lorsque vous déplacez des fichiers d’un dossier à un autre en [!DNL Experience Manager] mode [!DNL Dynamic Media]-Scene7 (NPR-31630).

* Une erreur est observée lors de la modification d’un ensemble d’images distant, pour l’image résidant dans le dossier portant le même nom que le nom de la société Scene7 (NPR-31340).

* [!DNL Dynamic Media] les ressources contenant des références ne sont pas publiées (NPR-31180).

* Les téléchargements du mode [!DNL Dynamic Media]7-Scene7 vers [!DNL Dynamic Media Classic] Scene7 prennent trop de temps à se terminer (NPR-31048).

* La zone réactive ajoutée à un fichier d’image n’est pas visible dans Interactive Image Viewer dans la page des détails du fichier (NPR-30979).

* D’immenses tâches de création d’un sling sont créées et la bannière de traitement réapparaît lorsque les actions effectuées sur des fichiers dans [!DNL Experience manager Assets] Scene7 sont transmises à Scene7 (NPR-30947).

* Un conflit se produit lors de la création de la copie de langue des fichiers et ceux-ci ne sont pas téléchargés vers Scene7 (NPR-30932).

* Les rendus dynamiques téléchargés depuis l’ [!DNL Experience Manager] exécution en mode [!DNL Dynamic Media]hybride sont rompus (ils sont de type texte avec un contenu &quot;impossible de trouver l’image&quot; au lieu du type de contenu d’image) (NPR-30876).

* [!DNL Dynamic Media] Le processus de codage vidéo ne parvient pas à générer une miniature pour la vidéo qui est migrée du mode [!DNL Dynamic Media Classic] vers [!DNL Dynamic Media]Scene7 sur Adobe Experience Manager (CQ-4282011).

* IpsApiException a été observé lors de la migration de fichiers d’une instance à une autre à l’aide de différents identifiants de société Scene7 (CQ-4280548).

* La miniature des ressources 3D n’est pas instructive lorsqu’un modèle 3D pris en charge est assimilé à [!DNL Experience Manager] (CQ-4283701).

* Les boutons de défilement s’affichent dans le lecteur si un fichier 3D comporte peu de vues d’appareil photo (CQ-4283322).

* Hauteur de conteneur incorrecte d’un modèle 3D téléchargé prévisualisé dans DimensionalViewer sur la page Détails du fichier (CQ-4283309).

* Les vidéos ne peuvent pas être lues avec SmartCropVideoViewer sur Internet Explorer 11 et Safari (CQ-4281422).

* L’utilisation du bouton de déplacement pour déplacer plusieurs fichiers d’un dossier à un autre échoue lors de l’ [!DNL Experience Manager] exécution en mode [!DNL Dynamic Media]-exécution Scene7 (CQ-4280384).

* Une vidéo déformée s’affiche sur les détails de la ressource lorsque le type MIME est autre que MP4 (CQ-4279704).

* Les vidéos nouvellement ingérées dans des dossiers avec profil vidéo restent en état de traitement même après que le pourcentage de codage se termine à 100 % (CQ-4279389).

* Le déplacement de fichiers à partir d’un dossier crée un grand nombre de tâches Sling (appels d’API Scene7) plus que ce qui est idéalement requis (CQ-4278664).

* Les noms des visionneuses d’images sont remplacés en minuscules dans Scene7, lorsque des visionneuses d’images (ou visionneuse de supports) sont créées et nommées avec la convention d’affectation de nom appropriée dans DAM (CQ-4281112).

* Scene7 Migrator définit incorrectement l’état de publication (CQ-4263492).

* La page de résultats de la recherche tactile dans l’interface utilisateur (effectuée via Omnisearch) défile automatiquement vers le haut et perd la position de défilement de l’utilisateur dans les fragments de contenu (CQ-4282898).

* Les fichiers PDF ne sont pas indexés et le contenu au sein de ne peut pas faire l’objet de recherches (CQ-4278916).

* Une erreur &quot;Groupe non répertorié par le sélecteur d’utilisateurs : la valeur &quot;false&quot; attendue est observée lors de l’ajout d’un groupe d’utilisateurs fermé avec des éléments différents `principalName` et `authorizableId` (CQ-4278177).

* La Vue de colonne de l’interface utilisateur des ressources affiche tous les chemins, quel que soit le chemin racine du barrage du client (CQ-4278175).

* La recherche du sélecteur de ressources ne fonctionne pas comme prévu (CQ-4275886).

* Les Workflows de rendu échouent (CQ-4271928).

* DAM Événement Purge supprime les dernières (`maxSavedActivities`) données de événement et contient les données créées précédemment (NPR-31336).

* La page de résultats de la recherche tactile dans l&#39;interface utilisateur (effectuée via Omnisearch) défile automatiquement vers le haut et perd la position de défilement de l&#39;utilisateur (NPR-31307).

* La barre d’actions et le nombre de ressources ne sont pas mis à jour lors de la sélection de tous les éléments, puis lors de la désélection de certains éléments (dossiers/fichiers individuels) dans l’interface utilisateur tactile (NPR-31118).

* Une exception s’affiche lors de l’interrogation [!DNL Experience Manager] des détails d’une tâche d’une ressource (CQ-4283569).

### Sites {#sites}

* Si l’héritage de LiveCopy est rompu, les pages de copie dynamique affichent des liens de copie de langue au lieu de liens LiveCopy (NPR-30980).
* Pour un nouveau plan directeur, si le nombre d&#39;enregistrements est supérieur à 40, seuls les 40 premiers enregistrements sont affichés. Le plan directeur affiche des lignes vierges pour le reste des enregistrements (NPR-31182).
* Lorsqu&#39;un utilisateur ajoute des caractères japonais ou coréens à la propriété description d&#39;un menu, celui-ci affiche des caractères déformés pour le texte en japonais et en coréen (NPR-31331).
* L’Editeur de texte enrichi (RTE) ne permet pas d’insérer un tableau incorporé en tant qu’élément de liste (NPR-30879).
* Editeur de texte enrichi (RTE) à l’échafaudage prêt à l’emploi. applique inopinément la taille de police en ligne aux éléments (NPR-31284).
* Lorsqu’un utilisateur se concentre sur les champs du rail gauche et utilise un raccourci clavier pour coller du contenu, il colle le le contenu du Presse-papiers de l’éditeur de page au lieu du contenu copié à partir des champs du rail gauche (NPR-31172).
* Lorsqu’un utilisateur ajoute un champ Téléchargement de fichier à un champ multichamp, le chemin d’accès à l’image est stocké dans le noeud de composant au lieu du noeud de champs multiples (NPR-30882).
* L’ `ResponsiveGridExporter` API ne renvoie pas `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` d’interface. Le `com.day.cq.wcm.foundation.model.impl` package est déclaré comme package privé (NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* Lorsqu’une page contenant certains fragments d’expérience est ouverte en mode non éditeur (dans Auteur sans préfixe et `editor.html` ou dans Editeur). La requête se termine en code d’erreur d’état HTTP `wcmmode=disabled``500` (NPR-30743).
* Les utilisateurs ne peuvent pas modifier leur mot de passe et accéder à leur page de profil (NPR-31161).

### Interface utilisateur et de recherche {#search-ui-interface}

* Lorsque vous passez de la vue de carte à la vue de liste sur une page de résultats de recherche, il y a un décalage avant que la page puisse être défilée (NPR-31286).

* La case à [!UICONTROL cocher Sélectionner tout] est masquée dans la vue de liste sur [!DNL Sites] l&#39;interface utilisateur (NPR-31614).

* Le nombre [!UICONTROL Sélectionner tout] sur une page de résultats de recherche est incorrect (NPR-31120).

* L’éditeur de métadonnées affiche les balises qui n’existent pas (NPR-31119).

### Traduction {#translation}

* Deux fenêtres contextuelles de calendrier s’affichent lorsque vous sélectionnez l’option Échéance dans une tâche de traduction (NPR-31270).

### Plate-forme {#platform}

* L&#39;option de type Mime dans la console Web ne fonctionne pas (NPR-31108).

* Le certificat client n&#39;est pas accepté lors de la configuration de la connexion unique (NPR-31165).

* Les mises à jour de la configuration de la taille de la mémoire tampon pour le service HTTP basé sur Jetty ne sont pas enregistrées (NPR-30925).

* QueryBuilder prend désormais en charge orderby ``fn:name()`` dans les requêtes xpath (NPR-31322).

* L&#39;arborescence des activations de Duplicata est créée lors de la mise à niveau à partir de la version [!DNL Experience Manager] 6.3 (NPR-31513).

* Les requêtes transférées ne conservent pas les en-têtes de réponse définis lors de l’authentification sling (NPR-30013).

* La recherche dans les composants du sélecteur ne fonctionne pas (NPR-31692).

* Une erreur s’affiche lorsque vous joignez un fichier ZIP à une [!DNL Experience Manager Communities] publication en raison de différentes versions d’Apache POI et du lot Apache Tika (NPR-31018).

* Le ``org.apache.sling.distribution.api`` lot est masqué dans le gestionnaire de configuration et n’est donc pas disponible pour les lots personnalisés (NPR-31720).

### Projets {#projects}

* La permutation des vues de calendrier ne fonctionne pas (NPR-31271).

### Brand Portal {#assets-brand-portal-6530}

**Améliorations apportées au produit**

* Le processus d’importation d’origine des ressources dans [!DNL Experience Manager Assets] est modifié afin de récupérer uniquement les ressources nouvellement créées de [!DNL Brand Portal] dans [!DNL Experience Manager]et d’ignorer les ressources qui existent déjà dans le dossier NEW pour éviter la réplication (CQ-4278527).

**Correctifs**

* Une icône incorrecte s’affiche lors de la création d’un dossier de contribution dans la fonction d’origine des ressources (CQ-4282825).
* Lors de la création d’un dossier de contribution, un ou les deux sous-dossiers (NOUVEAU et PARTAGÉ) n’apparaissent pas dans le dossier de contribution (CQ-4282424).
* Le système renvoie une exception si l’utilisateur tente de republier le dossier des contributions [!DNL Experience Manager] vers [!DNL Brand Portal] après avoir reçu de nouveaux actifs du dossier des contributions de [!DNL Brand Portal] fin (CQ-4279740).
* La création d’un dossier de contribution dans un dossier de contribution (dossier imbriqué) est interdite pour éviter toute complexité (CQ-4278391).
* Le système renvoie une exception lors du transfert de la liste [!DNL Brand Portal] utilisateur (.csv) importée à partir de [!DNL Experience Manager] la console d’administration. Seuls les champs Courriel, Prénom et Nom du fichier .csv sont obligatoires (CQ-4278390).

### Communities {#communities-6530}

**Correctifs**

* Les liens rapides permettant de gérer les groupes (Ouvrir/Modifier/Publier/Supprimer des groupes) ne sont pas visibles par les administrateurs de la communauté (administrateur du groupe/administrateur du site) (NPR-31627).
* Un blog envoyé n&#39;est pas affiché à moins que la page ne soit manuellement actualisée/rechargée (NPR-31599).
* La requête JCR utilisée par la fonction &quot;Mentions&quot; est sensible à la casse et prend trop de temps pour renvoyer les résultats (NPR-31475).
* [!DNL Experience Manager] 6.5 Le fichier UberJar renvoie une exception, `cq-social-translation` lot manquant dans le fichier [!DNL Experience Manager] 6.5 UberJar (NPR-31186).
* Les bibliothèques Jackson Databind ont été mises à jour vers la version 2.9.9.3 pour répondre à de nouvelles vulnérabilités (NPR-30967).
* Les titres des activités et des notifications sont contradictoires (NPR-30941).
* Pagination is not working properly in [!DNL Communities] Blogs (NPR-30914).
* Analytics reports are not populated in [!DNL Experience Manager] author environment, blank page appears (NPR-30913).

### Oak {#oak}

* Les mises à jour de l&#39;index Lucene provoquent un ralentissement du serveur d&#39;auteur (NPR-31548).

### Formulaires {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Le Service Pack n’inclut pas de correctifs pour [!DNL Experience Manager Forms]. Les correctifs sont fournis à l’aide d’un module complémentaire Forms distinct.  In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. Pour plus d’informations, voir [Installation du module complémentaire](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) Experience Manager Forms et [Installation d’Experience Manager Forms sur JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

#### Package de modules complémentaires Forms {#forms-add-on-package-6530}

**Formulaires adaptatifs**

* Les chaînes contiennent la clé du dictionnaire lors de la localisation des formulaires adaptatifs (NPR-31110).

**Communication interactive**

* **MissingNode.toString()** renvoie des résultats inexacts après la mise à niveau des bibliothèques Jackson vers la version 2.10.0 (NPR-31549).

* L’éditeur de texte supprime de manière aléatoire les caractères d’espace du texte copié à partir de Microsoft Word (NPR-31113).

**Correspondence Management**

* Les légendes et les info-bulles ne s’affichent pas lors de la migration de lettres de LiveCycle ES4SP1 à [!DNL Experience Manager] 6.5 (NPR-31615).

* **Le formatage de flux de texte n’est plus pris en charge** lorsque le message d’erreur s’affiche lors de l’enregistrement de lettres en tant que brouillons (NPR-30463).

**Processus**

* Le processus OSGi échoue en raison d’une utilisation 100 % du processeur (NPR-31233).

**Formulaires HTML5**

* La génération de l’aperçu HTML5 d’un formulaire XDP affiche un scintillement lors de l’ajout d’instances d’un sous-formulaire (NPR-30909).

#### Programme d’installation de Forms sur JEE {#forms-jee-installer-6530}

**Forms - Document Services**

* Le service Web SOAP utilisant MTOM dans un projet .NET affiche des exceptions pour les méthodes d’appel AssemblerServiceClient et HtmlToPDF2 (NPR-4281771).

**Foundation JEE**

* La configuration de l’action ne charge pas les noms de processus pour l’action d’envoi Appeler un processus de formulaires (NPR-31478).

### Packs de fonctionnalités inclus {#feature-packs-included-6530}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Prise en charge de Forms pour Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] La version 6.5.2.0 est une version importante qui comprend des améliorations et des correctifs concernant les performances, la stabilité, la sécurité et les clients clés depuis la publication de la version [!DNL Adobe Experience Manager] 6.5 en **avril 2019**. It can be installed on top of [!DNL Experience Manager] 6.5.

Les principaux points forts de cette version du Service Pack incluent les éléments suivants :

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.10.3.
* Added a configuration property to allow exporting Experience Fragments directly to user-defined workspaces for [!DNL Adobe Target].
* Les utilisateurs de ressources peuvent rechercher des images visuellement similaires. [!DNL Experience Manager] affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. Voir [Recherche visuelle](../assets/search-assets.md#visualsearch).

* La fonctionnalité Ressources connectées a été améliorée afin d’ajouter la prise en charge de la récupération de documents à partir de déploiements DAM distants. Les auteurs de site peuvent désormais rechercher et filtrer les types de documents pris en charge dans l’outil Recherche de contenu. Les documents distants peuvent être ajoutés au composant Télécharger sur les pages web. Voir [Utilisation des ressources connectées](../assets/use-assets-across-connected-assets-instances.md).

* filtres de type EnhanceDocument avec plus de types MIME pour prendre en charge les options à plusieurs valeurs.
* Un processus de retraitement externe pour la prise en charge de ressources multiples a été mis en place.
* Optimisation [!DNL Dynamic Media] des performances en utilisant les filtres de ressources par défaut pour la réplication.
* Les options de recadrage/rotation des fichiers ont été restaurées pour DMS7.
* Une option permettant de désactiver une vidéo au chargement dans VideoPlayer a été mise en œuvre.
* Une correction a été apportée pour assurer que la vue en colonne de l’interface utilisateur Asset affiche uniquement le contenu spécifique au client.
* Une correction a été apportée pour permettre aux modifications d’accordéon de style de se refléter dans les résultats de la recherche.

### Ressources {#assets}

**Améliorations apportées au produit**

* La fonctionnalité Ressources connectées a été améliorée afin d’ajouter la prise en charge de la récupération de documents à partir de déploiements DAM distants. Les auteurs de site peuvent désormais rechercher et filtrer les types de documents pris en charge dans l’outil Recherche de contenu. Les documents distants peuvent être ajoutés au composant Télécharger sur les pages web. Correctif pour CQ-4270245. Voir [Utilisation des ressources connectées](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Experience Manager Assets] les utilisateurs peuvent rechercher des images visuellement similaires. [!DNL Experience Manager] affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. Voir [Recherche visuelle](../assets/search-assets.md#visualsearch).

**Correctifs**

* Les chemins d’accès aux ressources dans les URL et les métadonnées des dossiers générés par l’API ACP ne sont pas codés dans les URL. GRANITE-26198 : correctif pour CQ-4271814
* Unzipping an archive with a folder having a percent sign (%) in its name can not be opened using [!DNL Experience Manager Assets] interface. NPR-29989 : correctif pour CQ-4270467
* Interface utilisateur tactile : Lors de l’assistant de gestion de publication, les références sont ajoutées après la page dans le corps de la demande de publication, ce qui entraîne la publication de tous les actifs après la page. Une fois la page rendue, certaines des ressources de l’instance de publication sont ignorées. NPR-29985 : correctif pour CQ-4270724
* La fonction Dissocier ne fonctionne pas pour les éléments associés dont le nom comporte des caractères spéciaux (caractères codés au format URI). NPR-30387 : correctif pour CQ-4274446
* Lors de la modification d’un fragment de contenu, la version est créée avec le mauvais utilisateur.
* Échec lors de la création de collections sur un système basé sur le client. NPR-30114 : correctif pour CQ-4272948
* L’affichage en colonne de l’interface utilisateur Asset ne respecte pas le chemin racine DAM du client actuel, mais l’accès à tous les chemins DAM du client. NPR-30636 : correctif pour CQ-4275481
* Attaque de XSS possible via une fenêtre d&#39;alerte de fichier restreinte, car l&#39;image injectée est visible. NPR-30617 : correctif pour CQ-4270133
* MultiTenant : Les clients qui enregistrent les propriétés du dossier observent à la fois l’invite de succès et le message d’erreur décrivant l’action a échoué. &quot;Impossible de modifier les propriétés. Autorisations insuffisantes. » et par conséquent, ils les confondent. NPR-30545 : correctif pour CQ-4275333
* La boîte de dialogue du sélecteur de ressources n’autorise pas la sélection de ressources, ce qui empêche la mise à jour de la source à l’aide de la fonctionnalité de remplacement de la source correspondante. NPR-30502 : correctif pour CQ-4275029
* [!UICONTROL Processus de mise à jour des ressources] DAM - En l&#39;état obsolète lors du téléchargement de fichiers mp4 volumineux. NPR-30480 : correctif pour CQ-4271352
* La fonctionnalité Créer une tâche de révision ne fonctionne pas en raison d’une charge utile nulle qui entraîne l’échec de toutes les actions de révision suivantes liées à la tâche. NPR-30468 : correctif pour CQ-4274263
* Problème de connectivité d’Adobe Smart Tag via Datapower. NPR-30026 : correctif pour CQ-4269457
* L’affichage en colonne de l’interface utilisateur Assets renvoie une erreur lors de la tentative d’ouverture des filtres à gauche du rail. NPR-30501 : correctif pour CQ-4273862
* Lors de l’ajout de groupes synchronisés à partir du protocole LDAP dans les propriétés du groupe d’utilisateurs fermés (CUG) d’un dossier de ressources, le groupe n’est pas enregistré ni récupéré. NPR-30615 : correctif pour CQ-4274689
* Les champs d’orientation et de style de recherche de filtre n’appliquent pas la valeur auto-renseignée à la requête de recherche. NPR-30620 : correctif pour CQ-4275724
* Le lien de partage de ressources d’un dossier avec un espace et le caractère « &amp; » dans le nom affiche des cartes grises vides pour certains fichiers. NPR-30557 : correctif pour CQ-4270187
* Le formulaire de schéma de métadonnées de dossier ne détecte pas automatiquement le type de données et ne crée donc pas le TypeHint associé dans l’envoi du formulaire. NPR-30599 : correctif pour CQ-4275227
* Les options de recadrage et de rotation des fichiers sont désactivées dans l’interface utilisateur de création de DMS7. NPR-30118 : correctif pour CQ-4273221
* Share Link feature is not working on [!DNL Experience Manager] instance with DMS7 configuration. NPR-30080, NPR-30492 : Correctif pour CQ-4273651
* Adding the [!DNL Dynamic Media]–Scene7 component to the page, and then publishing the page does not trigger the dmscene7 configuration every time. NPR-30641 : correctif pour CQ-4275962
* Added an IPSJobJournal in [!DNL Experience Manager] to create only one Intrusion Prevention Systems (IPS) job per processing profile. NPR-30490 : correctif pour CQ-4273614
* [!DNL Dynamic Media]: Ajouté des filtres par défaut pour exclure les ressources du noeud de [!DNL Experience Manager] publication. NPR-30538 : correctif pour CQ-4274678
* Un processus de retraitement externe a été mis en place pour la prise en charge de ressources multiples afin d’autoriser le dossier comme charge utile. Le workflow comporte deux étapes : retraitement des fichiers sans poignées via un mappage de métadonnées à l’étape suivante et retéléchargement de tous les fichiers sans poignée de ressources vers S7 dans une seule tâche IPS. For more details, see Configuring [!DNL Dynamic Media] Cloud Services. NPR-30489 : correctif pour CQ-4272903
* Le téléchargement d’un fichier CSV incorrect après un fichier CSV correct efface le fichier CSV correct. Correctif pour CQ-4277694, CQ-4277814
* L’icône incorrecte spécifique aux dossiers de contribution est à supprimer. Correctif pour CQ-4277580
* Lors de la sélection d’un utilisateur dans le sélecteur d’utilisateur de l’onglet Contribution, le nom de l’utilisateur n’apparaît pas dans le tableau et la boîte de dialogue Supprimer l’utilisateur de la page de propriétés affiche un texte incorrect. Correctif pour CQ-4277875
* Les contributeurs ne peuvent pas être ajoutés au dossier de contribution à partir du sélecteur d’utilisateurs en sélectionnant l’utilisateur et en cliquant sur Ajouter. Correctif pour CQ-4277824, CQ-4278087
* La recherche par nom d’utilisateur en minuscules ne fonctionne pas dans le sélecteur d’utilisateurs. Correctif pour CQ-4277958, CQ-4277930
* Les non-administrateurs peuvent publier des fichiers dans un nouveau dossier d’un dossier de contribution. Correctif pour CQ-4278200
* Un utilisateur DAM (non-admin) n’a pas la possibilité d’ajouter des contributeurs au dossier de contribution. Correctif pour CQ-4278192
* Le bouton « Créer » est visible dans le dossier de contribution. Correctif pour CQ-4277560
* Sorting search query by relevance returns [!DNL InDesign] documents along with [!DNL InDesign] templates. Correctif pour CQ-4273864
* Si l’utilisateur dispose d’un ID de courrier électronique en majuscules, il n’est pas possible d’archiver les fichiers qui ont été précédemment extraits. Correctif pour CQ-4276575
* L’opération Supprimer s’applique uniquement aux paramètres prédéfinis sélectionnés. Si l’écran actualise automatiquement la liste après l’opération, elle affiche les autres paramètres prédéfinis qui ont déjà été actualisés. Correctif pour CQ-4261461
* Configuring [!DNL Dynamic Media] Cloud Services in [!DNL Dynamic Media]–Hybrid mode results in multiple empty report suites created in [!DNL Analytics], and with no report suite id stored in [!DNL Experience Manager], resulting in report suite duplication. Correctif pour CQ-4249780
* Rename operation in [!DNL Experience Manager] asset to duplicated name fails to synchronize to Scene7. Correctif pour CQ-4276763
* Le contenu créé par l’utilisateur s’affiche incorrectement dans le panneau du filtre de recherche. Correctif pour CQ-4273875
* L’option Rechercher des images similaires n’est pas disponible pour les images TIFF. Correctif pour CQ-4278238
* Une option permettant de mettre en sourdine la vidéo au chargement dans VideoPlayer a été mise en œuvre. Correctif pour CQ-4266465
* Visionneuses - Visionneuse de vidéos : poster=none fonctionne incorrectement en cas d’utilisation d’une vidéo externe. Correctif pour CQ-4265536
* Une icône d’attente est visible pendant la lecture vidéo sur les navigateurs IE11 et MS Edge. Correctif pour CQ-4251539
* Les fichiers README des lecteurs 3.8 SDK et 5.13 ne sont pas mis à jour et contiennent des informations provenant de versions précédentes. Correctif pour CQ-4273737
* Le fragment de contenu est versionné avant même d’enregistrer les modifications. NPR-30616 : correctif pour CQ-4273088
* Remplacez Asset#getMetadata(String) par Asset#getMetadataValueFromJcr(String) dans le traitement des miniatures. NPR-30491 : correctif pour CQ-4273067
* Le téléchargement de fichiers jpg entraîne plusieurs instances du message : « ReplicateOnModifyWorker Replicating UPDATED » pour chaque ressource, ce qui entraîne une dégradation des performances.
* La décompression de l’archive zip à l’aide de la fonctionnalité Extraction de l’archive entraîne des problèmes avec les dossiers dont le nom contient le signe pourcentage (%) dans leur titre. NPR-29990 : correctif pour CQ-4270467

### Sites {#sites-6520}

* Si l’héritage de LiveCopy est rompu, les pages de copie dynamique affichent des liens de copie de langue au lieu de liens LiveCopy (NPR-30980).
* Pour un nouveau plan directeur, si le nombre d&#39;enregistrements est supérieur à 40, seuls les 40 premiers enregistrements sont affichés. Le plan directeur affiche des lignes vierges pour le reste des enregistrements (NPR-31182).
* Le module RTE (Rich Text Editor) du composant de texte affiche des caractères déformés pour le japonais et le coréen (NPR-31331).
* L’Editeur de texte enrichi (RTE) ne permet pas d’insérer un tableau incorporé en tant qu’élément de liste (NPR-30879).
* L’Editeur de texte enrichi (RTE) d’échafaudage prêt à l’emploi applique de manière inattendue la taille de police en ligne aux éléments (NPR-31284).
* Lorsqu’un utilisateur se concentre sur les champs du rail de gauche et utilise un raccourci clavier pour coller du contenu, il colle le contenu du Presse-papiers de l’éditeur de page au lieu du contenu copié à partir des champs du rail de gauche (NPR-31172).
* Lorsqu’un utilisateur ajoute un champ Téléchargement de fichier à un champ multichamp, le chemin d’accès à l’image est stocké dans le noeud de composant au lieu du noeud de champs multiples (NPR-30882).
* L’ `ResponsiveGridExporter` API ne renvoie pas `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` d’interface. Le `com.day.cq.wcm.foundation.model.impl` package est déclaré comme package privé (NPR-31398).
* Lorsqu’une page contenant certains fragments d’expérience est ouverte en mode non éditeur (dans Auteur sans préfixe et `editor.html` `wcmmode=disabled`ou dans Editeur), la requête se termine par le code d’erreur d’état HTTP 500 (NPR-30743).

### WCM - Éditeur de page {#wcm-page-editor-6520}

**Améliorations apportées au produit**

* Améliorez les filtres de type de document avec plus de types MIME pour prendre en charge les options à plusieurs valeurs. Correctif pour CQ-4270694

### Gestion des fragments de contenu {#content-fragment-management-6520}

* La requête utilisée par l’interface utilisateur des modèles de fragments de contenu est très lente et entraîne éventuellement une erreur. Correctif pour CQ-4270807

### IU - Fondation {#ui-foundation}

* Le déclencheur de raccourcis empêche l’utilisateur d’utiliser &#39;m,&#39; &#39;p,&#39; &#39;e&#39; dans des interfaces utilisateur spécifiques. NPR-30355 : correctif pour GRANITE-26346
* Closing [!DNL Experience Manager Assets] Search UI does not reset the left rail to Content selection preventing the user from opening the filter rail the second time subsequently. NPR-30509 : correctif pour CQ-4274716
* Multi-tenant environment: [!DNL Experience Manager Assets] UI top navigation is not available and throwing JavaScript error. NPR-30104 : correctif pour GRANITE-26344

### Traduction {#translation-6520}

* Problème de traduction : seuls quelques composants sont traduits à l’aide de la traduction automatique. NPR-30079 : correctif pour CQ-4273764

### Plate-forme {#platform-6520}

* [!DNL Experience Manager] Default Mail Sender ne peut pas envoyer de courrier à un serveur SMTP distant via TLS v1.2. NPR-30476 : Correctif pour GRANITE-26605

### Projets {#projects-6520}

* Les valeurs dam:folderThumbnailPaths ne sont pas actualisées et n’affichent pas les anciennes miniatures, même après la suppression des fichiers dans le dossier. NPR-30424 : correctif pour CQ-4273667
* Lorsque vous terminez avec l’option « déplacer », le titre et le nom du fichier restent inchangés. NPR-30647 : correctif pour CQ-4276265

### Communities {#communities-6520}

* Les diagnostics de synchronisation des utilisateurs sont complètement rompus et ne fonctionnent pas. NPR-30004, NPR-29943 : correctif pour CQ-4270287, CQ-4271348

### Sling {#sling}

* L’instance mise à niveau de 6.3.3.2 vers 6.5 entraîne la duplication des configurations OSGi. NPR-30130 : correctif pour CQ-4274016

### Intégration {#integration}

* Le contenu personnalisé ne s’affiche pas correctement sur l’instance de publication tant que l’instance n’a pas été redémarrée. NPR-30377 : correctif pour CQ-4273706
* Lors de la configuration de Launch sur un site web, l’adresse de la bibliothèque comporte une barre oblique (/) pré-activée, ce qui entraîne une intervention manuelle à chaque fois. NPR-30694 : correctif pour CQ-4275501

### Formulaires {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Le Service Pack n’inclut pas de correctifs pour [!DNL Experience Manager Forms]. They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. For more information, see [Install Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) and [Install Experience Manager Forms JEE installer](#forms-jee-installer).

The key highlights for [!DNL Experience Manager] 6.5.2.0 forms are:

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager] Forms OSGi.

#### Package de modules complémentaires Forms {#forms-add-on-package}

**Intégration dorsale**

* Impossible de configurer le modèle de données de formulaire à l’aide d’une URL équilibrée de charge hébergée par AWS. NPR-30123 : correctif pour CQ-4273359
* Lors de la création du modèle de données de formulaire (FDM) avec le langage WSDL (Web Service Definition Language), le message d’erreur `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` est renvoyé : NPR-30477 : Correctif pour CQ-4272921

**Correspondence Management**

* &quot;Le rendu de l’interface utilisateur de création de correspondance (IU CCR) échoue par intermittence avec l’erreur suivante dans la console :
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Communication interactive**

* Un champ marqué comme obligatoire dans le modèle de données de formulaire s’affiche comme requis dans l’interface utilisateur de création de correspondance (CCR UI). NPR-30623 : correctif pour CQ-4274902

**Forms - Workflow**

* Les variables de sortie non mappées sur les dossiers de contrôle provoquent l’échec de l’appel. Correctif pour CQ-4264451

**Formulaires HTML5**

* Lorsque le code personnalisé ou le projet est déployé pour la deuxième fois, la page ne s’affiche pas et l’erreur suivante se produit :

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539 : correctif pour CQ-4272509

* Lors de l’utilisation de l’option Accès aux ordinateurs de bureau non visuels en mode Navigation pour lire un formulaire HTML5, le navigateur Chrome affiche &quot;graphic&quot; avant chaque graphique vectoriel évolutif (SVG) dans la conception du formulaire. NPR-30449 : correctif pour CQ-4274732

#### Programme d’installation de Forms JEE {#forms-jee-installer}

**Forms - Document Security**

* L’application d’une signature avec horodatage échoue avec l’erreur : ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException : Erreur d&#39;appel. NPR-30820 : correctif pour CQ-4275852

**Forms - Document Services**

* Si &quot;SubmitURL&quot; contient une esperluette (&amp;), des erreurs d’analyse sont affichées dans le journal lorsque la demande POST est effectuée pour le rendu du servlet pdf. NPR-30865 : correctif pour CQ-4278232

**Forms - Foundation JEE**

* Le service HTMLtoPDF n’affiche pas maxReuseCount dans la console JMX. NPR-30134, NPR-30304 : correctif pour CQ-4273763
* Adding or editing a Web Service connection by invoking web services from [!DNL Experience Manager Forms] Workbench throws an error: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105 : correctif pour CQ-4273217

### Packs de fonctionnalités inclus {#feature-packs-included}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Sites {#sites-feature-packs-included}

* Added a configuration property to allow exporting Experience Fragments directly to user-defined workspaces for [!DNL Adobe Target]. NPR-29189 : correctif pour CQ-4249782

#### Forms - Document Services {#forms-document-services-1}

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager Forms] OSGi. NPR-30759 : correctif pour CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] La version 6.5.1.0 est une version importante qui comprend des améliorations et correctifs concernant les performances, la stabilité, la sécurité et les clients clés depuis la version 6.5 de la version [!DNL Adobe Experience Manager] d’ *avril 2019.*[!DNL Experience Manager] Elle peut être installée sur 6.5.

Les principaux points forts de cette version du Service Pack incluent les éléments suivants :

* Activation de l’inclusion de l’état d’interface utilisateur dynamique dans le suivi des événements en tant qu’attributs personnalisés.
* Included support for the delivery of 360-degree video assets in [!DNL Dynamic Media]–Scene7 mode.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. Pour plus d’informations, voir [Configuration du renvoi à la ligne de mots japonais](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Ressources

* Mise à jour de l&#39;interface DAM DMGGateway pour la prise en charge multipartie S3. NPR-29740 : correctif pour CQ-4226303
* La prévisualisation Rendus génère `Only empty tenantId is currently supported` une erreur après la mise à niveau vers [!DNL Experience Manager] 6.5. NPR-29986 : Correctif pour CQ-4272353
* La boîte de dialogue Supprimer n’est pas visible pour autoriser la suppression de tâches. NPR-29720 : correctif pour CQ-4271074
* After adding asset title in the properties page, when a user attempts to close the page, [!DNL Experience Manager] opens the properties page again. NPR-29627 : correctif pour CQ-4264929
* VersioningTimelineEventProvider doit fournir la version racine avec le nœud de type nt : version. Correctif pour GRANITE-26063
* Implemented the ability to upload and play 360 spherical videos in [!DNL Experience Manager] DM-Scene7 mode. Correctif pour CQ-4265131
* La Live Copy récupère un état incorrect si la source est modifiée. Correctif pour CQ-4265451
* Enabled Multi-Site Manager support for [!DNL Experience Manager Assets]. Correctif pour CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] doit afficher une entrée supplémentaire pour la version actuelle de la ressource dans l’historique de chronologie, affichant le dernier commentaire d’intégration provenant de [!DNL Adobe Asset Link]cette dernière. Correctif pour CQ-4262864
* Le Journal de fragment de contenu affiche un message d’erreur lorsque des propriétés sont manquantes. Correctif pour CQ-4272560
* Un problème survient avec le lecteur vidéo Scene7 lorsqu’il est agrandi en plein écran. Correctif pour CQ-4266700
* ZoomVerticalViewer : Les boutons de panoramique ne doivent pas être affichés si un seul fichier d’image est utilisé. Correctif pour CQ-4264795
* La suppression d’un nœud enfant dans la Live Copy doit détacher les informations liveRelationship. Correctif pour CQ-4270395
* Le schéma de métadonnées contient uniquement des éléments de la configuration globale et ne contient pas ceux du client actif. La valeur de l’URL formPath est rétablie par défaut, même en cas de modification. NPR-29945 : correctif pour CQ-4262898
* Publish image presets to [!DNL Brand Portal] fails with 500 error code. NPR-29510 : correctif pour CQ-4268659

### Sites

* Les propriétés vides et les propriétés multiples ne se propagent pas à partir du plan directeur lors du déploiement. La réinitialisation de la Live Copy avec le plan directeur ne fonctionne pas pour les composants. NPR-29253 : correctif pour CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537 : correctif pour CQ-4266129
* Enhancement of [!DNL Experience Manager] text component and Text Editor to Japanese. NPR-29785 : correctif pour CQ-4265090
* La page restaurée avec la distorsion du temps doit faire référence à l’image correcte au moment du contrôle de version. NPR-29431 : correctif pour CQ-4262638
* Problème d’héritage des noeuds Style System du parent à l’enfant. NPR-29516 : correctif pour CQ-4270330
* An error message while setting up the social posting to [!DNL Facebook] authentication. NPR-29211 : correctif pour CQ-4266630
* La miniature générée sur le fragment de contenu affiche une représentation de calendrier interne pour les champs Date et Heure. NPR-29531 : correctif pour CQ-4269362
* L’ouverture de l’onglet Autorisations dans l’implémentation Coral2 n’affiche pas les boutons. Correctif pour CQ-4269419

### Commerce

* ConstraintViolationException, lors de l’exécution d’une migration différée de contenu pour le commerce électronique. NPR-29247 : correctif pour CQ-4264383

### Gestion des fragments de contenu

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. Correctif pour CQ-4270266

### Fragments d’expérience

* Exportez [!DNL Experience Manager] des fragments d’expérience vers [!DNL Adobe Target]. Correctif pour CQ-4265469
* L’exportation des fragments d’expérience vers la cible échoue avec l’image dynamique. Correctif pour CQ-4269606

* L’utilisateur atteint une impasse lorsqu’il tente de déplacer les fragments d’expérience dans Omnisearch en mode d’affichage Carte. Correctif pour CQ-4263848

### WCM - Éditeur de page

* Les scripts intersites (XSS) se reflètent lors de l’utilisation d’un sélecteur non valide. Correctif pour CQ-4270397

### Réplication

* Les données fournies par l’utilisateur ne sont pas ignorées lors de la sortie dans le composant `cq/replication/components/agent`, ce qui entraîne une vulnérabilité Cross-site scripting (XSS) par stockage. Correctif pour CQ-4266263

### Workflow

* Le champ du sélecteur de calendrier du participant à la boîte de dialogue est rompu. NPR-29727 : correctif pour CQ-4270423

### WCM - Éditeur d’application monopage

* Activation de la récupération du contenu prérendu à partir d’un point de fin distant. Correctif pour CQ-4270238
* Avertissements dans les journaux lors de l’ouverture d’une page de modèle d’application monopage générée côté serveur. Correctif pour CQ-4270238

### WCM - MSM

* Upgrade to [!DNL Experience Manager] 6.4.3 makes Multi-Site Manager take a long time to roll out. Correctif pour CQ-4271410

### Intégration

* Échec des informations d’identification BrightEdge en cas d’erreur de connexion. NPR-29168 : correctif pour CQ-4265872

* An exception message is displayed when trying to edit and save the [!DNL Experience Manager] launch configuration. NPR-29176 : Correctif pour CQ-4265782 / CQ-4266153

### Interface utilisateur

* Ajout de la prise en charge du suivi des états de l’interface utilisateur dynamique en tant qu’attributs personnalisés lors du suivi de certains événements dans l’API de suivi des bases. Correctif pour GRANITE-26283
* Impossible de définir la fonction de suivi sur le bouton d&#39;envoi. Correctif pour GRANITE-26326
* L’assistant ne parvient pas à définir la fonction de suivi sur le bouton d’envoi. NPR-29995, NPR-30025 : correctif pour CQ-4264289

### Communities

* Impossible d&#39;aligner les nouveaux badges dans la liste déroulante de la page du profil du membre. NPR-29381 : correctif pour CQ-4267987
* Les visiteurs et les membres, sans privilèges de modérateur, peuvent voir les publications non approuvées / en attente en collant l’URL. NPR-29724 : correctif pour CQ-4271124, CQ-4271441
* Un temps de réponse élevé allant jusqu&#39;à 40-50 secondes est observé lors de la connexion de l&#39;utilisateur à la Communauté. NPR-29677 : correctif pour CQ-4269444

### Réplication

* Le composant Agent de réplication est exposé à une vulnérabilité qui divulgue des informations sensibles à des utilisateurs non autorisés. NPR-29611 : correctif pour GRANITE-25070

* Fuite de session pendant OAuth pour chaque réplication vers [!DNL Brand Portal]. NPR-30001 : correctif pour GRANITE-26196

### Projets

* Publish [!DNL Experience Manager Assets] from [!DNL Experience Manager] Author /content/dam/mac folder to [!DNL Brand Portal] doesn&#39;t work. NPR-29819 : correctif pour CQ-4271118

### Plate-forme

* HtmlLibraryManager supprime tout le contenu de crx-quickstart lors de l’invalidation du cache. NPR-29863 : correctif pour GRANITE-26197

### Felix

* Les détails d’utilisation de la mémoire ne s’affichent pas dans la console système lors de l’utilisation de Java11\. NPR-29669

### Formulaires

The key highlights for [!DNL Experience Manager Forms] 6.5.1.0 are:

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* OSGI uniquement : Activation de la prise en charge de la création de fichiers PDF statiques à l’aide de Forms Service.
* Autorisations activées sur XMLForm.exe pour les administrateurs et les utilisateurs racines.
* Prise en charge d’ADFS v3.0 pour l’intégration de Dynamics sur site activée.

#### Package de module complémentaire Forms

**Intégration du serveur principal**

* Échec de récupération du WSDL (Web Service Definition Language) protégé. NPR-29944 : correctif pour CQ-4270777
* When [!DNL Experience Manager Forms] is installed on IBM WebSphere, creating a form data model based on SOAP fails. Correctif pour CQ-4251134
* Activation de la prise en charge d’Active Directory Federation Services (ADFS) v3.0 pour l’intégration sur site de Microsoft Dynamics. Correctif pour CQ-4270586
* Lorsque le titre d’une source de données est modifié, le modèle de données de formulaire n’affiche pas le titre mis à jour. Correctif pour CQ-4265599
* Si le nom d&#39;une entité ou d&#39;un attribut contient un trait d&#39;union ou un espace, les expressions ne parviennent pas à évaluer ces entités et attributs. Correctif pour CQ-4225129

* Une sortie incorrecte est observée lorsqu’un deux-points est présent dans la sortie de chaîne primitive. Correctif pour CQ-4260825

* Même si aucun contenu n’est attendu de la sortie de l’API REST, l’opération d’appel du modèle de données de formulaire renvoie une erreur. Correctif pour CQ-4268828

**Formulaires adaptatifs**

* Impossible d’ajouter une nouvelle instance dans le fragment de formulaire adaptatif pendant le chargement différé. NPR-29818 : correctif pour CQ-4269875
* Le composant Vérifier ne consigne ni n’affiche d’erreur pour les modèles de document d’enregistrement. Correctif pour CQ-4272999
* Ajout de la prise en charge nécessaire à la désactivation de l’éditeur de mise en page pour les formulaires adaptatifs. Correctif pour CQ-4270810
* Restored the verify step for Adaptive Forms in [!DNL Experience Manager] 6.5. Hotfix for CQ-4269583

* Adaptive Form field validation failure breaks [!DNL Adobe Sign]. Correctif pour CQ-4269463
* When an [!DNL Experience Manager Forms] instance has more than 20 adaptive form fragments and name of all the form fragments starts with the same string, the search returns no or only recent 20 created fragments. Correctif pour CQ-4264414, CQ-4264914

* Problèmes de performances lorsque l’application de formulaires adaptatifs est utilisée avec un jeu de données volumineux. . Correctif pour CQ-4235310

* Lorsqu’il est accessible via un compte anonyme sur une instance de publication, le script GuideRuntime ne charge pas. Correctif pour CQ-4268679

**Forms - Communication interactive**

* Le modèle de communication interactive ne répertorie pas les composants d’en-tête et de pied de page dans la liste des composants autorisés. Correctif pour CQ-4237895
* Lorsque vous créez un modèle d’impression de communication interactive contenant un champ d’image, le titre du graphique est défini sur vide. Correctif pour CQ-4264772
* La couleur de ligne d’un graphique, une fois supprimée, est paramétrée comme non définie. Correctif pour CQ-4264762
* Les modifications de calque de mise en page effectuées sur le fragment de Document disparaissent lors de l’exécution de la synchronisation des modifications. Correctif pour CQ-4266054
* L’élément de modèle de données de formulaire à l’intérieur d’un fragment de document lié à un champ de texte n’affiche pas d’icône d’héritage et permet la liaison. Correctif pour CQ-4261089
* L’API de rendu de canal d’impression n’a pas la possibilité de transmettre des données en tant que paramètre dans l’API. Correctif pour CQ-4263540
* Les paramètres de l’agent ne sont pas visibles, car la case à cocher Modifier par l’agent est décochée lorsque le type de liaison est modifié du fragment de texte en Aucun/Objet de modèle de données pour le champ/variable de chaîne. Correctif pour CQ-4261953
* Lors de l’envoi de l’interface utilisateur de l’agent, le fichier json de données Web résultant stocke des informations pour les champs non liés annulés par héritage. Correctif pour CQ-4265621

**Forms - Workflow**

* Lorsqu’un formulaire est renvoyé à partir de la boîte d’envoi de l’application de formulaires adaptatifs, cela entraîne une perte de données. NPR-28345 : correctif pour CQ-4260929
* Les documents ne sont pas fermés lors de l’enregistrement pour les cas non variables. Correctif pour CQ-4269784
* L’application de formulaires adaptatifs a abandonné la prise en charge de Microsoft Windows 8.1. Correctif pour CQ-4265274
* When an image of more than 2 MB is attached as a field level attachment to a form in the Android version of [!DNL Experience Manager Forms] app, the app crashes. Correctif pour CQ-4265578

* Activation des options de préremplissage pour le canal d’impression Communication interactive dans la tâche Attribuer. Correctif pour CQ-4265577
* Les utilisateurs ne peuvent pas afficher une tâche partagée tant qu’ils ne sont pas membres du groupe auquel la tâche est affectée. Correctif pour CQ-4248733
* L’enregistrement ou l’envoi d’applications JEE sur une application de formulaire adaptatif est bloqué sous Windows. Correctif pour CQ-4268704
* Le modèle de données de formulaire associé à la variable de modèle de données de formulaire n’est pas visible. Correctif pour CQ-4266554
* Aucune prise en charge de la variable de statut du symbole de document utilisant la prise en charge des variables n’existe. Correctif pour CQ-4266312
* Les envois à partir de l’espace de travail échouent avec un caractère d’umlaut. Correctif pour CQ-4263172
* Lors d’une configuration mise à niveau, si le processus est ouvert pour modification, une erreur s’affiche au lieu du nom du processus dans l’interface utilisateur du dossier de contrôle. Correctif pour CQ-4238579

**Forms - Gestion**

* Lorsqu’une extension autre que xsd ou schema.json est téléchargée, le téléchargement n’a pas lieu et aucun message d’erreur n’est généré. Correctif pour CQ-4266716

**Forms - Gestion de correspondance**

* [!DNL Experience Manager Forms] 6.5 L’interface utilisateur de création de correspondance (interface utilisateur CCR) ne parvient pas à ouvrir la correspondance créée avec [!DNL Experience Manager Forms] 6.3. Correctif pour CQ-4266392.
* La fonction Somme dans XDP ne fonctionne pas si le type de données DDE est un numéro. Correctif pour CQ-4227403
* La logique d’invalidation du cache de lettres en mémoire doit être mise à jour, car lorsqu’un fichier est publié, son heure de dernière modification n’est pas mise à jour. Correctif pour CQ-4250465
* Impossible de publier le fragment de document, DD et lettres. Correctif pour CQ-4272893

#### Programme d’installation de Forms JEE

**PDF Generator**

* La conversion des fichiers CAO en PDF échoue avec le JDK 64 bits. NPR-29924, NPR-29925 : Correctif pour CQ-4272113
* Remplacement du nom de PhantomJS en WebToPDF pour la conversion HTML vers PDF. NPR-29933 : correctif pour CQ-4234545
* Une erreur est générée lors de la conversion du fichier zip au format PDF. Correctif pour CQ-4268628

**Forms - Designer**

* When a full accessibility check is performed on the static PDF created using [!DNL Experience Manager Forms Designer], the Primary Language check fails due to missing language attribute. Correctif pour CQ-4272923, CQ-4271002

**Forms - Document Security**

* La signature numérique avec le module de sécurité matérielle (HSM) ne fonctionne pas sous OSGi Linux sur Java 11 et Java 8\. NPR-29838 : correctif pour CQ-4270441
* La signature numérique avec le module de sécurité matérielle (HSM) ne fonctionne pas sur JEE Linux ni tous les serveurs d’applications pris en charge, c’est-à-dire JBoss et Websphere. NPR-29839 : correctif pour CQ-4266721
* La vérification des signatures dans un PDF à l’aide de PDF Advanced Electronic Signatures (PAdES) génère InvalidOperationException. NPR-29842 : correctif pour CQ-4244837
* Ajout de la prise en charge de Document Security Extension pour Office 2019\. Correctif pour CQ-4254369, CQ-4259764

**Forms - Document Services**

* La conversion du fichier PDF en PDF/A-1b avec le champ de formulaire n’a pas de code d’apparence. NPR-29940 : correctif pour CQ-4269618

* OSGi : Impossible de déterminer le nombre de pages générées lors du rendu. NPR-28922 : correctif pour CQ-4270870
* Activation de la prise en charge des fichiers PDF statiques à l’aide de Forms Service dans [!DNL Experience Manager Forms OSGi]. NPR-28572 : correctif pour CQ-4270869
* Impossible de modifier les autorisations sur XMLForm.exe. NPR-29828, NPR-29237 : Correctif pour le Q-4267080
* The static PDF created by the [!DNL Experience Manager Forms] server’s output module does not populate the language attribute/tag with the language of the document created. NPR-27332 : correctif pour CQ-4271002

**Forms - Foundation JEE**

* L’indisponibilité de pdfg_srt dans les artefacts finaux provoque l’échec du programme d’installation. NPR-29854 : correctif pour CQ-4270137
* LCBackupMode.sh ne fonctionne pas. NPR-29840 : correctif pour CQ-4269424
* La référence de port UDP doit être supprimée de l’interface utilisateur (IU) pour WebSphere. Correctif pour CQ-4264782

### Packs de fonctionnalités inclus

#### Ressources - incluses

* Enabled Multi-Site Manager support for [!DNL Experience Manager Assets]. For more information, see [Reuse assets using MSM for Experience Manager Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199 : correctif pour CQ-4259922

#### Sites - inclus

* Exportez [!DNL Experience Manager] des fragments d’expérience vers [!DNL Adobe Target]. For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Correctif pour CQ-4265469

#### Forms - Document Services - Inclus

* OSGi uniquement : Ajouté un nouvel attribut PAGECOUNT dans Output et Forms Service. NPR-28922 : correctif pour CQ-4270870
* OSGi uniquement : Activation de la prise en charge de la création de fichiers PDF statiques à l’aide de Forms Service. NPR-28572 : correctif pour CQ-4270869
* Autorisations activées sur XMLForm.exe pour les administrateurs et les utilisateurs racines. NPR-29237 : correctif pour CQ-4267080

### Lots OSGi et packages de contenu

The following text documents list the OSGi bundles and Content Packages included in [!DNL Experience Manager] 6.5.1.0

List of OSGi bundles included in [!DNL Experience Manager] 6.5.1.0

[Obtenir le fichier](assets/6_5-bundle-list.txt)

List of Content Packages included in [!DNL Experience Manager] 6.5.1.0

[Obtenir le fichier](assets/6_5-content-package-list.txt)
