---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: bb6e843bfad3feb194dd00588dbb4a2d3539743a
workflow-type: tm+mt
source-wordcount: '4658'
ht-degree: 41%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | Vendredi 21 novembre 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.22.0 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par la clientèle, ainsi que correctifs. Cette version comprend également des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la mise à disposition initiale de la version 6.5 en avril 2019. [Installez ce pack de services](#install) pour [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Principales fonctionnalités et améliorations

<!-- * _6.5.22.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Voici quelques-unes des fonctionnalités et améliorations clés de cette version :


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Problèmes corrigés dans le pack de services 22 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### Accessibilité {#sites-accessibility-6522}

* Il manquait un nom accessible au bouton du sélecteur d’échantillon d’annotation. En d’autres termes, avec un lecteur d’écran, il n’existe aucun nom compréhensible pour le bouton à sélectionner après avoir saisi une nouvelle valeur hexadécimale. (SITES-11992) MAJEUR
* Les éléments suivants du menu du rail de gauche apparaissent comme une liste, mais ne sont pas marqués comme tels dans le lecteur d’écran :

   * Site
   * Live Copy
   * Launch
   * Copie de la langue
   * Dossier
   * Rapport CSV (SITES-2874)

* AEM Core Web Content Management requiert un libellé d’accessibilité pour les hyperliens dans l’éditeur de texte enrichi. Lorsqu’un lien hypertexte est utilisé dans le composant de texte, la balise d’ancrage doit inclure l’attribut `aria-label` pour s’assurer que les lecteurs d’écran peuvent lire et transmettre le texte du lien avec précision à des fins d’accessibilité. (SITES-11511)
* Dans AEM, les éléments interactifs dans l’en-tête du tableau en mode Liste ne disposent pas du rôle &quot;bouton&quot; requis. Ainsi, le lecteur d’écran NVDA n’annonce pas les rôles de bouton attendus pour les en-têtes de tableau suivants : Titre, Nom, Modifié, Publié, Aperçu, Modèle, Opération, Workflow. Chaque élément interactif de l’en-tête du tableau doit se voir attribuer un rôle &quot;bouton&quot; pour garantir la compatibilité avec les technologies d’assistance telles que NVDA. (SITES-10962)


#### Interface utilisateur d’administration{#sites-adminui-6522}

* Dans certains cas d’AEM, les fonctionnalités de prévisualisation et de comparaison de versions ne fonctionnaient pas comme prévu sur plusieurs pages. Plus précisément :

   * **Problème d’aperçu :** lors de la tentative de prévisualisation d’une version de page, une erreur s’affiche initialement. Après une nouvelle tentative, l’aperçu génère une page vierge.
   * **Problème de comparaison de versions :** La fonction &quot;Comparer à actuel&quot; affichait uniquement la version actuelle, sans mettre en évidence les différences entre les versions. (SITES-23988) MAJEUR

* Une balise `<br>` inattendue s’affiche dans le champ de l’éditeur de texte enrichi lors de l’utilisation de l’ `defaultPasteMode` défini sur `plaintext` lors d’une action de copier-coller. Ce problème entraîne des balises différentes pour le même contenu, ce qui entraîne la traduction du même contenu texte deux fois dans la mémoire de traduction d’un client. (SITES-23606) MAJEUR
* Dans AEM 6.5.20.0, un problème de fonctionnalité s’est produit avec la fonction **Gérer la publication**. Lors de la sélection d’un noeud et de sa planification en vue d’une publication ultérieure, un message d’erreur &quot;Échec de la récupération des ressources enfants pour les éléments sélectionnés&quot; peut s’afficher lors de la tentative d’inclusion de noeuds enfants. Ce problème bloquait l’utilisation de l’option **Inclure les enfants**, empêchant la publication complète de la hiérarchie de contenu prévue. (SITES-23000) MAJEUR
* L’horodatage &quot;Publié&quot; d’un modèle ne se mettait pas à jour dans l’environnement de création, même si le modèle a été répliqué avec succès vers les instances de publication. Le comportement attendu était que l’horodatage sur l’instance d’auteur reflète la dernière publication, mais cette mise à jour ne s’est pas produite comme prévu. (SITES-21585) MAJEUR
* Le nombre de liens entrants était incohérent dans l’environnement de création AEM. Le rail de gauche présentait moins de liens que l’interface utilisateur classique. En outre, certains liens entrants légitimes ne fonctionnent pas. (SITES-24837)
* Les temps de chargement extrêmement longs étaient signalés lors de l’affichage des versions de page dans la vue Chronologie d’AEM. Il fallait jusqu’à 19 minutes pour afficher les versions. Ce problème était en cours depuis la mise à niveau d’AEM 6.4.8 vers 6.5.18, ce qui a considérablement perturbé l’efficacité des workflows. (SITES-22468 et SITES-22467)

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* Dans l’AEM mise à niveau version 6.5.17, l’enregistrement des fragments de contenu entraînait l’erreur suivante : *ERROR: Impossible d’enregistrer le fragment de contenu.* (SITES-22993) CRITIQUE
* Un problème a été identifié avec un résolveur de ressources non fermé dans `ContentFragmentModelOmniSearchHandler` sur l’éditeur dans AEM. (SITES-24903)


#### [!DNL Content Fragments] - Admin{#sites-admin-6522}

* Un clic sur le lien contenu dans la notification électronique redirige l’utilisateur vers la visionneuse ou l’éditeur de ressources par défaut. Il le fait au lieu de l’éditeur de fragment de contenu, même si la ressource du workflow est considérée comme un fragment de contenu. (SITES-24338) MAJEUR


#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6522}

* Lors de l’utilisation de fragments de contenu avec des éléments de champ de texte multiligne, les balises générées lors de l’interrogation à l’aide de GraphQL ne conservaient pas la mise en forme spécifiée dans l’HTML. Par exemple, une nouvelle ligne manquait après la liste. L&#39;impact a été que le dernier paragraphe est devenu une partie de la liste. (SITES-23233)


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### Back-end principal{#sites-core-backend-6522}

* Les erreurs `SegmentNotFoundException` récurrentes ont été signalées sur une instance d’auteur AEM. Le redémarrage de l’auteur a temporairement résolu le problème, mais une solution à long terme a été nécessaire pour empêcher d’autres occurrences. (SITES-22573)
* Un problème a été soulevé concernant la fonctionnalité de chronologie dans AEM Sites, en particulier concernant la gestion des propriétés `cq:lastModified` manquantes sur les annotations. Après l’application d’AEM version 6.5.20, des doutes subsistaient quant à savoir si le contenu existant nécessitait une correction pour la propriété manquante ou si la chronologie était mise à jour pour fonctionner correctement sans elle. (SITES-21861)


#### Composants principaux{#sites-core-components-6522}

* Suite à une mise à niveau d’AEM 6.5.18 vers 6.5.21, un problème a été identifié avec la fonctionnalité qui vérifie l’utilisation en direct des composants. Lorsque vous tentez de faire défiler la page Utilisation en direct pour d’autres éléments, le tableau ne parvenait pas à charger plus de résultats, même si &quot;Chargement d’autres éléments&quot; s’affichait dans l’interface utilisateur. (SITES-23919)
* Un problème a été signalé avec la validation des champs requis dans une boîte de dialogue de composant AEM contenant deux onglets. L’onglet 1 comprenait un éditeur de texte enrichi et des champs de texte, tandis que l’onglet 2 comportait des champs de chemin et de texte. Bien que tous les champs soient marqués comme obligatoires (`required=true`), les notifications d’erreur persistent incorrectement dans l’onglet 1, même après avoir renseigné tous les champs obligatoires. En revanche, les erreurs de l’onglet 2 ont été corrigées comme prévu. (SITES-23243)
* Après la migration vers AEM 6.5.21, l’instruction HTML Template Language `data-sly-include` ne fonctionnait plus comme prévu, en particulier en ne prenant pas en charge les expressions `appendPath` et `prependPath`. Par conséquent, la sortie de la ressource incluse n’était pas correctement rendue, même si elle fonctionnait correctement avant la migration. Ce problème provoquait des échecs de rendu pour les ressources qui reposent sur ces expressions pour la manipulation de chemin. (GRANITE-52970)


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### Fragments d’expérience{#sites-experiencefragments-6522}

* Les fragments d’expérience ne sont pas triés par titre comme prévu lorsque l’utilisateur clique sur l’en-tête de colonne **Titre** en mode Liste. Un scintillement rapide de l’écran est observé, mais il n’est pas trié. (SITES-23706) MAJEUR

* Dans AEM 6.5.17, un problème s’est produit lors de la conversion d’un composant de page en fragment d’expérience à l’aide de la fonctionnalité prête à l’emploi. Après la conversion, le fragment d’expérience s’affichait vide lors de la modification, même s’il s’affichait correctement sur la page sur laquelle il était utilisé. Le problème provenait d’une création de noeud incorrecte : le noeud de composant était placé en dehors du noeud racine/conteneur, ce qui violait la structure du modèle. Vous deviez déplacer manuellement le noeud de composant dans le noeud racine/conteneur approprié pour restaurer l’éditabilité du fragment. (SITES-22974) MAJEUR

* Après la migration d’AEM 6.5.11 vers 6.5.20, les configurations cloud sur les fragments d’expérience n’étaient pas correctement enregistrées. Bien que les configurations semblent enregistrer dans `crx/de`, elles ne s’affichaient pas lors de la réouverture de la console de configurations, indiquant un problème de persistance. (SITES-22287) MAJEUR


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### Lancements{#sites-launches-6522}

* Lors de l’ajout de ressources de fragments d’expérience à l’aide du filtre de balisage dans AEM production, l’utilisateur peut le sélectionner, mais une erreur s’est produite après avoir sélectionné **Créer une copie de langue**. Le comportement attendu était que la ressource de fragment d’expérience sélectionnée à partir du filtre de balisage était censée être ajoutée au projet de traduction. (SITES-24152) MAJEUR

#### Vérificateur de lien{#sites-link-checker-6522}

* L’authentification de LinkCheckerTask échoue, car le client HTTP tente NTLM avant l’authentification de base, ce qui entraîne le proxy à bloquer les utilisateurs après plusieurs tentatives infructueuses. Le système doit plutôt utiliser l’authentification de base pour s’authentifier par rapport au proxy, ce qui permet aux services LinkCheckerTask de fonctionner correctement. (SITES-25034) MAJEUR


#### MSM - Live Copies{#sites-msm-live-copies-6522}

* Lorsque les balises robots d’optimisation pour les moteurs de recherche sont appliquées à la copie principale et déployées sur les pages Live Copy, les valeurs s’affichent correctement dans `crx/de`. Toutefois, les valeurs n’étaient pas reflétées dans l’interface utilisateur sous Propriétés de page des pages Live Copy. (SITES-23475) MAJEUR
* Des erreurs liées aux lancements s’affichaient lorsqu’une tentative de promotion d’un lancement via l’interface utilisateur était effectuée. L’assistant Convertir le lancement est resté vide, ce qui empêche la fin du processus de promotion. (SITES-19718)
* Des problèmes se produisaient avec les fragments d’expérience dans AEM suite aux tentatives de création de Live Copies et d’exécution de déploiements. Le problème s’est produit lorsque les utilisateurs ont rencontré une erreur `NotFound` lors de la tentative de revenir à l’écran de gestion des fragments d’expérience à partir de l’écran Déploiement . (SITES-21933)


#### Éditeur de page{#sites-pageeditor-6522}

* Le bouton Annuler a modifié la position du composant, en plus de remplacer le texte par la dernière version. (SITES-17465) BLOQUEUR
* Lorsqu’un composant de conteneur copié était collé, il apparaissait visuellement deux fois, ce qui se traduisait par trois instances sur la page. Cependant, après avoir actualisé la page, le doublon a disparu, ce qui suggère que le problème était probablement un problème visuel temporaire. (SITES-21890) MAJEUR
* Lors de la navigation dans le volet de gauche Composants à l’aide des touches de tabulation du clavier ou Maj+Tab, plusieurs éléments de texte n’étaient pas clairement visibles, à la fois visuellement et en mode de tabulation. Ce problème affectait l’accessibilité, rendant difficile l’identification ou l’interaction avec ces composants lors de la navigation au clavier. (SITES-2266)

#### Réplication{#sites-replication-6522}

* Dans AEM 6.5.18 et 6.5.19, lors de la désactivation d’une page parente, plusieurs demandes de désactivation ont été générées pour chaque page enfant. Ce problème a également interrompu l’annulation de la publication en masse des points de terminaison GraphQL. (NPR-42075 &amp; NPR42010) CRITIQUE


### [!DNL Assets]{#assets-6522}

* Lors de l’utilisation de la fonction Assets connectée, les mises à jour effectuées dans AEM Assets ne sont pas répercutées sur l’environnement AEM Sites. (ASSETS-42344) MAJOR <!-- Leave the "MAJOR" status priorities in place. -->
* (ASSETS-41158) MAJEUR
* Le téléchargement de ressources à l’aide de l’API entraîne l’affichage d’un message d’erreur `unclosed resource resolver`. (ASSETS-41049) MAJEUR
* (ASSETS-40384) MAJEUR
* Dans AEM version 6.5.19, si vous supprimez une option des résultats du panneau de recherche, toutes les autres cases à cocher disponibles sont également décochées. (ASSETS-37335) MAJEUR
* Les valeurs &quot;indésirables&quot; s’affichent dans la sortie Excel lors de l’opération d’exportation des métadonnées en bloc. (ASSETS-37260) MAJEUR
* Dans AEM version 6.5.19, lorsque vous téléchargez un fichier de SVG au format UTF-8, la sortie est floue. (ASSETS-36616) MAJEUR
* L’option `Fetch original rendition for Dynamic Media Connected Assets` est manquante dans la configuration Assets connectée. (ASSETS-41726)
* Les propriétés de la ressource sont enregistrées même si vous ne définissez pas de valeur pour les champs obligatoires. (ASSETS-37914)

#### [!DNL Dynamic Media]{#assets-dm-6522}

* Un problème de production a perturbé le processus de migration lorsqu’un chargement vidéo vers Dynamic Media a échoué, affichant une erreur d’échec de processus dans l’interface utilisateur. (ASSETS-36038)


### [!DNL Forms]{#forms-65220}

Les correctifs dans [!DNL Experience Manager] Forms sont fournis par le biais d’un package complémentaire distinct une semaine après la date de publication prévue du pack de services [!DNL Experience Manager]. Dans ce cas, la publication du package complémentaire AEM 6.5.22.0 Forms est planifiée pour le vendredi 28 novembre 2024. Une liste des correctifs et améliorations de Forms est ajoutée à cette section après cette publication.


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### Foundation {#foundation-6522}

* Dans la console AEM Assets, un problème s’est produit lors de la tentative de réorganisation des documents DITA. Le chemin de navigation situé en haut de la boîte de dialogue Explorateur de chemins d’accès affiche incorrectement le nom du noeud au lieu du titre du noeud pour le parent racine. Le titre de noeud correct s’affiche uniquement après la sélection d’un élément dans le chemin de navigation, indiquant une erreur d’affichage temporaire. (NPR-42106) MAJEUR


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### Communities {#foundation-communities-6522}

* Après la mise à niveau d’AEM 6.5.19 vers 6.5.20, un problème s’est produit lorsque les threads `Connection evic` n’ont pas pu se fermer correctement après les appels vers `UgcSearch`. Ce problème, observé dans l’environnement de production, entraîne la persistance et l’accumulation de ces threads dans le temps, ce qui peut avoir un impact sur les performances. (NPR-42019) MAJEUR


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* Le tri ne fonctionnait pas conformément aux **Groupes** dans le menu de gauche du Gestionnaire de modules CRX. (GRANITE-53277)
* Le gestionnaire de modules dans AEM limite l’installation des versions de modules inférieures par défaut, mais permet des installations puissantes des versions antérieures. Cependant, l’utilisation de l’option forcer l’installation peut interférer avec les futures installations via le pipeline standard. Par exemple, si la version 1.21 est installée et que la version 1.24 est ajoutée, l’installation réussit, répertoriant les deux versions. Cependant, la tentative d’installation de la version 1.22 sur 1.24 échoue via le pipeline, mais fonctionne si l’installation est forcée, répertoriant toutes les versions. De même, l’installation de la version 1.23 est bloquée si la version 1.24 est déjà présente, car le pipeline n’autorise pas les mises à niveau. (GRANITE-53263)


#### Granite{#foundation-granite-6522}

* Les packages instantanés étaient installés dans AEM à l’aide des commandes CURL. Pendant l’installation, le programme d’installation JCR a analysé les modules par le biais du programme d’installation OSGI pour s’assurer qu’aucun regroupement ou configuration OSGI supplémentaire n’est requis. Si une version de package contenait &quot;SNAPSHOT&quot;, le programme d’installation OSGI a déclenché VLT pour créer un package instantané correspondant. Cependant, comme chaque instance d’auteur AEM exécute son propre programme d’installation OSGI, les deux instances peuvent tenter de générer l’instantané simultanément, ce qui entraîne des conflits de session dans le référentiel. (NPR-42003) MAJEUR
* Une contention de verrouillage existait dans `ScriptDependencyResolver` avec AEM 6.5.21. (GRANITE-53181) MAJOR
* Après la mise à niveau d’AEM vers la version 6.5.21, des problèmes se produisaient lorsque les chemins relatifs étaient utilisés dans la syntaxe Sightly (HTL), comme `data-sly-use`. (GRANITE-53080) MAJOR


#### Intégrations{#foundation-integrations-6522}

* Ajout d’une déclaration d’attribution légale pour l’interface utilisateur Cloud Service. (FORMS-16373)
* Ajout d’autorisations de lecture pour l’utilisateur **fd-cloudservice** afin d’accéder aux configurations Captcha et Turnstile, ce qui lui permet de récupérer l’identifiant client et le secret client nécessaires au rendu et à la validation du captcha. En outre, un modèle de liste de contrôle d’accès a été mis en oeuvre pour gérer l’accès à ces configurations. (FORMS-16360)


#### Localisation{#foundation-localization-6522}

* Dans ![Icône Marteau](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) Outils > **Sécurité** > ![Icône Utilisateur](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **Utilisateurs**, sur la page Gestion des utilisateurs, les données de la colonne **État** de la table s’affichaient verticalement. (GRANITE-48304)


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### Plateforme{#foundation-platform-6522}

* Le suivi de la gestion des informations d’entreprise introduit dans AEM 6.5.18 a entraîné des anomalies dans le calcul des scores d’adoption des produits. La bibliothèque Mesures d’Adobe provoquait ce problème en écrasant les données utilisateur fournies par la bibliothèque de suivi Oméga. Par conséquent, les scores d’adoption pour de nombreux clients AEM Sites et AEM Assets sont tombés à zéro à compter de février 2024. (CQ-4358438) CRITIQUE
* Un problème critique a été identifié dans l’environnement de production, où le collecteur d’mémoire d’entrepôt gérait incorrectement les balises. Plus précisément, lorsqu’une balise a été déplacée ou renommée, le récupérateur de mémoire n’a pas réussi à mettre à jour la propriété `cq:MovedTo`, provoquant la disparition de la balise des pages. (CQ-4358293) MAJOR
* Un problème avec ContextHub dans AEM 6.5.19 provoquait une résolution incorrecte des segments lorsqu’un chemin d’accès contextuel était ajouté à une instance AEM. Le problème affectait spécifiquement le champ URL dans les objets JavaScript générés par le composant de page, où il manquait le préfixe de chemin de contexte requis. Cette omission empêchait les segments de fonctionner comme prévu. (SITES-21852)
* Mise à jour AEM Quickstart pour utiliser la bibliothèque `commons-collections-3.2.2-adobe-2`. La mise à jour permet de s’assurer que l’application peut continuer à s’exécuter en douceur. (NPR-42150)
* La configuration SMTP OAuth2 dans AEM 6.5 diffère considérablement de ce qui est utilisé dans AEM as a Cloud Service. Pour rationaliser la configuration et assurer la cohérence, la configuration dans AEM 6.5 devait être alignée sur les normes utilisées dans AEM as a Cloud Service. (GRANITE-53273)
* Un problème a été détecté lorsque vous avez cliqué sur ![Icône de compas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg) > ![Icône Projet](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg) Projets, puis que vous avez survolé l’icône ![Icône de gauche du rail](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![Icône Chevron Down](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) avec un accent grave apparaissait avant le texte de l’info-bulle &quot;Contenu uniquement&quot;. (CQ-4356633)

#### Sécurité{#foundation-security-6522}

* Des problèmes ont été rencontrés avec une bibliothèque cryptographique JSAFE obsolète (version 6.0.0) dans AEM. Un lot corrigé avec la version 6.2.5 de JSAFE est inclus dans AEM 6.5.22. (NPR-42006) CRITIQUE
* Lors de la validation des protocoles autorisés lors des contrôles XSS, les gestionnaires se comparent à &quot;http&quot; et &quot;https&quot;. Cependant, la propriété `protocol` d’un objet URL a renvoyé ces valeurs avec un deux-points à la fin, comme `http:` et `https:`. Cette incohérence provoquait des problèmes de validation. Pour garantir une analyse exacte, la vérification de protocole nécessaire pour tenir compte des deux-points ou ajuster la logique de comparaison en conséquence.  (NPR-42119)
* Après avoir installé AEM 6.5.21 (la version précédente était AEM 6.5.19) sur IBM® WebSphere® Liberty Profile et Semeru Java 8.0, il n’était pas possible d’ouvrir des pages. Les journaux d’erreurs indiquent les problèmes liés aux versions de servlet requis par différents lots. Pour résoudre ce problème, la dépendance sur `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` a dû être rétablie car elle était liée au problème. (NPR-42116)
* Plusieurs navigateurs abandonnent progressivement la prise en charge des cookies **SameSite=None**, utilisés pour autoriser l’accès aux cookies sur plusieurs sites. Autre possibilité, des **cookies partitionnés** sont introduits. Ces cookies isolent le stockage en fonction du contexte dans lequel ils sont utilisés, ce qui renforce la confidentialité et la sécurité en empêchant le suivi sur plusieurs sites tout en permettant aux cookies de fonctionner dans des partitions spécifiques, telles que le contenu tiers incorporé. (GRANITE-51953)


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### Traduction{#foundation-translation-6522}

* Ajout de la prise en charge des modifications récentes apportées aux composants principaux aux règles de traduction par défaut. (NPR-42029) CRITIQUE
* Un problème a été identifié avec l’exportation de fichiers XLIFF dans AEM Forms. Lors de l’utilisation de l’option **Exporter la sélection en tant que XLIFF (chaînes uniquement)**, la séquence de composants n’était pas conservée de manière cohérente. Toutefois, la séquence reste correcte lors de l’exportation de XLIFF pour une langue spécifique. Deux fichiers ont été fournis pour démontrer le problème : **DE-CH_Export.xliff** (séquence correcte) et **String_Export.xliff** (séquence incorrecte). (NPR-42118) MAJEUR


#### Interface utilisateur{#foundation-ui-6522}

* Le `coralui-component-dialog` modifiait l’emplacement de `cq-dialog-actions`, ce qui affectait potentiellement la disposition ou le comportement des boutons d’action dans les boîtes de dialogue d’AEM. (NPR-42294) BLOQUEUR
* La fonctionnalité de sélecteur de couleurs d’AEM ne fonctionnait pas correctement. Une fois accessible, un modal vierge s’affichait, empêchant la sélection de couleurs. Ce problème a commencé après l’installation d’AEM 6.5.20 dans l’environnement d’évaluation. Le sélecteur de couleurs a fonctionné correctement *avant* la mise à jour. (NPR-42163)
* Dans ![Icône de marteau](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Outils** > **Workflow** > **Modèles** > sélectionnez un modèle > **Démarrer le processus**, l’icône Parcourir manquait dans le champ Charge utile de la boîte de dialogue **Exécuter le processus**. (NPR-42162)


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A 


## Install [!DNL Experience Manager] 6.5.22.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible sur la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.22.0 sur l’une des instances de création à l’aide du gestionnaire de packages.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Experience Manager] 6.5.22.0. Par conséquent, avant d’installer le package, vous devez créer une sauvegarde du `crx-repository` au cas où vous auriez besoin de le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installer le pack de services dans [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois lors de l’installation du Service Pack. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation de la mise à jour complète pour vous assurer que l’installation est réussie. En règle générale, ce problème se produit dans [!DNL Safari], mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.22.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.22.0 ne prend pas en charge l’installation en Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche le numéro de version mis à jour `Adobe Experience Manager (6.5.22.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->.

1. Tous les bundles OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.20 ou ultérieure (utilisez la console web : `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Installer le pack de services pour [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du pack de services pour Experience Manager Forms, consultez les [instructions d’installation du pack de services Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La fonctionnalité de formulaires adaptatifs, disponible dans [AEM 6.5 QuickStart](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), est conçue à des fins d’exploration et d’évaluation uniquement. Pour une utilisation à des fins de production, il est essentiel d’obtenir une licence valide pour AEM Forms, car la fonctionnalité de formulaires adaptatifs nécessite une licence appropriée.

### Installer le package d’index GraphQL pour les fragments de contenu d’Experience Manager{#install-aem-graphql-index-add-on-package}

La clientèle qui utilise GraphQL doit installer le [fragment de contenu d’Experience Manager avec le package d’index GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Vous pouvez ainsi ajouter la définition d’index requise selon les fonctionnalités que vous utilisez réellement.

L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Pack de services.

### UberJar{#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.22.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.


## Fonctionnalités obsolètes et supprimées{#removed-deprecated-features}

Consultez les [fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md/).

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


* **Lié à Oak**
Depuis le pack de services 13 et les versions ultérieures, le journal d’erreur suivant a commencé à s’afficher, ce qui affecte le cache de persistance :

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  Ou

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Pour résoudre cette exception, procédez comme suit :

   1. Supprimez les deux dossiers suivants de `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Installez le Pack de services ou redémarrez Experience Manager as a Cloud Service.
Les nouveaux dossiers `cache` et `diff-cache` sont automatiquement créés et vous ne voyez plus d’exception liée à `mvstore` dans `error.log`.

* Mettez à jour vos requêtes GraphQL qui peuvent avoir utilisé un nom d’API personnalisé pour votre modèle de contenu afin d’utiliser plutôt le nom par défaut du modèle de contenu.

* Une requête GraphQL peut utiliser l’index `damAssetLucene` plutôt que l’index `fragments`. Il peut en résulter l’échec des requêtes GraphQL ou l’exécution de celles-ci peut prendre beaucoup de temps.

  Pour résoudre le problème, `damAssetLucene` doit être configuré pour inclure les deux propriétés suivantes sous `/indexRules/dam:Asset/properties` :

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Une fois la définition d’index modifiée, une réindexation est nécessaire (`reindex` = `true`).

  Après ces étapes, les requêtes GraphQL doivent être plus rapides.

* Lorsque vous tentez de déplacer, de supprimer ou de publier des fragments de contenu, des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées. La requête en arrière-plan échoue. En d’autres termes, la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement de cette opération, vous devez ajouter les propriétés suivantes au nœud de définition d’index `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de la version 6.5.0 - 6.5.4 au pack de services le plus récent sur Java™ 11, des exceptions `RRD4JReporter` s’affichent dans le fichier `error.log`. Pour arrêter les exceptions, redémarrez votre instance d’[!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie dans [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’[!DNL Experience Manager] 6.5.x.x :
   * « Lorsque l’intégration d’Adobe Target est configurée dans [!DNL Experience Manager] à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. » Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur `granite/operations/maintenance`.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur `granite/operations/maintenance`.
   * La zone réactive d’une image interactive de Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières avec achat.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : temporisation en attente de modification d’enregistrement pour terminer la désinscription.

* À partir de la version 6.5.15 d’AEM, le moteur JavaScript Rhino fourni par le lot ```org.apache.servicemix.bundles.rhino``` a un nouveau comportement d’hébergement. Les scripts qui utilisent le mode strict (```use strict;```) doivent déclarer leurs variables correctes. Dans le cas contraire, elles ne sont pas exécutées et finissent par générer une erreur d’exécution.

* L’installation du balisage du contenu d’usine par le biais d’un package de mise à jour officiel réinitialise la propriété languages du nœud `/content/cq:tags` par défaut. Cette action est vraie pour les packs de services, les packs de services de sécurité, les packs de correctifs, les packs de correctifs cumulatifs, les correctifs, etc. Il est donc nécessaire de l’ajouter à partir des propriétés avant l’installation.

### Problèmes connus pour AEM Sites {#known-issues-aem-sites-6522}

* L’aperçu des fragments de contenu échoue en raison de la protection DoS pour une grande arborescence de fragments. Consultez l’ [ article de la base de connaissances sur les options de configuration de l’exécuteur de requête GraphQL par défaut](https://experienceleague.adobe.com/fr/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934).


### Problèmes connus d’AEM Forms {#known-issues-aem-forms-6522}


* Après l’installation du pack de services AEM Forms JEE 21 (6.5.21.0), vous pouvez trouvez des entrées en double de fichiers JAR Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` sous le dossier `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926). Suivez ces étapes pour résoudre le problème :

   1. Arrêtez les localisateurs s’ils sont en cours d’exécution.
   1. Arrêtez le serveur AEM.
   1. Accédez à `<AEM_Forms_Installation>/lib/caching/lib`.
   1. Supprimez tous les fichiers de correctifs Geode, à l’exception de `geode-*-1.15.1.2.jar`. Confirmez que seuls les fichiers JAR Geode avec `version 1.15.1.2` sont présents.
   1. Ouvrez l’invite de commande en mode administration.
   1. Installez le correctif Geode à l’aide du fichier `geode-*-1.15.1.2.jar`.

* Si un utilisateur ou une utilisatrice tente de prévisualiser un brouillon de lettre avec des données XML enregistrées, certaines lettres spécifiques restent bloquées à l’état `Loading`. Pour télécharger et installer le correctif, voir l’article [Correctifs Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-14521)

* Après la mise à niveau vers le pack de services AEM Forms 6.5.21.0, le service `PaperCapture` ne parvient pas à effectuer d’opérations OCR (reconnaissance optique de caractères) sur les PDF. Le service ne génère pas de sortie sous la forme d’un PDF ou d’un fichier journal. Pour télécharger et installer le correctif, voir l’article [Correctifs Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (CQDOC-21680)

* Lorsque les utilisateurs ont effectué la mise à niveau d’AEM 6.5 Forms Service Pack 18 ou 19 vers Service Pack 20 ou 21, ils ont rencontré une erreur de compilation JSP. Cette erreur les empêchait d’ouvrir ou de créer des formulaires adaptatifs. Cela provoquait également des problèmes avec d’autres interfaces AEM. Il s’agissait notamment de l’éditeur de page, de l’interface utilisateur d’AEM Forms, de l’éditeur de processus et de l’interface Aperçu du système. (FORMS-15256)

  Si vous rencontrez ce problème, procédez comme suit pour le résoudre :
   1. Accédez au répertoire `/libs/fd/aemforms/install/` dans CRXDE.
   1. Supprimez le lot dont le nom est `com.adobe.granite.ui.commons-5.10.26.jar`.
   1. Redémarrez votre serveur AEM.

* Après la mise à jour vers AEM Forms Service Pack 20 (6.5.20.0) avec le module complémentaire Forms, les configurations reposant sur l’ancien service Adobe Analytics Cloud à l’aide de l’authentification basée sur les informations d’identification ne fonctionnent plus. Ce problème empêchait les règles d’analyse de s’exécuter correctement. Pour télécharger et installer le correctif, voir l’article [Correctifs Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-15428)

* Lorsqu’un utilisateur effectue une mise à jour vers AEM Forms Service Pack 20 (6.5.20.0) sur le serveur JEE et génère des PDF à l’aide des services de sortie, le rendu des PDF pose des problèmes d’accessibilité. Pour télécharger et installer le correctif, voir l’article [Correctifs Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922112)
* Lorsqu’un utilisateur génère des PDF balisés à l’aide du service de sortie sur JEE, un &quot;avertissement de structure inapproprié&quot; s’affiche. Pour télécharger et installer le correctif, voir l’article [Correctifs Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922038)
* Lorsqu’un formulaire est envoyé sur AEM Forms JEE, les instances d’un élément XML répétitif sont supprimées des données. Pour télécharger et installer le correctif, voir l’article [Correctifs Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922017)
* Lorsqu’un utilisateur d’un environnement Linux® effectue le rendu d’un formulaire adaptatif (on JEE) dans HTML, le rendu ne se fait pas correctement. Pour télécharger et installer le correctif, voir l’article [Correctifs Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921957)
* Lorsqu’une personne convertit un fichier XTG au format PostScript à l’aide du service Output sur AEM Forms JEE, l’erreur d’échec suivante se produit : `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. Pour télécharger et installer le correctif, voir l’article [Correctifs Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921720)
* Après la mise à niveau vers le pack de services AEM Forms 18 (6.5.18.0) sur le serveur JEE, lorsqu’une personne envoie un formulaire, elle ne parvient pas à générer des fichiers HTML5 ou PDF Forms et XMLFM se bloque. Pour télécharger et installer le correctif, voir l’article [Correctifs Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921718)
* Dans l’aperçu avant impression de l’IU de l’agent de communication interactive, le symbole monétaire (comme le symbole du dollar « $ ») s’affiche de manière incohérente pour toutes les valeurs de champ. Il s’affiche pour les valeurs allant jusqu’à 999, mais il est absent pour les valeurs supérieures ou égales à 1 000. (FORMS-16557)
* Les modifications apportées au fichier XDP des fragments de mise en page imbriqués dans une communication interactive ne sont pas répercutées dans l’éditeur de communication interactive. (FORMS-16575)
* Dans l’aperçu avant impression de l’IU de l’agent de communication interactive, certaines valeurs calculées ne s’affichent pas correctement. (FORMS-16603)
* Lorsque la lettre est affichée dans l’aperçu avant impression, le contenu est modifié. En d’autres termes, certains espaces disparaissent et certaines lettres sont remplacées par &quot;x&quot; (FORMS-15681).

## Lots OSGi et packages de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans cette version du pack de services [!DNL Experience Manager] 6.5.

* [Liste des lots OSGi inclus dans Experience Manager 6.5.22.0](/help/release-notes/assets/65210-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.22.0](/help/release-notes/assets/65210-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites Web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/fr/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-65)
>* [S’abonner aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)
