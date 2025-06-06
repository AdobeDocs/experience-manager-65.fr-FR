---
title: 'Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager] '
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 8cbf7188baf8cc997e0747be366f13c3b6c2c632
workflow-type: tm+mt
source-wordcount: '4590'
ht-degree: 35%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.23.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | Vendredi 22 mai 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.23.0 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par la clientèle, ainsi que correctifs. Cette version comprend également des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la mise à disposition initiale de la version 6.5 en avril 2019. [Installez ce pack de services](#install) pour [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Principales fonctionnalités et améliorations

<!--### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

### Formulaires {#forms-sp23}

Voici quelques-unes des fonctionnalités et améliorations clés de cette version :

* [Hyperliens accessibles avec style de texte mixte dans les PDF statiques](https://helpx.adobe.com/content/dam/help/fr/experience-manager/6-5/forms/pdf/using-designer.pdf) : les hyperliens contenant des styles de texte mixte dans les PDF statiques sont désormais balisés en tant qu’élément accessible unique. Cette amélioration simplifie l’arborescence des balises, améliore la navigation dans le lecteur d’écran et prend en charge une meilleure conformité en matière d’accessibilité.

* [Mise à jour de la matrice des plateformes prises en charge](/help/forms/using/aem-forms-jee-supported-platforms.md)

  La dernière version introduit des mises à jour de la matrice de plateforme prise en charge, assurant ainsi la compatibilité avec les technologies plus récentes.

   * IBM Content Manager Client 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Pilote Microsoft® SQL Server JDBC 12.8

   * Microsoft® Office 2021

   * Red Hat® Enterprise Linux® 9 (noyau 4.x, 64 bits) 



* [Composant de pièce jointe renforcé](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment) : par mesure de sécurité, le composant empêche désormais l’envoi de fichiers avec des extensions modifiées qui tentent de contourner les vérifications de type de fichier autorisées. Ces fichiers sont bloqués pendant l’envoi afin de s’assurer que seuls des types de fichiers valides sont acceptés.

<!--* **Two-Factor authentication with SAML for AdminUI** 

  AdminUI in AEM Forms JEE now supports two-factor authentication using Security Assertion Markup Language (SAML) single sign-on (SSO), providing stronger security and a seamless login experience for administrators, similar to what is available in HTML Workspace. 

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## Problèmes corrigés dans le pack de services 23 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### Accessibilité {#sites-accessibility-6523}

* Les sections Zone de travail des pages de l’éditeur AEM prennent désormais en charge l’accessibilité clavier complète. Les utilisateurs peuvent activer les titres de section et modifier les boutons à l’aide du clavier uniquement, sans avoir à pointer avec la souris. Cette mise à jour garantit la conformité à WCAG 2.1.1 et améliore la convivialité sur les composants tels que le teaser, l’image, le carrousel, la disposition, la déformation temporelle et les modèles d’annotation. (SITES-25256) <!-- 6.5 LTS SP1 -->
* Correction d’un problème d’accessibilité dans l’éditeur de page d’AEM en raison duquel le focus au clavier se réinitialisait de manière inattendue au début de la barre d’outils démographique après l’activation de boutons tels que persona, panier ou abandonné. Le focus reste désormais sur le bouton activé pour prendre en charge les workflows cohérents de navigation au clavier et de lecteur d’écran. (SITES-25306)
* Correction d’un problème d’accessibilité critique dans l’éditeur de page d’AEM en raison duquel les éléments de la zone de travail dans plusieurs boîtes de dialogue et modèles (par exemple, le rail des ressources ou l’aperçu de la disposition) ne pouvaient pas être utilisés uniquement à l’aide du clavier. Tous les éléments de zone de travail interactifs prennent désormais en charge la navigation au clavier uniquement, ce qui garantit la conformité au critère de succès 2.1.1 WCAG 2.1 (SITE-25256)
* Correction d’un problème d’accessibilité dans l’interface utilisateur d’administration de Sites en raison duquel les éléments de liste interactifs dans le pop-up Créer utilisaient des rôles ARIA incorrects. Les éléments qui se comportaient comme des liens étaient affectés `role="listitem"` au lieu de `role="menuitem"`, enfreignant les modèles de conception ARIA et déroutant les lecteurs d’écran. Les mises à jour garantissent que tous les composants de liste suivent les rôles sémantiques appropriés pour une meilleure prise en charge du clavier et des technologies d’assistance. (SITES-24493)
* Correction d’un problème d’association des libellés d’accessibilité pour les champs de titre de page et de balises. L’interface AEM associe désormais correctement les libellés d’accessibilité aux champs « Titre » et « Titre de la page » lors de l’utilisation de lecteurs d’écran tels que JAWS. Le correctif garantit une lecture correcte des libellés et améliore la conformité ADA sur la création de pages, les propriétés et les workflows de déplacement. (SITES-27149)
* Correction d’un problème d’accessibilité lié à l’identification du tableau dans la boîte de dialogue Autorisations. Le tableau des autorisations dans AEM utilise désormais les rôles et attributs ARIA corrects pour s’assurer que les lecteurs d’écran comme JAWS l’identifient correctement en tant que tableau. Le correctif améliore la conformité en matière d’accessibilité et garantit que les utilisateurs reçoivent des annonces de navigation et de contenu précises. (SITES-27140)
* Correction d’un libellé visuel manquant pour les champs de saisie de commentaire dans la chronologie. Correction des libellés visuels manquants pour les champs d’entrée « Commentaire » sous la section chronologie afin d’améliorer l’accessibilité. La mise à jour garantit que les lecteurs d’écran peuvent annoncer avec précision les libellés du champ. Cette expérience améliore la navigation et l’envoi de formulaires pour tous les utilisateurs et utilisatrices, en particulier ceux et celles qui dépendent des technologies d’assistance. (SITES-26903)
* Correction de l’accessibilité du clavier pour le bouton représentant des points de suspension dans les commentaires de la chronologie. Activation de la navigation au clavier pour le bouton représentant des points de suspension (points de suspension) en regard des commentaires sous la section Journal. Les utilisateurs peuvent désormais accéder au bouton et interagir avec celui-ci à l’aide de la touche de tabulation, ce qui améliore l’accessibilité pour les utilisateurs qui ne disposent que d’une navigation à l’aide du clavier. (SITES-26891)
* Amélioration des annonces NVDA/Narrateur pour les résultats de recherche dans les boîtes de dialogue de sélection. Mise à jour de la boîte de dialogue Ouvrir la sélection pour indiquer si des résultats de recherche sont trouvés ou non lors de l’utilisation de lecteurs d’écran, tels que NVDA ou Narrateur. Cette amélioration aide les utilisateurs et utilisatrices qui reposent sur des technologies d’assistance à comprendre le résultat de leurs actions de recherche sans avoir besoin d’une confirmation visuelle. (SITES-26883)
* Rôle ARIA corrigé pour l’icône représentant des points de suspension en regard du champ de saisie de commentaire. Mise à jour de l’icône représentant des points de suspension (trois points) à côté du champ de saisie de commentaire pour utiliser le rôle ARIA approprié, afin que les lecteurs d’écran puissent identifier précisément l’élément. Cette amélioration améliore la conformité en matière d’accessibilité et améliore l’expérience des utilisateurs qui dépendent des technologies d’assistance. (SITES-26881)
* Correction d’attributs ARIA non valides dans les composants de l’IU Coral. Mise à jour des composants de l’IU Coral pour garantir que tous les attributs ARIA utilisent des valeurs valides, améliorant ainsi la conformité en matière d’accessibilité. En particulier, les cas où des valeurs non valides telles que `aria-modal="dialog"` ont été attribuées de manière incorrecte ont été traités. Cette amélioration permet aux lecteurs d’écran d’interpréter correctement les éléments de boîte de dialogue, ce qui améliore l’accessibilité pour les utilisateurs qui dépendent des technologies d’assistance. (SITES-26873)
* Amélioration de la visibilité et des info-bulles des icônes dans les scénarios de redistribution. Amélioration du comportement de redistribution afin de garantir que les infobulles s’affichent correctement pour les icônes **Télécharger**, **Retraiter les ressources** et **Extraire**. Mise en évidence d’un problème d’accessibilité en raison duquel les icônes et leurs libellés sont devenus invisibles lorsque les paramètres de zoom de la fenêtre d’affichage ou du navigateur ont changé. Ce correctif prend en charge les utilisateurs souffrant de déficience visuelle en préservant la visibilité et en fournissant des descriptions d’icône appropriées lors du redistribution. (SITES-26871)

#### Interface d’utilisation d’administration{#sites-adminui-6523}

Correction d’une exception du service d’URL de l’éditeur universel avec des points d’entrée Externalizer manquants. Le service d’URL de l’éditeur universel gère désormais les points d’entrée de création, de publication ou d’externaliseur local manquants sans générer d’exceptions. Les utilisateurs administrateurs peuvent ouvrir l’éditeur de page avec succès même lorsque certaines configurations de l’externaliseur sont incomplètes. (SITES-28877) <!-- LTS -->

#### Interface utilisateur classique{#sites-classicui-6523}

* Problème dans les boîtes de dialogue de l’interface utilisateur classique en raison duquel le fait de basculer sur un bouton masquait une zone de texte et ne l’affichait pas à nouveau lors des clics suivants. Le correctif garantit que la zone de texte réapparaît correctement lorsqu’elle est basculée, restaurant le comportement attendu et évitant toute perturbation des workflows de boîte de dialogue dynamique. (SITES-30230)
* Correction de la fonctionnalité de recherche de ressources d’image de l’interface utilisateur classique endommagée après la mise à niveau du Service Pack 22. L’outil de recherche d’images de l’interface utilisateur classique gère désormais correctement les noms de ressources contenant des espaces ou des caractères spéciaux. Cette mise à jour permet de s’assurer que l’outil de recherche de ressources code correctement les noms de fichier, évitant les échecs de recherche et permettant aux auteurs de localiser et de sélectionner des ressources d’image sans erreurs. (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* Correction de l’échec du test de validation pour `DeleteVariationIT.testUpdateBasic`. Le test `DeleteVariationIT.testUpdateBasic` n’échoue plus lors de l’exécution de la validation du pack de services . Le correctif corrige un problème de mappage de texte manquant dans la logique de gestion JSON, assurant ainsi la stabilité des tests et évitant les perturbations inutiles des tests. (SITES-28022)
* AEM empêche désormais la dégradation des performances causée par des métadonnées XMP incorrectes dans les ressources d’image. Les Assets qui contiennent des noms de propriété XMP non valides ou non conformes, tels que ceux avec des segments numériques ou des structures non qualifiées, ne déclenchent plus de logs d’avertissement répétés pendant le traitement. Le système filtre les métadonnées problématiques pour garantir que l’ingestion et la validation des ressources se terminent sans erreurs. (SITES-30683) <!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] - Éditeur de fragments{#sites-fragments-editor-6523}

D’autres auteurs peuvent toujours publier des fragments de contenu même lorsqu’un autre auteur les extrait, ce qui est contraire au comportement prévu de la fonction d’extraction. Ce correctif empêche d’autres utilisateurs de voir ou d’utiliser les boutons Publier dans l’interface de création lorsqu’un fragment de contenu est extrait. (SITES-30578) <!-- LTS -->

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6523}

Correction de l’erreur QueryValidationError de GraphQL avec les schémas de fragment de contenu. L’actualisation du lot `cq-dam-cfm-graphql` corrige les erreurs de validation de schéma lors de l’utilisation de références à des fragments de contenu. Le correctif garantit que les requêtes GraphQL fonctionnent correctement sans nécessiter un réalignement manuel des schémas ou une republication après les déploiements de packages. (SITES-27001) <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### Console des composants{#sites-component-console-6523}

Améliorations apportées au chargement de la page « Utilisation des composants en direct ». Optimise la page « Utilisation en direct des composants » dans AEM pour empêcher l’affichage de lignes vides lors du défilement de jeux de données volumineux. Les utilisateurs qui chargent des composants avec des références d’utilisation étendues peuvent désormais charger des données en continu, sans espaces inutiles ni entrées vides. Cette expérience améliore la navigation dans les pages, la précision du suivi et l’efficacité de gestion dans les rapports d’utilisation des composants. (SITES-26454)

#### Back-end principal{#sites-core-backend-6523}

* Échec de la liste des ressources de l’outil de recherche de contenu fixe en raison de noms de ressources non valides. L’outil de recherche de contenu gère désormais correctement les noms de ressources contenant des caractères non codables. La liste des ressources dans l’éditeur de page n’échoue plus ou ne lance plus d’exceptions lorsque vous rencontrez des ressources aux noms problématiques. (SITES-28722)
* Problème en raison duquel le composant `SearchPathLimiter` générait un nombre excessif d’entrées de journal en imprimant des messages au niveau ERREUR pour chaque appel. Ce comportement a commencé après le pack de services 17 et a entraîné des problèmes de performances en raison de volumes de journaux extrêmement élevés. Le correctif réduit le niveau de journalisation à DEBUG, ce qui réduit considérablement le bruit du journal et améliore la surveillance du système et l&#39;efficacité des diagnostics. (SITES-29835)
* Une métadonnée XMP mal formatée a déclenché une erreur lors du traitement des ressources d’image dans le `ValidationDataServlet`. Le correctif garantit la conformité de la gestion des métadonnées et évite l’analyse redondante de propriétés non valides. (SITE-30683) <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### Lancements{#sites-launches-6523}

* Correction de l’affichage incorrect de la date de lancement entre le 25 et le 31 décembre. L’interface utilisateur des lancements affiche désormais les dates comprises entre le 25 et le 31 décembre avec l’année correcte. Le correctif garantit que les dates ne s’affichent plus incorrectement l’année suivante, évitant ainsi toute confusion lors de la planification et de la planification des campagnes. (SITES-28706)
* Correction de modèles AEM Launch endommagés après la mise à niveau du pack de services 22. Les modèles AEM Launch se chargent désormais correctement après une mise à niveau du Service Pack 22. Le correctif corrige les données non valides dans les configurations de lancement internes, ce qui permet aux utilisateurs d’afficher, de modifier et de créer des lancements sans erreurs ni champs manquants. (SITES-28504)


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### Éditeur de page{#sites-pageeditor-6523}

* Correction d’un problème de chargement du AssetPicker avec des résolutions d’écran inférieures. AssetPicker charge désormais correctement les ressources lorsque les utilisateurs font défiler l’écran vers une résolution inférieure (1 728 × 1 1117 ou inférieure). Les utilisateurs ne voient plus de ressources manquantes lors du défilement, ce qui améliore la gestion des ressources entre différents points d’arrêt d’appareil. (SITES-28065)
* Correction de l’annonce de lecteur d’écran manquant pour les actions de verrouillage et de déverrouillage de page. L’éditeur de page affiche désormais correctement le message « Informations : la page a été verrouillée/déverrouillée » lorsque les utilisateurs activent le bouton de verrouillage/déverrouillage. Le correctif améliore la conformité en matière d’accessibilité et garantit que les utilisateurs et utilisatrices de lecteurs d’écran reçoivent des mises à jour dynamiques lors de la modification des pages. (SITES-27143)
* Amélioration du comportement du focus de clavier pour les actions de composant dans la création AEM. Amélioration de la navigation au clavier dans l’outil de création AEM afin de s’assurer que le focus reste sur le composant nouvellement créé ou sélectionné après des actions telles que Configurer, Supprimer ou Convertir. Auparavant, le focus se déplaçait vers le haut de la page, ce qui provoquait des problèmes de conformité en matière d’accessibilité. Cette mise à jour améliore l’expérience utilisateur pour les utilisateurs et utilisatrices de clavier et de technologie d’assistance. Cela s’effectue en conservant la progression logique du focus dans le workflow d’édition. (SITES-26549)
* Amélioration de la navigation par onglets dans les boîtes de dialogue de création. Améliore la navigation au clavier dans les boîtes de dialogue de création d’AEM en permettant aux utilisateurs et utilisatrices de continuer à avancer après avoir atteint la zone d’édition Description. Auparavant, le recouvrement de la mise au point au niveau du champ Description bloquait la navigation supplémentaire sans utiliser de combinaisons de touches spéciales. La mise à jour garantit que les utilisateurs et utilisatrices peuvent se déplacer facilement dans les champs à l’aide de la seule touche de tabulation, améliorant ainsi la conformité en matière d’accessibilité et l’expérience utilisateur. (SITES-26524)
* Une régression introduite dans le pack de services 22 d’AEM 6.5 a empêché les utilisateurs d’inclure des espaces dans les titres de Launch. Le correctif restaure la possibilité d’utiliser des espaces, ce qui permet aux équipes de définir et d’organiser les noms de lancement de manière plus flexible, conformément au comportement attendu. (SITES-29414)
* Correction d’un problème de redimensionnement des composants dans les conteneurs de mises en page après les actions de masquage/affichage. L’éditeur de page calcule désormais correctement les valeurs des colonnes après avoir masqué et affiché un conteneur de disposition. Les utilisateurs et utilisatrices peuvent redimensionner les composants sans erreur et les colonnes s’affichent correctement lors des actions de redimensionnement. (SITES-28463)
* Correction du mauvais positionnement du bouton de l’arborescence de contenu dans l’éditeur de page. L’éditeur de page positionne désormais correctement le bouton Configuration de l’arborescence de contenu sous la boîte de dialogue Prévue « Teaser de titre » au lieu de la mauvaise section. Le correctif met à jour le CSS de la boîte de dialogue Arborescence de contenu pour qu’elle utilise `top:0` au lieu de `bottom:0`, assurant ainsi un emplacement correct des boutons. (SITES-28448)


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### Éditeur de texte enrichi{#sites-rte-6523}

Correction de balises `<br>` inattendues dans l’éditeur de texte enrichi avec le mode de collage de texte brut. L’éditeur de texte enrichi gère désormais correctement les opérations de couper-coller lors de l’utilisation de `defaultPasteMode` en texte brut. Le correctif empêche l’insertion de balises `<br>` inattendues lorsque les utilisateurs et utilisatrices coupent et collent du texte dans les champs de l’éditeur de texte enrichi, assurant ainsi une mise en forme épurée lors de la modification du contenu. (SITES-27780)

#### Éditeur universel {#sites-universal-editor-6523}

* Lorsque plusieurs requêtes contenant le paramètre de requête sont envoyées à AEM, le cookie du jeton de connexion peut ne pas être renvoyé à temps, ce qui peut entraîner l’échec de la connexion. (SITES-30659) <!-- LTS -->
* Pour garantir la compatibilité et la prise en charge avec les gestionnaires SAML, vous devez configurer la propriété `service.ranking` afin que le gestionnaire `Query Token Auth` s’exécute *avant* le gestionnaire `SAML Auth`. (SITES-29684)

### [!DNL Assets]{#assets-6523}

* Les problèmes suivants se produisent sur [!DNL AEM] page de navigation On-Premise (6.5.22.0) après avoir sélectionné ![Assets](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL Assets ]**, accédé au dossier**[!UICONTROL  Rechercher Adobe Stock ]**et sélectionné une image système :
   * Impossible d’obtenir la licence de l’image boursière sélectionnée et de l’enregistrer, car cliquer sur **[!UICONTROL Obtenir la licence et enregistrer]** affiche une liste déroulante vide.
   * La sélection de l’image Stock ou la saisie de l’URL de la page Stock redirige vers la page d’accueil [!DNL AEM], empêchant l’accès à l’image Adobe Stock. (ASSETS-48687)
* Problèmes lors de la gestion des dossiers si le nom du dossier contient un `/` dans la page de navigation On-Premise (6.5.22.0) [!DNL AEM]. (ASSETS-46740)
* Sur [!DNL AEM] 6.5, la page des détails de la ressource ne se charge pas depuis la vue ![Collection](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL Collections ]**en raison d’une utilisation élevée de la mémoire. (ASSETS-46738)
* Les problèmes d’intégration avec [!DNL InDesign] as `Day CQ DAM Mime Type OSGI` Service identifient incorrectement les fichiers [!DNL InDesign] comme `x-adobe-indesign` au lieu de `x-indesign`. (ASSETS-45953)
* [!DNL AEM 6.5.21] fuite de session identifiée à l’étape de workflow prête à l’emploi **[!UICONTROL Publication planifiée sur Brand Portal]**. (ASSETS-44104)
* Les erreurs **[!UICONTROL Mémoire insuffisante (OOM)]** s’affichent en [!DNL AEM] lors du traitement et de la publication des images. Ce problème était dû à des méthodes obsolètes dans les workflows, tels que **[!DNL Dam Asset update]** et **[!DNL Dynamic Media: Reprocess assets]**. (ASSETS-43343)
* Après avoir apporté une modification mineure, comme la mise à jour du titre, vous rouvrez et enregistrez à nouveau le **[!DNL Connected Assets configuration]** sur l’instance Sites locale. L’instance distante perd alors sa connexion à l’instance locale. Par conséquent, il ne peut pas établir de communication avec l’instance Sites locale. (ASSETS-44484)
* En [!DNL AEM 6.5.21], lorsqu’un chargement de ressources dans la vue Liste est annulé et qu’un second chargement est effectué, [!DNL AEM] affiche une erreur **[!UICONTROL 0 de NaN ressources chargées]**. (ASSETS-44124)

#### [!DNL Dynamic Media]{#assets-dm-6523}

Ajout d’une propriété de métadonnées (`jcr:content/metadata/dam:scene7SmartCropStatus`) aux ressources pour identifier les générations de recadrage intelligent ayant échoué. Permet une recherche, un filtrage et un retraitement efficaces des ressources présentant des problèmes de recadrage intelligent au moyen de workflows manuels ou automatisés. (ASSETS-46237)

#### [!DNL Dynamic Media] - Mode hybride {#assets-dm-hybrid-6523}

##### Dynamic Media - Package de module complémentaire hybride (AEM 6.5.23 et versions ultérieures)

À partir du pack de services 23 d’AEM 6.5, un nouveau package complémentaire est disponible pour Dynamic Media en mode hybride. Ce package comprend l’offre groupée `cq-scene7-imaging` spécifiquement compatible avec le mode d’exécution hybride de Dynamic Media.

**Correctif clé inclus**

Correction d’un problème dans Dynamic Media - Déploiements hybrides en raison desquels les mises à jour du paramètre `catalog.expiration` sous `/conf/global/settings/dam/dm/imageserver` n’étaient pas reflétées sur les URL du serveur ou de l’instance de création, malgré la réussite de la réplication sans erreurs. La mise à jour garantit la cohérence des valeurs d’expiration entre CRX/DE, la réponse du serveur et les URL de diffusion publiques. Cela améliore ensuite le comportement du cache et la fiabilité des transformations d’image. (ASSETS-44837)

**Points importants à prendre en compte**

* L’offre groupée `cq-scene7-imaging` de l’installation de base d’AEM 6.5.23 (et versions ultérieures) n’est *pas compatible* avec Dynamic Media en mode d’exécution hybride.
* L’installation du pack de services 23 (et versions ultérieures) seul *ne met pas automatiquement à jour* l’offre groupée `cq-scene7-imaging` existante sur les instances AEM configurées pour Dynamic Media en mode hybride (mode d’exécution `-r dynamicmedia`).

**Quand installer le package de module complémentaire hybride**

* Lors de la mise à niveau directe vers AEM 6.5.23 (et versions ultérieures) à partir d’AEM 6.5.19 ou version antérieure.
* Si des correctifs spécifiques à la fonctionnalité Dynamic Media en mode hybride sont nécessaires.
* Lors du déploiement d’une nouvelle instance Dynamic Media en mode hybride directement depuis AEM 6.5 GA (disponibilité générale) vers le pack de services 23 (et versions ultérieures).

**Télécharger le package de module complémentaire hybride**

Le package de module complémentaire hybride est disponible publiquement dans la distribution logicielle d’Adobe à compter du jeudi 22 mai 2025, avec la version officielle d’AEM 6.5.23. Les utilisateurs peuvent le trouver en recherchant **Package de module complémentaire hybride AEM 6.5 Dynamic Media** dans la distribution logicielle.


<!--### [!DNL Forms]{#forms-6523}


#### Forms Designer 

* When a user exports the data for an XFA-based PDF using the exportDataAPI, the resulting XML shows discrepancies when compared with the XML data exported manually using Acrobat Reader. Values of some fields were missing in the output compared to the output generated from Acrobat Reader. (LC-3922791).  

* On AEM Forms 6.5.22.0, when a user attempts to generate a tagged PDF using the Output Service in Workbench, the resulting PDF contains an extra label tag under the reference tag in the table of content item. (LC-3922756) 

* When a user places field captions with bottom or right alignment in AEM Forms Designer, the tag tree includes only the caption without the corresponding value, leading to incomplete accessibility tagging. (LC-3922619). 

* On upgrading from AEM Forms 6.5 Service Pack 6 to AEM Forms Service Pack 20, the QR codes in generated PDFs become unreadable. The alternative text for the QR codes also fails accessibility testing, affecting screen reader compatibility. (LC-3922551). 

* When a user renders a letter in Agent UI on AEM Forms Service Pack 18, the content fails to display correctly due to the FormService.render() API. (LC-3922461). 

 

#### Forms

* When a user enables "Allow Rich Text for Title" on the root panel in an AEM Forms Adaptive Form, the "Exclude Title from Document of Record" setting on a nested panel incorrectly hides the root panel's title in the auto-generated Document of Record. (FORMS-19696). 

* When a user attempts to assign a custom sling:resourceType to a core component using the aem:afProperties in a JSON schema on an on-premise AEM 6.5 instance, the custom resource type is not applied. (FORMS-19691). 

* When a user submits an Adaptive Form with prefilled attachments using URIs, the form submission fails with a NullPointerException due to missing binary data. (FORMS-19371) (FORMS-19486). 

* When a user uploads a PDF under the 'Forms and Documents' section in AEM 6.5 Forms, the timeline feature stops functioning. (FORMS-19407)(FORMS-19234). 

* When a user uploads files using the out-of-the-box (OOTB) file attachment component in AEM Forms, security vulnerabilities are identified. This leads to potential interception of the submission process by unauthorized entities. (FORMS-19271). 

* When a user configures an out-of-the-box Adaptive Form in AEM Forms to automatically generate a Document of Record (DoR), the "Title" field in Acrobat Reader's Document Properties does not display the captured DoR title, and the form title does not appear by default in place of the filename. (FORMS-19263). 

* When a user opens an Interactive Communication in Agent UI, the prefilled data cannot be completely erased; upon removal, it automatically refills with the same data. (FORMS-19151). 

* When a user previews a date field in the Agent UI, the date unexpectedly changes due to time zone discrepancies between the VM's UTC setting and the system's interpretation of the date. (FORMS-19115). 

* When a user submits a form, file attachments may duplicate leading to multiple uploads of the same file. (FORMS-19045)(FORMS-19051). 

* Adding coordinators to policy sets in AEM 6.5 Document Security fails across both production and lower environments. (FORMS-18603, FORMS-18212, FORMS-19697). 

* When a user clicks the "datepicker-calendar-icon" in desktop mode with an empty field in AEM Forms Service Pack 22, an error occurs due to the undefined _$focusedDate variable, disrupting associated custom scripts. (FORMS-18483)(FORMS-18268). 

* On AEM Forms Service Pack 19 (6.5.19.0), when a customer previews a letter, the 'Amount in words' field fails to display or update number values incorrectly, leading to misalignment and missing spaces in the content. (FORMS-18437, FORMS-17330, FORMS-18209, FORMS-18557, CTG-4150848,FORMS-19614, LC-3922004) 

* When a customer previews a saved letter in AEM Forms 6.5 SP19 on RHEL, the content misaligns, spaces are missing, and unexpected characters like 'x' appear. (FORMS-18422)(FORMS-17641). 

* When a user navigates between tabs in AEM Forms, selecting components on the first tab becomes unresponsive. (FORMS-18345). 

* In AEM Forms 6.5.21.0, when a user converts an HTML file to PDF using the WebToPDF option, the output PDF is missing the header section, including metadata and title tags. (FORMS-18223, FORMS-17835, FORMS-19642, FORMS-18224). 

* In the AEM JEE Process Manager SDK, when a user invokes the retryAction(long actionOid) method, the system incorrectly retries the first action found in the tb_action_instance table. This occurs even when a specific action ID is provided or when the ID is null, resulting in unintended behavior. (FORMS-18187). 

* After updating to SP22, a user encounters issues where the save draft and submission functionalities fail without displaying any error message. (FORMS-18069). 

* In AEM 6.5.21.0, transitioning from XSD-based foundation components to core components prevents the implementation of cross-file references in JSON schemas, impacting Adaptive Forms migration. (FORMS-18065). 

* When a user previews a letter in the Agent UI, the date field shows an incorrect value due to IC time conversion issues. These discrepancies arise from time zone differences between the VM environment and the system's interpretation of time (UTC vs. local time). (FORMS-17988) (FORMS-17248). 

* When a user previews letters using Notice IC templates in AEM Forms, PDF generation times vary significantly, from 1.5 seconds to more than 10 seconds, even on the same server. This inconsistency affects business critical workflows. (FORMS-17951). 

* When a user binds a Scribble Signature object in an Adaptive Form to an XDP using the 'Data Sources' option, changes cannot be saved due to persistent aspect ratio validation errors, even when using valid values. (FORMS-17587). 

* When a user uses a specific XDP with many hidden fields for document fragments, AEM creates CRX nodes with the cm:optional property set to false, which causes the Interactive Communication (IC) submission to fail. (FORMS-17538). 

* On AEM Forms 6.5.19.0, when a customer previews a letter, the numeric box field fails to handle negative values correctly when digit limits for Lead and Frac are defined. This issue occurs due to the use of parseFloat, which treats the minus sign as part of the number. (FORMS-17451). 

* On AEM Forms 6.5, when a letter is previewed, the use of the "*" wildcard in the Adobe.json file is noticed, raising a concern about its purpose and potential modification (FORMS-17317). 

* When a user uses a screen reader on the "Apply for a Fixed Rate Saver joint account", the headings are incorrectly announced as 'clickable', causing accessibility issues. (FORMS-17038). 

* When a form is embedded, the generated iframe is missing a title attribute, leading to an accessibility compliance issue. (FORMS-17010). 

* It is not possible to download a form using the Forms Manager UI without including associated dependencies such as themes and fragments. (FORMS-15811). 

* When a user accesses the form on mobile devices (iOS and Android), the 'next' and 'previous' buttons on the first page are disabled, but the screen reader does not identify them as disabled. (FORMS-15773). 

* When a user saves a large form with fragments and lazy loading enabled, it fails to retrieve drafts, disrupting the workflow. (FORMS-19890, FORMS-19808). 

 

#### Forms JEE 

* When a user reconfigures the database in AEM Forms, the connection fails due to hardcoded parameters. (FORMS-19568, FORMS-17621) 

* When a user sets up AEM 6.5 with MySQL 8.4 using the partial turnkey method, the LiveCycle Configuration Manager (LCM) fails to recognize the required MySQL connector driver during the database connection test, causing the setup to fail. (FORMS-19442). 

* When a user runs LCM with JDBC 12.8.1 on JRE 11 in a JEE environment, the setup fails due to incompatibility issues.(FORMS-19276). 

* When a user opens a task in AEM On-Premise, the system executes the Workspace Start Action Profile instead of the AssignedUserProfile. (FORMS-19065). 

* When a user uses the retryAction(long actionOid) method in the AEM JEE Process Manager, unexpected behavior occurs. (FORMS-18357)(FORMS-18187). 

* On AEM Forms 6.5.21.0, the PDFG conversion fails with the error below: (FORMS-16851)(FORMS-14613).   
 
#### Forms Captcha {#forms-captcha-6523} 

* Improved reCAPTCHA alerting in Adaptive Forms by updating submit error codes to 400. Also, refined log alerts to distinguish between timeouts, expirations, and bot detection failures, enhancing troubleshooting accuracy and system observability. (FORMS-19240) 
* Closed an unclosed `ResourceResolver` instance in `ReCaptchaConfigurationServiceImpl` to prevent potential resource leaks and improve system stability when using reCAPTCHA integrations in AEM Forms. (FORMS-19242) 
* Improved CAPTCHA configuration handling for AEM Forms by ensuring the correct configuration binds to each form when multiple entries exist in the `/conf/global` folder. Prevents unintended use of incorrect CAPTCHA settings when the configuration container is not explicitly selected. (FORMS-19239)-->


<!--
#### XMLFM {#forms-xmlfm-6523}

* A () -->

<!--
#### [!DNL Adaptive Forms] {#adaptive-forms-6523}

* A () -->

<!--
#### [!DNL Forms Designer] {#forms-designer-6523}

* A () -->


### Foundation {#foundation-6523}

* Correction d’un problème dans les bannières d’alerte Coral en raison duquel la couleur du texte apparaissait en blanc au lieu de noir après la mise à niveau vers le pack de services 21. Garantit l’application d’un style correct pour conserver un contraste et une lisibilité appropriés des messages d’alerte dans l’interface. (NPR-42359)
* Ajout de la prise en charge de l’intégration OAuth dans la configuration des balises intelligentes pour s’aligner sur l’obsolescence de JWT (JSON Web Token). Garantit le maintien des fonctionnalités des balises intelligentes à l’aide des méthodes d’authentification mises à jour. (NPR-42296)

#### Apache Felix {#foundation-apachefelix-6523}

Correction d’une exception NullPointerException qui se produisait lors du chargement de fichiers de clé privée vers un champ de propriété de type binaire dans CRX, restaurant la compatibilité présente via le pack de services 16. Active les workflows de chargement de fichiers de clés sécurisés dans AEM Managed Services sans erreurs de serveur ni interruption des processus de renouvellement de certificat. (CQ-4359178)


<!--
#### Campaign{#foundation-campaign-6523}

* A () -->

<!--
#### Cloud Services{#foundation-cloudservices-6523}

* A () -->

<!--
#### Communities {#foundation-communities-6523}

* A () -->

<!--
#### Content distribution{#foundation-content-distribution-6523}

* A () -->

<!--
#### CRX {#foundation-crx-6523}

* A () -->


#### Granite{#foundation-granite-6523}

* Résolution des cycles de dépendance OSGi entre les services de script Apache Sling qui provoquaient des retards ou des échecs lors du chargement des pages HTML après la mise à niveau vers le pack de services 21. Mise à jour des références de service internes afin d’éliminer les dépendances cycliques impliquant des composants `SightlyScriptingEngineFactory` et associés, ce qui améliore la fiabilité et le comportement de démarrage du moteur de script. (GRANITE-56808)
* Mise à jour des scripts JS dans Apache Sling pour qu’ils se chargent uniquement à la demande plutôt que rapidement au démarrage, ce qui élimine les conflits de thread et réduit le risque que les serveurs de publication ne répondent pas lors du chargement. Cette modification améliore la stabilité du serveur et les temps de réponse lors de scénarios à trafic élevé en empêchant le verrouillage des ressources provoqué par une résolution précoce du script. (GRANITE-56611)
* Correction d’un problème dans AEM Omnisearch en raison duquel les espaces réservés des champs de saisie s’affichaient incorrectement sous forme de libellés, ce qui entraînait une confusion visuelle. Permet d’assurer un rendu correct des espaces réservés dans les champs de filtre, en conservant un comportement de formulaire cohérent et accessible. (GRANITE-51791)
* Correction d’une erreur de serveur déclenchée lors de la sélection de plus de 30 modèles de fragments de contenu avec des références à plusieurs champs dans l’éditeur de modèles de fragments de contenu. Amélioration du composant de suggestion de filtre pour la prise en charge des opérations POST. Cette fonctionnalité permet de gérer correctement les grands jeux de références lors de la création de fragments de contenu et d’améliorer la stabilité des configurations de modèle à volume élevé. (GRANITE-57164)
* Correction d’un problème dans les CRM, en raison duquel un clic sur la fermeture d’une case à cocher entraînait involontairement le changement de son état. Mise à jour des styles pour limiter strictement l’activation des clics à l’élément de case à cocher, empêchant les interactions utilisateur accidentelles et améliorant l’utilisation et l’accessibilité des formulaires. (GRANITE-52384)


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

Correction d’un problème en raison duquel la validation SNI bloquait les appels API via HTTPS pour les clients AEM utilisant des configurations SSL Dispatcher avec des en-têtes d’hôte personnalisés. Introduit une option pour désactiver la validation SNI dans le cadre de la configuration Jetty, permettant la compatibilité avec des configurations de proxy inverse spécifiques lorsque la `mod_proxy` n’est pas possible. (NPR-42614)


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### Plateforme{#foundation-platform-6523}

* Correction d’un comportement de fusion de balises incohérent en s’assurant que la valeur de balise fusionnée s’affiche toujours correctement dans les ressources, que les balises soient créées en ligne ou par la méthode de création de balise standard. Empêche les valeurs résiduelles des champs `EN:title` de remplacer l’affichage de la balise fusionnée. (CQ-4358812)
* Correction du codage répété de l’esperluette et des caractères dans les valeurs de balise dans la boîte de dialogue d’édition de balise. Empêche l’ajout d’entités «&amp; » supplémentaires à chaque enregistrement, ce qui garantit que les valeurs des balises restent propres et cohérentes entre les modifications et évite les erreurs d’affichage dans le contenu créé. (CQ-4359048)
* Correction d’une erreur `ClassCastException` qui empêchait la diffusion d’e-mails lors de l’envoi du formulaire adaptatif dans AEM 6.5 s’exécutant sur WebSphere®. Le correctif permet une transmission réussie des e-mails en assurant la compatibilité entre `com.sun.mail.handlers.text_plain` et `java.activation.DataContentHandler`, en s’alignant sur la configuration du gestionnaire de messagerie attendue par les environnements WebSphere®. (NPR-42500)
* Amélioration de la gestion des erreurs dans le gestionnaire de packages, en veillant à ce qu’AEM affiche un message clair lorsque l’installation échoue et que la réponse d’erreur est vide dans le cas contraire. Ce correctif empêche les échecs silencieux et permet un débogage plus rapide lors du déploiement des packages. (NPR-42375)

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### Traduction{#foundation-translation-6523}

Correction d’un problème NullPointerException (NPE) déclenché lors de la mise à jour de fragments de contenu dans les workflows à l’aide de **Mettre à jour la copie de langue**. Ce correctif garantit que les workflows ne passent pas dans un état d’échec ou ne restent pas bloqués dans un état d’exécution lors de la modification du contenu lié aux références de traduction. (NPR-42115)

#### Interface d’utilisation{#foundation-ui-6523}

Ajoute des attributs de `title` manquants aux boutons de boîte de dialogue de l’interface utilisateur Coral, tels que **Terminé** et **Annuler** dans les boîtes de dialogue de modification des composants afin d’améliorer l’accessibilité et d’activer la validation automatisée. Garantit que les boutons conservent les attributs attendus dans le rendu du balisage, évitant les échecs dans les tests d’interface utilisateur basés sur Selenium. (NPR-42412)

#### Gestion de contenu web (WCM){#foundation-wcm-6523}

Correction d’un problème qui empêchait l’ajout de pages aux tâches de traduction lors de l’utilisation de la **mise à jour de la copie de langue** dans les environnements avec le pack de services 19 ou une version ultérieure. Garantit que les workflows de traduction se déroulent comme prévu, ce qui permet un transfert de page correct entre les copies de langue sans intervention manuelle. (CQ-4357929)

#### Workflow{#foundation-workflow-6523}

Correction d’un problème dans l’`EmailNotificationServiceProcessor` où la méthode `getSegmentId` renvoie des `null` après le déploiement du correctif, ce qui entraînait l’échec des déclencheurs d’e-mail lors du traitement du workflow. Restaure la logique de résolution correcte de l’identifiant de segment en s’assurant que le processeur récupère les valeurs de `SegmentInfo` requises pour prendre en charge les workflows de notification par e-mail sur les instances AEM. (CQ-4359755)


## Installer [!DNL Experience Manager] 6.5.23.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des informations détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.23.0 sur l’une des instances de création à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Experience Manager] 6.5.23.0. Par conséquent, avant d’installer le package, vous devez créer une sauvegarde du `crx-repository` au cas où vous auriez besoin de le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Installer le pack de services dans [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface d’utilisation du gestionnaire de packages se ferme occasionnellement pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation de la mise à jour complète pour vous assurer que l’installation est réussie. En règle générale, ce problème se produit dans [!DNL Safari], mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.23.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.23.0 ne prend pas en charge l’installation Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche le numéro de version mis à jour `Adobe Experience Manager (6.5.23.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->.

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

UberJar pour [!DNL Experience Manager] 6.5.23.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.23</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.



## Fonctionnalités obsolètes et supprimées{#removed-deprecated-features}

Consultez [Fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md/) pour obtenir une liste détaillée de toutes les fonctionnalités obsolètes ou supprimées pour AEM 6.5.

### Éditeur de SPA {#spa-editor}

[L’éditeur de SPA](/help/sites-developing/spa-overview.md) a été abandonné pour les nouveaux projets commençant par la version 6.5.23 d’AEM 6.5. L’éditeur de SPA reste pris en charge pour les projets existants, mais ne doit pas être utilisé pour de nouveaux projets.

Les éditeurs privilégiés pour la gestion du contenu découplé dans AEM sont désormais les suivants :

* [Éditeur universel](/help/sites-developing/universal-editor/introduction.md) pour la modification visuelle.
* [Éditeur de fragments de contenu](/help/sites-developing/universal-editor/introduction.md) pour la modification basée sur les formulaires.

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Problème avec le lot de script JSP dans AEM 6.5.21-6.5.23 et AEM 6.5 LTS GA**
AEM 6.5.21, 6.5.22, 6.5.23 et AEM 6.5 LTS GA sont fournis avec le lot `org.apache.sling.scripting.jsp:2.6.0`, qui contient un problème connu. Le problème se produit généralement sous une charge élevée lorsque l’instance AEM gère de nombreuses requêtes simultanées.

  Lorsque ce problème se produit, l’une des exceptions suivantes peut apparaître dans les journaux d’erreurs avec des références à `org.apache.sling.scripting.jsp:2.6.0` :

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  Lorsque cette erreur se produit, la seule méthode de récupération consiste à redémarrer l’instance AEM.

  Contactez le service clientèle d’Adobe et référencez cette note de mise à jour pour obtenir une résolution.

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

### Problèmes connus pour AEM Sites {#known-issues-aem-sites-6523}

Fragments de contenu : la prévisualisation échoue en raison de la protection DoS pour une arborescence de fragments volumineuse. Voir l’[article de la base de connaissances sur les options de configuration par défaut de l’exécuteur de requêtes GraphQL](https://experienceleague.adobe.com/fr/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934).

<!--### Known issues for AEM Forms {#known-issues-aem-forms-6523}

* When a customer upgrades from Struts 2.x to 6.x, stricter type checking can cause silent failures—especially when checkbox components return false and are bound to a List *Integer*. This value mismatch must be handled explicitly to avoid deserialization errors.

* If the HTML to PDF conversion fails on a SUSE&reg; Linux&reg; (SLES 15 SP6 onwards) server with the following error:
  
  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
  then set the following environment variable and restart the server:
    `OPENSSL_CONF=/etc/ssl`

* After installing AEM Forms JEE Service Pack 21 (6.5.21.0), if you find duplicate entries of Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` under the `<AEM_Forms_Installation>/lib/caching/lib` folder (FORMS-14926), perform the following steps to resolve the issue:

  1. Stop the locators, if they are running.
  1. Stop the AEM Server. 
  1. Go to the `<AEM_Forms_Installation>/lib/caching/lib`. 
  1. Remove all the Geode patch files except `geode-*-1.15.1.2.jar`. Confirm that only the Geode jars with `version 1.15.1.2` are present.
  1. Open the command prompt in administrator mode.  
  1. Install the Geode patch using the `geode-*-1.15.1.2.jar` file. 

* If a user tries to preview a draft letter with saved XML data, it gets stuck in `Loading` state for some specific letters. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (FORMS-14521)
  
* After upgrading to AEM Forms Service Pack 6.5.21.0, the `PaperCapture` service fails to perform OCR (Optical Character Recognition) operations on PDFs. The service does not generate output in the form of a PDF or a log file. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (CQDOC-21680)

* When users upgraded from AEM 6.5 Forms Service Pack 18 or 19 to Service Pack 20 or 21, they encountered a JSP compilation error. This error prevented them from opening or creating adaptive forms. It also caused issues with other AEM interfaces. Those interfaces included the Page Editor, AEM Forms UI, Workflow editor, and System Overview UI. (FORMS-15256)

  If you face such an issue, perform the following steps to resolve it:
    1. Navigate to the directory `/libs/fd/aemforms/install/` in CRXDE.
    1. Delete the bundle with the name `com.adobe.granite.ui.commons-5.10.26.jar`.
    1. Restart your AEM Server.

* After updating to AEM Forms Service Pack 20 (6.5.20.0) with the Forms Add-On, configurations relying on the legacy Adobe Analytics Cloud Service using credential-based authentication stop working. This issue prevented analytics rules from executing correctly. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (FORMS-15428)

* When a user updates to AEM Forms Service Pack 20 (6.5.20.0) on the JEE server and generates PDFs using output services, the PDFs render with accessibility issues. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922112)
* When a user generates Tagged PDFs using the output service on JEE, it shows "Inappropriate structure warning." To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922038)
* When a form is submitted on AEM Forms JEE, the instances of a repeating XML element are removed from the data. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922017)
* When a user in a Linux&reg; environment renders an Adaptive Form (on JEE) in HTML, it fails to render properly. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921957)
* When a user converts an XTG file to PostScript format using the Output Service on AEM Forms JEE, it fails with the error: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921720)
* After upgrading to AEM Forms Service Pack 18 (6.5.18.0) on JEE server, when a user submits a form, it fails to render HTML5 or PDF Forms and XMLFM crashes. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921718)
* In the Print Preview of the Interactive Communications Agent UI, the currency symbol (such as the dollar sign $) is inconsistently displayed for all field values. It appears for values up to 999 but is missing for values of 1000 and above. (FORMS-16557)
* Any modifications to nested layout fragments' XDP in an Interactive Communication are not reflected in the IC editor. (FORMS-16575)
* In the Print Preview of the Interactive Communications Agent UI, some calculated values are not displayed correctly. (FORMS-16603)
* When the letter is viewed in Print Preview, the content is changed. That is, some spaces disappear, and certain letters are replaced with `x`. (FORMS-15681)
* When a user configures a WebLogic 14c instance, the PDFG service in AEM Forms Service Pack 21 (6.5.21.0) on JEE running on JBoss&reg; fails due to classloader conflicts involving the SLF4J library. The error is displayed as follows (CQDOC-22178):
  
    ```java
    Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
    the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
    @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
    (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
    have different Class objects for the type org/slf4j/ILoggerFactory used in the signature-->

## Lots OSGi et packages de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans cette version du pack de services [!DNL Experience Manager] 6.5.

* [Liste des lots OSGi inclus dans Experience Manager 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/fr/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-65)
>* [S’abonner aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)
