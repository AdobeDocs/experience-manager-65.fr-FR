---
title: 'Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager] '
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 3f64cfa688ef1f0090b7ce0d821324593cbea693
workflow-type: tm+mt
source-wordcount: '6707'
ht-degree: 99%

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
| Date | Jeudi 22 mai 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.23.0 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par la clientèle, ainsi que correctifs. Cette version comprend également des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la mise à disposition initiale de la version 6.5 en avril 2019. [Installez ce pack de services](#install) sur [!DNL Experience Manager] 6.5.

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

* [Hyperliens accessibles avec style de texte mixte dans les PDF statiques](https://helpx.adobe.com/content/dam/help/fr/experience-manager/6-5/forms/pdf/using-designer.pdf) : les hyperliens contenant des styles de texte mixte dans les PDF statiques sont désormais balisés en tant qu’élément accessible unique. Cette amélioration simplifie l’arborescence des balises, améliore la navigation dans le lecteur d’écran et permet une meilleure conformité en matière d’accessibilité.

* [Mise à jour de la matrice des plateformes prises en charge](/help/forms/using/aem-forms-jee-supported-platforms.md)

  La dernière version introduit des mises à jour de la matrice des plateformes prises en charge, assurant ainsi la compatibilité avec les technologies plus récentes.

   * IBM®Content Manager Client 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Pilote Microsoft® SQL Server JDBC 12.8

   * Red Hat® Enterprise Linux® 9 (Kernel 4.x, 64 bits)

* [Composant de pièce jointe renforcé](https://experienceleague.adobe.com/fr/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment) : par mesure de sécurité, le composant empêche désormais l’envoi de fichiers avec des extensions modifiées qui tentent de contourner les vérifications des types de fichier autorisés. Ces fichiers sont bloqués lors de la soumission afin de garantir que seuls des types de fichiers valides sont acceptés.

* FORMS-20533, FORMS-20532 : AEM Forms comprend désormais une mise à niveau de la version Struts de 2.5.33 vers 6.x. La prise en charge a été ajoutée via un [correctif](/help/release-notes/aem-forms-hotfix.md) que vous pouvez [télécharger et installer](/help/release-notes/aem-forms-hotfix.md) pour ajouter la prise en charge de la dernière version de Struts.

* **LC-3922769** : désormais, certaines fonctionnalités d’AEM Forms nécessitent OpenSSL 3 pour fonctionner correctement. OpenSSL 3 doit être installé sur le système avec les bibliothèques `libcrypto.so.3` et `libssl.so.3`. Comme les mises à jour de sécurité ne sont disponibles que dans les versions avec OpenSSL 3.0.14 et que la prise en charge de SafeLogic prend fin en février 2025, nous avons supprimé bsafe et utilisons désormais OpenSSL 3 pour la conformité en matière de sécurité. Pour connaître la compatibilité des plateformes et les exigences détaillées, voir [Plateformes prises en charge par AEM Forms sur JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) et [Exigences techniques](/help/sites-deploying/technical-requirements.md).

  **Pour vérifier l’installation d’OpenSSL 3, procédez comme suit :**

   * **Systèmes basés sur RHEL/CentOS/Fedora** : `rpm -qa | grep   openssl3`
   * **Systèmes basés sur Ubuntu/Debian** : `dpkg -l | grep openssl3`
   * **Autre vérification** : `ldd /path/to/XMLForm |   grep -E 'libcrypto.so.3|libssl.so.3'` (si les bibliothèques sont dans LD_LIBRARY_PATH)





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

* Les sections Zone de travail des pages de l’éditeur AEM prennent désormais en charge l’accessibilité clavier complète. Les utilisateurs et les utilisatrices peuvent activer les titres de section et modifier les boutons à l’aide du clavier uniquement, sans avoir à pointer avec la souris. Cette mise à jour garantit la conformité avec la norme WCAG 2.1.1 et améliore l’accessibilité et l’ergonomie des différents composants (comme les modèles Teaser, Image, Carrousel, Disposition, Distorsion du temps et Annotation). (SITES-25256) <!-- 6.5 LTS SP1 -->
* Correction d’un problème d’accessibilité dans l’éditeur de page AEM en raison duquel le focus au clavier se réinitialisait de manière inattendue au début de la barre d’outils démographique après l’activation de boutons tels que Persona, Panier ou Abandonné. Le focus reste désormais sur le bouton activé pour prendre en charge les workflows cohérents de navigation au clavier et de lecteur d’écran. (SITES-25306)
* Correction d’un problème d’accessibilité critique dans l’éditeur de page AEM en raison duquel les éléments de la zone de travail dans plusieurs boîtes de dialogue et boîtes de dialogue modales (par exemple, le rail des ressources ou l’aperçu de la disposition) ne pouvaient pas être utilisés uniquement à l’aide du clavier. Tous les éléments de zone de travail interactifs prennent désormais en charge la navigation au clavier uniquement, ce qui garantit la conformité au critère de succès 2.1.1 de WCAG 2.1 (SITE-25256).
* Correction d’un problème d’accessibilité dans l’interface d’utilisation d’administration de Sites en raison duquel les éléments de liste interactifs dans le pop-up Créer utilisaient des rôles ARIA incorrects. Les éléments qui se comportaient comme des liens se voyaient attribuer `role="listitem"` au lieu de `role="menuitem"`, ce qui enfreignait les modèles de conception ARIA et déroutait les lecteurs d’écran. Les mises à jour garantissent que tous les composants de liste suivent les rôles sémantiques appropriés pour une meilleure prise en charge du clavier et des technologies d’assistance. (SITES-24493)
* Correction d’un problème d’association des libellés d’accessibilité pour les champs de titre de page et de balises. L’interface AEM associe désormais correctement les libellés d’accessibilité aux champs « Titre » et « Titre de la page » lors de l’utilisation de lecteurs d’écran tels que JAWS. Le correctif garantit une lecture correcte des libellés et améliore la conformité ADA sur la création de pages, les propriétés et les workflows de déplacement. (SITES-27149)
* Correction d’un problème d’accessibilité lié à l’identification du tableau dans la boîte de dialogue des autorisations. Le tableau des autorisations dans AEM utilise désormais les rôles et attributs ARIA appropriés pour s’assurer que les lecteurs d’écran comme JAWS l’identifient correctement en tant que tableau. Le correctif améliore la conformité en matière d’accessibilité et garantit que les utilisateurs et utilisatrices reçoivent des annonces de navigation et de contenu précises. (SITES-27140)
* Correction d’un libellé visuel manquant pour les champs de saisie de commentaire dans la chronologie. Correction des libellés visuels manquants pour les champs d’entrée « Commentaire » sous la section chronologie afin d’améliorer l’accessibilité. La mise à jour garantit que les lecteurs d’écran peuvent annoncer avec précision les libellés des champs. Cette expérience améliore la navigation et l’envoi de formulaires pour les utilisateurs et utilisatrices, en particulier les personnes qui dépendent des technologies d’assistance. (SITES-26903)
* Correction de l’accessibilité du clavier pour le bouton représentant des points de suspension dans les commentaires de la chronologie. Activation de la navigation au clavier pour le bouton représentant des points de suspension en regard des commentaires sous la section Chronologie. Les utilisateurs et utilisatrices peuvent désormais interagir avec le bouton à l’aide de la touche de tabulation, ce qui améliore l’accessibilité pour les utilisateurs et utilisatrices qui nécessitent une navigation au clavier uniquement. (SITES-26891)
* Amélioration des annonces NVDA/Narrator pour les résultats de recherche dans les boîtes de dialogue de sélection. Mise à jour de la boîte de dialogue Ouvrir la sélection pour indiquer si des résultats de recherche sont trouvés ou non lors de l’utilisation de lecteurs d’écran, tels que NVDA ou Narrator. Cette amélioration aide les utilisateurs et utilisatrices qui utilisent des technologies d’assistance à comprendre le résultat de leurs actions de recherche sans confirmation visuelle. (SITES-26883)
* Correction du rôle ARIA pour l’icône représentant des points de suspension en regard du champ de saisie de commentaire. Mise à jour de l’icône représentant des points de suspension à côté du champ de saisie de commentaire pour utiliser le rôle ARIA approprié, afin que les lecteurs d’écran puissent identifier précisément l’élément. Cela permet d’améliorer la conformité en matière d’accessibilité et l’expérience des utilisateurs et utilisatrices qui dépendent des technologies d’assistance. (SITES-26881)
* Correction d’attributs ARIA non valides dans les composants de l’interface d’utilisation Coral. Mise à jour des composants de l’interface d’utilisation Coral pour garantir que tous les attributs ARIA utilisent des valeurs valides, améliorant ainsi la conformité en matière d’accessibilité. En particulier, des cas ont été traités où des valeurs non valides telles que `aria-modal="dialog"` ont été attribuées de manière incorrecte. Cette amélioration permet aux lecteurs d’écran d’interpréter correctement les éléments de boîte de dialogue, ce qui améliore l’accessibilité pour les utilisateurs et utilisatrices qui dépendent des technologies d’assistance. (SITES-26873)
* Amélioration de la visibilité et des infobulles des icônes dans les scénarios Reflow. Optimisation du comportement Reflow pour garantir l’affichage correct des infobulles des icônes **Télécharger**, **Retraiter les ressources** et **Extraire**. Mise en évidence d’un problème d’accessibilité en raison duquel les icônes et leurs libellés devenaient invisibles lorsque la fenêtre était redimensionnée ou que les paramètres de zoom du navigateur étaient modifiés. Cette correction améliore l’accessibilité pour les personnes ayant une mauvaise vue, en maintenant la visibilité et en fournissant des descriptions appropriées des icônes en mode Reflow. (SITES-26871)

#### Interface d’utilisation d’administration{#sites-adminui-6523}

Correction d’une exception du service d’URL de l’éditeur universel avec des points d’entrée de l’externaliseur manquants. Le service d’URL de l’éditeur universel gère désormais les points d’entrée de création, de publication ou de l’externaliseur local manquants sans générer d’exceptions. Les administrateurs et administratrices peuvent ouvrir l’éditeur de page même lorsque certaines configurations de l’externaliseur sont incomplètes. (SITES-28877) <!-- LTS -->

#### Interface d’utilisation classique{#sites-classicui-6523}

* Problème dans les boîtes de dialogue de l’interface d’utilisation classique en raison duquel l’activation d’un bouton masquait une zone de texte et ne l’affichait pas à nouveau lors des clics suivants. Le correctif garantit que la zone de texte réapparaît correctement lors de l’activation, restaurant le comportement attendu et évitant toute perturbation des workflows de boîte de dialogue dynamique. (SITES-30230)
* Correction du dysfonctionnement de la fonctionnalité de recherche de ressources d’image de l’interface d’utilisation classique après la mise à niveau vers le pack de services 22. L’outil de recherche d’images de l’interface d’utilisation classique gère désormais correctement les noms de ressources contenant des espaces ou des caractères spéciaux. Cette mise à jour permet de s’assurer que la recherche de ressources code correctement les noms de fichier, évitant les échecs de recherche et permettant aux personnes chargées de la création de localiser et de sélectionner des ressources d’image sans erreurs. (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* Correction de l’échec du test de validation pour `DeleteVariationIT.testUpdateBasic`. Le test `DeleteVariationIT.testUpdateBasic` n’échoue plus lors de l’exécution de la validation du pack de services. Le correctif résoud un problème de mappage de texte manquant dans la logique de gestion JSON, assurant ainsi la stabilité des tests et évitant les perturbations inutiles. (SITES-28022)
* AEM empêche désormais la dégradation des performances causée par des métadonnées XMP incorrectes dans les ressources d’image. Les ressources qui contiennent des noms de propriété XMP non valides ou non conformes, comme ceux avec des segments numériques ou des structures non qualifiées, ne déclenchent plus de journaux d’avertissement répétés pendant le traitement. Le système filtre les métadonnées problématiques afin de garantir que l’ingestion et la validation des ressources s’effectuent sans erreur. (SITES-30683) <!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] - Éditeur de fragments{#sites-fragments-editor-6523}

Les autres personnes chargées de la création peuvent continuer à publier des fragments de contenu même lorsqu’une autre personne les verrouille, ce qui est contraire au comportement prévu de la fonctionnalité de verrouillage. Ce correctif empêche les autres utilisateurs et utilisatrices de voir ou d’utiliser les boutons Publier dans l’interface de création lorsqu’un fragment de contenu est verrouillé. (SITES-30578) <!-- LTS -->

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6523}

Correction de l’erreur QueryValidationError de GraphQL avec les schémas de fragment de contenu. L’actualisation du lot `cq-dam-cfm-graphql` corrige les erreurs de validation de schéma lors de l’utilisation de références à des fragments de contenu. Le correctif garantit que les requêtes GraphQL fonctionnent correctement sans nécessiter un réalignement manuel des schémas ou une republication après les déploiements de packages. (SITES-27001) <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### Console des composants{#sites-component-console-6523}

Améliorations apportées au chargement de la page « Utilisation des composants en direct ». Optimise la page « Utilisation des composants en direct » dans AEM pour empêcher l’affichage de lignes vides lors du défilement de jeux de données volumineux. Les utilisateurs et utilisatrices qui chargent des composants avec des références d’utilisation étendues peuvent désormais charger des données en continu, sans espaces inutiles ni entrées vides. Cette expérience améliore la navigation dans les pages, la précision du suivi et l’efficacité de gestion dans les rapports d’utilisation des composants. (SITES-26454)

#### Back-end principal{#sites-core-backend-6523}

* Correction de l’échec de la liste des ressources de l’outil de recherche de contenu en raison de noms de ressources non valides. L’outil de recherche de contenu gère désormais correctement les noms de ressources contenant des caractères non codables. La liste des ressources dans l’éditeur de page n’échoue plus et ne déclenche plus d’exceptions lorsque vous rencontrez des ressources aux noms problématiques. (SITES-28722)
* Problème en raison duquel le composant `SearchPathLimiter` générait un nombre excessif d’entrées de journal en imprimant des messages au niveau ERREUR pour chaque appel. Ce comportement a commencé après le pack de services 17 et a entraîné des problèmes de performances en raison de volumes de journaux extrêmement élevés. Le correctif abaisse le niveau de journalisation à DEBUG, ce qui réduit considérablement le bruit du journal et améliore la surveillance du système et l’efficacité des diagnostics. (SITES-29835)
* Des métadonnées XMP mal formatées déclenchaient une erreur lors du traitement des ressources d’image dans le `ValidationDataServlet`. Le correctif garantit la conformité de la gestion des métadonnées et évite l’analyse redondante de propriétés non valides. (SITE-30683) <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### Lancements{#sites-launches-6523}

* Correction de l’affichage incorrect de la date de lancement entre le 25 et le 31 décembre. L’interface d’utilisation des lancements affiche désormais les dates comprises entre le 25 et le 31 décembre avec la bonne année. Le correctif garantit que les dates ne s’affichent plus incorrectement l’année suivante, évitant ainsi toute confusion lors de la planification des campagnes. (SITES-28706)
* Correction de modèles de lancement AEM endommagés après la mise à niveau vers le pack de services 22. Les modèles de lancement AEM se chargent désormais correctement après une mise à niveau vers le pack de services 22. Le correctif corrige les données non valides dans les configurations de lancement internes, ce qui permet aux utilisateurs et utilisatrices d’afficher, de modifier et de créer des lancements sans erreurs ni champs manquants. (SITES-28504)


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### Éditeur de page{#sites-pageeditor-6523}

* Correction d’un problème de chargement d’AssetPicker avec des résolutions d’écran faibles. AssetPicker charge désormais correctement les ressources lorsque les utilisateurs et les utilisatrices font défiler l’écran avec une faible résolution (1 728×1 117 ou inférieure). Les utilisateurs et les utilisatrices ne rencontrent plus de ressources manquantes lors du défilement, ce qui améliore la gestion des ressources entre différents points d’arrêt d’appareil. (SITES-28065)
* Correction de l’annonce de lecteur d’écran manquant pour les actions de verrouillage et de déverrouillage de page. L’éditeur de page affiche désormais correctement le message « Informations : la page a été verrouillée/déverrouillée » lorsque les utilisateurs et les utilisatrices activent le bouton de verrouillage/déverrouillage. Le correctif améliore la conformité en matière d’accessibilité et garantit que les utilisateurs et les utilisatrices de lecteurs d’écran reçoivent des mises à jour dynamiques lors de la modification des pages. (SITES-27143)
* Amélioration du comportement du focus de clavier pour les actions de composant dans l’outil de création AEM. Amélioration de la navigation au clavier dans l’outil de création AEM afin de s’assurer que le focus reste sur le composant qui vient d’être créé ou sélectionné après des actions telles que Configurer, Supprimer ou Convertir. Auparavant, le focus se déplaçait vers le haut de la page, ce qui provoquait des problèmes de conformité en matière d’accessibilité. Cette mise à jour améliore l’expérience des utilisateurs et utilisatrices de clavier et de technologie d’assistance. Cela s’effectue en conservant la progression logique du focus dans le workflow de modification. (SITES-26549)
* Amélioration de la navigation par tabulation dans les boîtes de dialogue de l’outil de création. Améliore la navigation au clavier dans les boîtes de dialogue de l’outil de création AEM en permettant aux utilisateurs et utilisatrices de continuer à naviguer avec la touche Tab après avoir atteint la zone de modification Description. Auparavant, le blocage du focus au niveau du champ Description bloquait toute navigation supplémentaire sans l’utilisation de combinaisons de touches spéciales. La mise à jour garantit que les utilisateurs et utilisatrices peuvent se déplacer facilement dans les champs à l’aide de la seule touche Tab, améliorant ainsi la conformité en matière d’accessibilité et l’expérience d’utilisation. (SITES-26524)
* Une régression introduite dans le pack de services 22 d’AEM 6.5 empêchait les utilisateurs et les utilisatrices d’inclure des espaces dans les titres de lancement. Le correctif restaure la possibilité d’utiliser des espaces, ce qui permet aux équipes de définir et d’organiser les noms de lancement de manière plus flexible, conformément au comportement attendu. (SITES-29414)
* Correction d’un problème de redimensionnement des composants dans les conteneurs de mises en page après les actions de masquage/affichage. L’éditeur de page calcule désormais correctement les valeurs des colonnes après avoir masqué et affiché un conteneur de mise en page. Les utilisateurs et les utilisatrices peuvent redimensionner les composants sans erreur et les colonnes s’affichent correctement lors des actions de redimensionnement. (SITES-28463)
* Correction du mauvais positionnement du bouton de l’arborescence de contenu dans l’éditeur de page. L’éditeur de page positionne désormais correctement le bouton Configuration de l’arborescence de contenu sous la boîte de dialogue prévue « Teaser d’en-tête » au lieu de la mauvaise section. Le correctif met à jour le CSS de la boîte de dialogue Arborescence de contenu pour qu’elle utilise `top:0` au lieu de `bottom:0`, assurant ainsi un emplacement correct des boutons. (SITES-28448)


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### Éditeur de texte enrichi{#sites-rte-6523}

Correction de balises `<br>` inattendues dans l’éditeur de texte enrichi avec le mode de collage de texte brut. L’éditeur de texte enrichi gère désormais correctement les opérations de couper-coller lors de l’utilisation de `defaultPasteMode` en texte brut. Le correctif empêche l’insertion de balises `<br>` inattendues lorsque les utilisateurs et utilisatrices coupent et collent du texte dans les champs de l’éditeur de texte enrichi, assurant ainsi une mise en forme nette lors de la modification du contenu. (SITES-27780)

#### Éditeur universel {#sites-universal-editor-6523}

* Lorsque plusieurs requêtes contenant le paramètre de requête sont envoyées à AEM, le cookie du jeton de connexion peut ne pas être renvoyé à temps, ce qui peut entraîner l’échec de la connexion. (SITES-30659) <!-- LTS -->
* Pour garantir la compatibilité et la prise en charge avec les gestionnaires SAML, vous devez configurer la propriété `service.ranking` afin que le gestionnaire `Query Token Auth` s’exécute *avant* le gestionnaire `SAML Auth`. (SITES-29684)

### [!DNL Assets]{#assets-6523}

* Les problèmes suivants se produisent sur la page de navigation [!DNL AEM] On-Premise (6.5.22.0) après avoir sélectionné ![Ressources](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL Ressources &#x200B;]**, accédé au dossier&#x200B;**[!UICONTROL &#x200B; Rechercher dans Adobe Stock &#x200B;]**&#x200B;et sélectionné une image système :
   * Il était impossible d’obtenir la licence de l’image Stock sélectionnée et de l’enregistrer, car cliquer sur **[!UICONTROL Accorder sous licence et enregistrer]** affichait une liste déroulante vide.
   * La sélection de l’image Stock ou la saisie de l’URL de la page Stock redirige vers la page d’accueil [!DNL AEM], empêchant l’accès à l’image Adobe Stock. (ASSETS-48687)
* Problèmes lors de la gestion des dossiers si le nom du dossier contient un élément `/` dans la page de navigation [!DNL AEM] On-Premise (6.5.22.0). (ASSETS-46740)
* Sur [!DNL AEM] 6.5, la page des détails de la ressource ne se charge pas depuis la vue ![Collection](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL Collections &#x200B;]**&#x200B;en raison d’une utilisation élevée de la mémoire. (ASSETS-46738)
* Problèmes d’intégration à [!DNL InDesign], car le service `Day CQ DAM Mime Type OSGI` identifie incorrectement les fichiers [!DNL InDesign] comme `x-adobe-indesign` au lieu de `x-indesign`. (ASSETS-45953)
* Fuite de session [!DNL AEM 6.5.21] identifiée à l’étape de workflow prête à l’emploi **[!UICONTROL Publication planifiée sur Brand Portal]**. (ASSETS-44104)
* Les erreurs **[!UICONTROL Mémoire insuffisante]** s’affichent dans [!DNL AEM] lors du traitement et de la publication des images. Ce problème était dû à des méthodes obsolètes dans les workflows, par exemple **[!DNL Dam Asset update]** et **[!DNL Dynamic Media: Reprocess assets]**. (ASSETS-43343)
* Après avoir apporté une modification mineure, comme la mise à jour du titre, vous rouvrez et réenregistrez la **[!DNL Connected Assets configuration]** sur l’instance Sites locale. L’instance distante perd alors sa connexion à l’instance locale. Par conséquent, elle ne peut pas établir de communication avec l’instance Sites locale. (ASSETS-44484)
* Dans [!DNL AEM 6.5.21], lorsqu’un chargement de ressources dans la vue Liste est annulé et qu’un second chargement est effectué, [!DNL AEM] affiche une erreur **[!UICONTROL 0 sur NaN ressources chargées]**. (ASSETS-44124)

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

Le package de module complémentaire hybride est disponible publiquement dans la distribution de logiciels d’Adobe à compter du jeudi 22 mai 2025, avec la version officielle d’AEM 6.5.23. Les utilisateurs et utilisatrices peuvent le trouver en recherchant **Package de module complémentaire hybride AEM 6.5 Dynamic Media** dans la distribution de logiciels.


### [!DNL Forms]{#forms-6523}

#### Concepteur Forms

* Lorsque la personne exporte les données d’un PDF XFA à l’aide de l’API exportData, le fichier XML obtenu présente des incohérences par rapport aux données XML exportées manuellement à l’aide d’Acrobat Reader. Les valeurs de certains champs étaient manquantes dans la sortie par rapport à la sortie générée à partir d’Acrobat Reader. (LC-3922791)

* Dans AEM Forms 6.5.22.0, la génération d’un PDF balisé avec le service Output dans Workbench ajoute une balise label inattendue sous la balise reference dans un élément de table des matières. (LC-3922756)

* Lorsque la personne place des légendes de champ avec un alignement inférieur ou droit dans AEM Forms Designer, l’arborescence des balises inclut uniquement la légende sans la valeur correspondante, ce qui entraîne un balisage d’accessibilité incomplet. (LC-3922619)

* Lors de la mise à niveau du pack de service 6 d’AEM Forms 6.5 vers le pack de service 20 d’AEM Forms, les codes QR dans les PDF générés deviennent illisibles. Le texte secondaire des codes QR échoue également aux tests d’accessibilité, ce qui affecte la compatibilité des lecteurs d’écran. (LC-3922551)

* Lorsqu’un utilisateur ou une utilisatrice effectue le rendu d’une lettre dans l’interface d’utilisation de l’agent sur le pack de services 18 d’AEM Forms, le contenu ne s’affiche pas correctement en raison de l’API FormService.render(). (LC-3922461)

#### Formulaires

* Dans AEM Forms, l’activation de l’option « Autoriser le texte enrichi pour le titre » sur le panneau racine entraîne une interaction incorrecte avec l’option « Exclure le titre du document de référence » sur un panneau imbriqué, qui masque alors à tort le titre du panneau racine. Ce comportement se produit dans le document de référence généré. (FORMS-19696)

* Le système ignore la valeur personnalisée `sling:resourceType` définie via `aem:afProperties` dans un schéma JSON sur AEM 6.5. Le type de ressource personnalisé est ignoré lors du rendu. (FORMS-19691)

* Lorsqu’une personne envoie un formulaire adaptatif avec des pièces jointes préremplies à l’aide d’URI, l’envoi du formulaire échoue avec une NullPointerException en raison de données binaires manquantes. (FORMS-19371) (FORMS-19486)

* Lorsqu’une personne charge un PDF sous la section « Formulaires et documents » dans AEM 6.5 Forms, la fonction de chronologie cesse de fonctionner. (FORMS-19407) (FORMS-19234)

* Lorsqu’une personne charge des fichiers à l’aide du composant de pièce jointe prêt à l’emploi dans AEM Forms, des vulnérabilités en matière de sécurité sont identifiées. Ce problème peut entraîner l’interception du processus de soumission par des entités non autorisées. (FORMS-19271)

* Lorsqu’un utilisateur ou une utilisatrice configure un formulaire adaptatif standard dans AEM Forms pour générer automatiquement un document de référence, le champ « Titre » dans les propriétés du document d’Acrobat Reader n’affiche pas le titre capturé du document de référence. Par défaut, le titre du formulaire ne remplace pas le nom de fichier. (FORMS-19263)

* Lorsqu’une personne ouvre une communication interactive dans l’interface d’utilisation de l’agent, les données préremplies ne peuvent pas être complètement effacées ; une fois supprimées, elles sont automatiquement remplies avec les mêmes données. (FORMS-19151)

* Lorsqu’un utilisateur ou une utilisatrice prévisualise un champ de type date dans l’interface Agent, la date change de façon inattendue. Ce comportement résulte de différences de fuseau horaire entre le paramètre UTC de la machine virtuelle et l’interprétation locale de la date par le système. (FORMS-19115)

* Lorsqu’un utilisateur ou une utilisatrice soumet un formulaire, les pièces jointes peuvent être dupliquées, entraînant plusieurs envois du même fichier. (FORMS-19045)(FORMS-19051).

* L’ajout de coordinateurs et coordinatrices aux jeux de politiques dans AEM 6.5 Document Security échoue dans les environnements de production et inférieurs. (FORMS-18603, FORMS-18212, FORMS-19697)

* Lorsqu’une personne clique sur « datepicker-calendar-icon » en mode bureau avec un champ vide dans le pack de services 22 d’AEM Forms, une erreur se produit en raison de la variable _$focusedDate non définie, interrompant les scripts personnalisés associés. (FORMS-18483)(FORMS-18268).

* Dans le pack de services 19 (6.5.19.0) d’AEM Forms, lorsqu’un client ou une cliente prévisualise une lettre, le champ « Montant en mots » ne s’affiche pas correctement ou ne met pas à jour correctement les valeurs numériques, ce qui entraîne un mauvais alignement et des espaces manquants dans le contenu. (FORMS-18437, FORMS-17330, FORMS-18209, FORMS-18557, CTG-4150848,FORMS-19614, LC-3922004)

* Lorsqu’un client ou une cliente prévisualise une lettre enregistrée dans le pack de services 19 d’AEM Forms 6.5 sur RHEL, le contenu ne s’aligne pas correctement, des espaces sont manquantes et des caractères inattendus tels que « x » apparaissent. (FORMS-18422)(FORMS-17641).

* Lorsqu’une personne navigue entre les onglets d’AEM Forms, la sélection de composants dans le premier onglet ne répond plus. (FORMS-18345)

* Dans AEM Forms 6.5.21.0, lorsqu’une personne convertit un fichier HTML en PDF à l’aide de l’option WebToPDF, la section d’en-tête est manquante dans le PDF de sortie, y compris les balises de métadonnées et de titre. (FORMS-18223, FORMS-17835, FORMS-19642, FORMS-18224)

* Dans le SDK du gestionnaire de processus AEM JEE, lorsqu’une personne appelle la méthode retryAction(long actionOid), le système tente à nouveau, de manière incorrecte, la première action trouvée dans la table tb_action_instance. Ce workflow se produit même lorsqu’un identifiant d’action spécifique est fourni, ou lorsqu’il est nul, ce qui engendre des effets inattendus. (FORMS-18187)

* Après la mise à jour vers SP22, des problèmes peuvent survenir lors de l’enregistrement d’un brouillon ou de la soumission du formulaire, sans qu’aucun message d’erreur ne s’affiche. (FORMS-18069)

* Dans AEM 6.5.21.0, la transition des composants de base basés sur XSD vers les composants principaux empêche l’implémentation de références entre fichiers dans les schémas JSON, ce qui a un impact sur la migration des formulaires adaptatifs. (FORMS-18065)

* Lorsqu’une personne prévisualise une lettre dans l’interface d’utilisation de l’agent, le champ de date affiche une valeur incorrecte en raison de problèmes de conversion d’heure IC (communication interactive). Ces dysfonctionnements sont liés à des écarts de fuseau horaire entre l’environnement VM et l’interprétation de l’heure par le système (UTC contre heure locale). (FORMS-17988) (FORMS-17248)

* Lorsqu’une personne prévisualise des lettres à l’aide de modèles Notice IC dans AEM Forms, les délais de génération de PDF varient considérablement, passant de 1,5 seconde à plus de 10 secondes, même sur le même serveur. Cette incohérence affecte les workflows critiques de l’entreprise. (FORMS-17951)

* Lorsqu’un utilisateur ou une utilisatrice associe un objet de signature manuscrite (Scribble Signature) dans un formulaire adaptatif à un XDP via l’option « Sources de données », les modifications ne peuvent pas être enregistrées. Cela est dû à des erreurs persistantes de validation du ratio d’aspect, même avec des valeurs valides. (FORMS-17587)

* Lorsqu’un utilisateur ou une utilisatrice utilise un XDP spécifique contenant de nombreux champs masqués pour les fragments de document, AEM crée des nœuds CRX avec la propriété `cm:optional` définie sur faux, ce qui entraîne l’échec de la soumission dans communication interactive (IC). (FORMS-17538)

* Dans AEM Forms 6.5.19.0, lorsqu’un client ou une cliente prévisualise une lettre, le champ de zone numérique ne gère pas correctement les valeurs négatives lorsque des limites numériques pour le lead et le fractionnement sont définies. Ce problème se produit en raison de l’utilisation de parseFloat, qui traite le signe moins comme faisant partie du nombre. (FORMS-17451)

* Sur AEM Forms 6.5, lorsqu’une lettre est prévisualisée, la présence du caractère générique « * » dans le fichier Adobe.json est détectée, ce qui soulève des interrogations quant à son utilité et à la possibilité de le modifier. (FORMS-17317)

* Lorsqu’un utilisateur ou une utilisatrice utilise un lecteur d’écran sur le `Apply for a Fixed Rate Saver joint account`, les titres sont annoncés de manière incorrecte comme `clickable`, ce qui entraîne des problèmes d’accessibilité. (FORMS-17038)

* Lorsqu’un formulaire est incorporé, il manque un attribut de titre à l’iframe généré, ce qui entraîne un problème de conformité en matière d’accessibilité. (FORMS-17010)

* Le téléchargement d’un formulaire depuis l’interface Forms Manager inclut toujours les dépendances associées, telles que les thèmes et les fragments. (FORMS-15811)

* Lorsqu’un utilisateur ou une utilisatrice accède au formulaire sur un appareil mobile (iOS ou Android™), les boutons « Suivant » et « Précédent » de la première page sont désactivés. Toutefois, le lecteur d’écran ne les identifie pas comme tels. (FORMS-15773)

* Lorsqu’une personne enregistre un formulaire volumineux avec des fragments et un chargement différé activés, la récupération des brouillons échoue, ce qui perturbe le workflow. (FORMS-19890, FORMS-19808)

#### Forms JEE

* Lorsqu’une personne reconfigure la base de données dans AEM Forms, la connexion échoue en raison de paramètres codés en dur. (FORMS-19568, FORMS-17621)

* Lorsqu’un utilisateur ou une utilisatrice configure AEM 6.5 avec MySQL 8.4 en utilisant la méthode partial turnkey, le gestionnaire de configuration LiveCycle (LCM) ne reconnaît pas le pilote de connexion MySQL requis. Cela entraîne l’échec du test de connexion à la base de données ainsi que de la configuration. (FORMS-19442)

* Lorsqu’un utilisateur ou une utilisatrice exécute LCM avec JDBC 12.8.1 sur JRE 11 dans un environnement JEE, la configuration échoue en raison de problèmes d’incompatibilité. (FORMS-19276)

* Lorsqu’une personne ouvre une tâche dans AEM On-Premise, le système exécute le profil d’action de démarrage Workspace au lieu du profil d’utilisation affecté. (FORMS-19065)

* Lorsqu’un utilisateur ou une utilisatrice utilise la méthode retryAction(long actionOid) dans le gestionnaire de processus AEM JEE, un comportement inattendu se produit. (FORMS-18357)(FORMS-18187).

* Sur AEM Forms 6.5.21.0, la conversion PDFG échoue avec l’erreur suivante : (FORMS-16851) (FORMS-14613)

#### Captcha de formulaires {#forms-captcha-6523}

* Amélioration des alertes reCAPTCHA dans les formulaires adaptatifs en mettant à jour les codes d’erreur d’envoi à 400. En outre, les alertes de journal ont été affinées pour faire la distinction entre les délais d’expiration, les expirations, les échecs de détection des robots et pour améliorer la précision du dépannage et l’observabilité du système. (FORMS-19240)
* Fermeture d’une instance de `ResourceResolver` non fermée dans `ReCaptchaConfigurationServiceImpl` pour éviter des fuites de ressources potentielles et améliorer la stabilité du système lors de l’utilisation des intégrations reCAPTCHA dans AEM Forms. (FORMS-19242)
* Amélioration de la gestion de la configuration CAPTCHA pour AEM Forms en veillant à ce que la bonne configuration se lie à chaque formulaire lorsqu’il existe plusieurs entrées dans le dossier `/conf/global`. Empêche l’utilisation involontaire de paramètres CAPTCHA incorrects lorsque le conteneur de configurations n’est pas explicitement sélectionné. (FORMS-19239)

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

* Correction d’un problème dans les bannières d’alerte Coral en raison duquel la couleur du texte apparaissait en blanc au lieu du noir après la mise à niveau vers le pack de services 21. Garantit l’application d’un style approprié pour maintenir un contraste et une lisibilité adéquats des messages d’alerte dans l’interface. (NPR-42359)
* Ajout de la prise en charge de l’intégration OAuth dans la configuration des balises intelligentes pour s’aligner sur l’obsolescence de JWT (jeton web JSON). Garantit le maintien des fonctionnalités des balises intelligentes à l’aide des méthodes d’authentification mises à jour. (NPR-42296)

#### Apache Felix {#foundation-apachefelix-6523}

Correction d’une exception NullPointerException qui se produisait lors du chargement de fichiers de clé privée vers un champ de propriété de type binaire dans CRX, restaurant la compatibilité du pack de services 16. Active les workflows de chargement de fichiers de clés sécurisés dans AEM Managed Services sans erreurs de serveur ni interruption des processus de renouvellement de certificat. (CQ-4359178)


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

* Résolution des cycles de dépendance OSGi entre les services de script Apache Sling qui provoquaient des retards ou des échecs lors du chargement des pages HTML après la mise à niveau vers le pack de services 21. Mise à jour des références de service internes afin d’éliminer les dépendances cycliques impliquant des composants `SightlyScriptingEngineFactory` et associés, ce qui améliore la fiabilité et le comportement de démarrage du moteur de script. (GRANITE-56808)
* Mise à jour des scripts JS dans Apache Sling pour qu’ils se chargent uniquement à la demande plutôt que rapidement au démarrage, ce qui élimine les conflits de thread et réduit le risque que les serveurs de publication ne répondent pas lors du chargement. Cette modification améliore la stabilité du serveur et les temps de réponse lors de scénarios à trafic élevé en empêchant le verrouillage des ressources provoqué par une résolution précoce du script. (GRANITE-56611)
* Correction d’un problème dans AEM Omnisearch en raison duquel les espaces réservés des champs de saisie s’affichaient incorrectement sous forme de libellés, ce qui entraînait une confusion visuelle. Permet d’assurer un rendu adéquat des espaces réservés dans les champs de filtre, en assurant un comportement de formulaire cohérent et accessible. (GRANITE-51791)
* Correction d’une erreur de serveur déclenchée lors de la sélection de plus de 30 modèles de fragments de contenu (CFM) avec des références à plusieurs champs dans l’éditeur de modèle de fragment de contenu. Amélioration du composant de suggestion de filtre pour la prise en charge des opérations POST. Cette fonctionnalité permet de gérer correctement les jeux de références volumineux lors de la création de fragments de contenu et d’améliorer la stabilité des configurations de modèle à volume élevé. (GRANITE-57164)
* Correction d’un problème dans les modèles de fragments de contenu en raison duquel cliquer près d’une case à cocher changeait involontairement son état. Mise à jour des styles pour limiter strictement l’activation des clics à l’élément de case à cocher, empêchant les interactions accidentelles de l’utilisateur ou de l’utilisatrice et améliorant l’utilisation et l’accessibilité des formulaires. (GRANITE-52384)


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

Correction d’un problème en raison duquel la validation SNI bloquait les appels API via HTTPS pour les clientes et clients AEM utilisant des configurations SSL Dispatcher avec des en-têtes d’hôte personnalisés. Introduit une option pour désactiver la validation SNI dans le cadre de la configuration Jetty, permettant la compatibilité avec des configurations de proxy inverse spécifiques lorsque `mod_proxy` n’est pas possible. (NPR-42614)


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### Plateforme{#foundation-platform-6523}

* Correction d’un comportement de fusion de balises incohérent en s’assurant que la valeur de la balise fusionnée s’affiche toujours correctement dans les ressources, que les balises soient créées en ligne ou par la méthode standard. Empêche les valeurs résiduelles des champs `EN:title` de remplacer l’affichage de la balise fusionnée. (CQ-4358812)
* Correction du codage répété de l’esperluette dans les valeurs de balise dans la boîte de dialogue de modification de balise. Empêche l’ajout d’entités « &amp; » supplémentaires à chaque enregistrement, ce qui garantit que les valeurs des balises restent nettes et cohérentes entre les modifications et évite les erreurs d’affichage dans le contenu créé. (CQ-4359048)
* Correction d’une erreur `ClassCastException` qui empêchait la diffusion d’e-mails lors de l’envoi d’un formulaire adaptatif dans AEM 6.5 sur WebSphere®. Le correctif permet une transmission réussie des e-mails en assurant la compatibilité entre `com.sun.mail.handlers.text_plain` et `java.activation.DataContentHandler`, en s’alignant sur la configuration du gestionnaire de messagerie adaptée aux environnements WebSphere®. (NPR-42500)
* Amélioration de la gestion des erreurs dans le gestionnaire de packages, en veillant à ce qu’AEM affiche un message clair lorsque l’installation échoue et que la réponse d’erreur est vide dans le cas contraire. Ce correctif empêche les échecs silencieux et permet un débogage plus rapide lors du déploiement des packages. (NPR-42375)

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### Traduction{#foundation-translation-6523}

Correction d’une erreur NullPointerException (NPE) déclenchée lors de la mise à jour de fragments de contenu dans les workflows à l’aide de la fonctionnalité **Mettre à jour la copie linguistique**. Ce correctif garantit que les workflows ne passent pas à un état d’échec ou ne restent pas bloqués dans un état d’exécution lors de la modification du contenu lié aux références de traduction. (NPR-42115)

#### Interface d’utilisation{#foundation-ui-6523}

Ajoute des attributs `title` manquants aux boutons de boîte de dialogue de l’interface d’utilisation Coral, comme **Terminé** et **Annuler** dans les boîtes de dialogue de modification des composants afin d’améliorer l’accessibilité et de permettre la validation automatisée. Garantit que les boutons conservent les attributs attendus dans le rendu du balisage, ce qui permet d’éviter les échecs dans les tests d’interface d’utilisation basés sur Selenium. (NPR-42412)

#### Gestion de contenu web (WCM){#foundation-wcm-6523}

Correction d’un problème qui empêchait l’ajout de pages aux traitements de traduction lors de l’utilisation de la fonctionnalité **Mettre à jour la copie linguistique** dans les environnements avec le pack de services 19 ou une version ultérieure. Garantit que les workflows de traduction se déroulent comme prévu, ce qui permet un transfert de page correct entre les copies linguistiques sans intervention manuelle. (CQ-4357929)

#### Workflow{#foundation-workflow-6523}

Correction d’un problème dans l’élément `EmailNotificationServiceProcessor` en raison duquel la méthode `getSegmentId` renvoie `null` après le déploiement du correctif, ce qui entraînait l’échec des déclencheurs d’e-mail lors du traitement du workflow. Restaure la logique de résolution correcte de l’identifiant de segment en s’assurant que le processeur récupère les valeurs `SegmentInfo` requises pour prendre en charge les workflows de notification par e-mail sur les instances AEM. (CQ-4359755)


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

Consultez [Fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md/) pour obtenir une liste détaillée de toutes les fonctionnalités obsolètes ou supprimées pour AEM 6.5.

### Éditeur de SPA {#spa-editor}

[L’éditeur de SPA](/help/sites-developing/spa-overview.md) a été abandonné pour les nouveaux projets à partir de la version 6.5.23 d’AEM 6.5. L’éditeur de SPA reste pris en charge pour les projets existants, mais ne doit pas être utilisé pour de nouveaux projets.

Les éditeurs privilégiés pour la gestion du contenu découplé dans AEM sont désormais les suivants :

* [Éditeur universel](/help/sites-developing/universal-editor/introduction.md) pour la modification visuelle.
* [Éditeur de fragments de contenu](/help/sites-developing/universal-editor/introduction.md) pour la modification basée sur les formulaires.

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Problème avec le lot de script JSP dans AEM 6.5.21-6.5.23 et AEM 6.5 LTS (disponibilité générale)**
AEM 6.5.21, 6.5.22, 6.5.23 et AEM 6.5 LTS (disponibilité générale) sont fournis avec le lot `org.apache.sling.scripting.jsp:2.6.0`, qui contient un problème connu. Le problème se produit généralement sous une charge élevée lorsque l’instance AEM gère de nombreuses requêtes simultanées.

  Lorsque ce problème se produit, l’une des exceptions suivantes peut apparaître dans les journaux d’erreurs avec des références à `org.apache.sling.scripting.jsp:2.6.0` :

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  Lorsque cette erreur se produit, la seule méthode de récupération consiste à redémarrer l’instance AEM.

  Contactez le service clientèle d’Adobe et mentionnez cette note de mise à jour pour obtenir une résolution.

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

### Problèmes connus d’AEM Forms {#known-issues-aem-forms-6523}

>[!NOTE]
>
> N’effectuez pas la mise à niveau vers le Pack de services 6.5.23.0 pour les problèmes ne disposant pas de correctifs, car cela peut entraîner des erreurs inattendues. Effectuez la mise à niveau vers le pack de services 6.5.23.0 uniquement après la publication des correctifs requis.

#### Problèmes avec des correctifs disponibles {#aem-forms-issues-with-hotfixes}

Un correctif logiciel peut être téléchargé et installé pour les problèmes suivants. Pour résoudre ces problèmes, vous pouvez [télécharger et installer le correctif](/help/release-notes/aem-forms-hotfix.md) :

* **FORMS-20203** : Lorsqu’un utilisateur ou une utilisatrice met à niveau le framework Struts de la version 2.5.x à la version 6.x, l’UI des politiques dans AEM Forms n’affiche pas toutes les configurations, telles que l’option d’ajout d’un filigrane.

* **FORMS-20360** : après la mise à niveau vers le pack de services 6.5.23.0 d’AEM Forms, le service de conversion ImageToPDF échoue avec l’erreur :
  ```17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp```

* **FORMS-20478** : lors de la tentative de conversion de fichiers TIFF de type 7/8 en PDF, le processus de conversion échoue avec l’erreur « ALC-PDG-001-000-Échec de la conversion Image2Pdf, en raison de : com/sun/image/codec/jpeg/JPEGCodec » et « ALC-PDG-016-003-Une erreur inconnue/inattendue s’est produite lors du post-traitement PDF. ». Le système tente d’effectuer une nouvelle tentative d’utiliser le décodeur TIFF ImageIO de TM, mais ne parvient pas à terminer le traitement.

* **FORMS-14521** : si un utilisateur ou une utilisatrice tente de prévisualiser un brouillon de lettre avec des données XML enregistrées, certaines lettres spécifiques restent bloquées à l’état `Loading`.

* AEM Forms comprend désormais une mise à niveau de Struts, de la version 2.5.33 vers la version 6.x, pour le composant de formulaire. Cela permet d’obtenir les modifications apportées à Struts et précédemment manquées qui n’étaient pas incluses dans SP23. La prise en charge a été ajoutée via un [correctif](/help/release-notes/aem-forms-hotfix.md) que vous pouvez télécharger et installer. La dernière version de Struts est alors prise en charge.

#### Autres problèmes connus {#aem-forms-other-known-issues}

* Après l’installation du pack de services AEM Forms JEE 21 (6.5.21.0), vous pouvez trouvez des entrées en double de fichiers JAR Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` sous le dossier `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926). Suivez ces étapes pour résoudre le problème :

   1. Arrêtez les localisateurs s’ils sont en cours d’exécution.
   2. Arrêtez le serveur AEM.
   3. Accédez à `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Supprimez tous les fichiers de correctifs Geode, à l’exception de `geode-*-1.15.1.2.jar`. Confirmez que seuls les fichiers JAR Geode avec `version 1.15.1.2` sont présents.
   5. Ouvrez l’invite de commande en mode administration.
   6. Installez le correctif Geode à l’aide du fichier `geode-*-1.15.1.2.jar`.

* Après la mise à niveau du pack de services 18 ou 19 d’AEM Forms 6.5 vers le pack de services 20 ou 21, une erreur de compilation JSP s’affiche. Cette erreur empêchait d’ouvrir ou de créer des formulaires adaptatifs. Cela provoquait également des problèmes avec d’autres interfaces AEM. Ces interfaces comprenaient l’éditeur de page, l’interface d’utilisation d’AEM Forms, l’éditeur de workflow et l’interface d’utilisation Présentation du système. (FORMS-15256)

  Si vous rencontrez ce problème, procédez comme suit pour le résoudre :
   1. Accédez au répertoire `/libs/fd/aemforms/install/` dans CRXDE.
   2. Supprimez le lot dont le nom est `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Redémarrez votre serveur AEM.

* Dans l’aperçu avant impression de l’IU de l’agent de communication interactive, le symbole monétaire (comme le symbole du dollar « $ ») s’affiche de manière incohérente pour toutes les valeurs de champ. Il s’affiche pour les valeurs allant jusqu’à 999, mais il est absent pour les valeurs supérieures ou égales à 1 000. (FORMS-16557)
* Les modifications apportées au fichier XDP des fragments de mise en page imbriqués dans une communication interactive ne sont pas répercutées dans l’éditeur de communication interactive. (FORMS-16575)
* Dans l’aperçu avant impression de l’IU de l’agent de communication interactive, certaines valeurs calculées ne s’affichent pas correctement. (FORMS-16603)
* Lorsque la lettre est affichée dans l’aperçu avant impression, le contenu change. Certains espaces disparaissent et certaines lettres sont remplacées par `x`. (FORMS-15681)
* **FORMS-15428** : après la mise à jour vers le pack de services 20 (6.5.20.0) d’AEM Forms avec le module complémentaire Forms, les configurations reposant sur l’ancien service Adobe Analytics Cloud à l’aide de l’authentification basée sur les informations d’identification ne fonctionnent plus. Ce problème empêchait les règles d’analyse de s’exécuter correctement.

* Lorsqu’un utilisateur ou une utilisatrice configure une instance WebLogic 14c, le service PDFG dans le pack de services 21 d’AEM Forms sur JEE (6.5.21.0) s’exécutant sur JBoss® échoue en raison de conflits de chargeurs de classes impliquant la bibliothèque SLF4J. L’erreur s’affiche comme suit (CQDOC-22178) :

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```

* FORMS-21378 : lorsque la validation côté serveur (SSV) est activée, les envois de formulaires peuvent échouer. Si vous rencontrez ce problème, contactez l’assistance Adobe pour obtenir de l’aide.



## Lots OSGi et packages de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans cette version du pack de services [!DNL Experience Manager] 6.5.

* [Liste des lots OSGi inclus dans Experience Manager 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites web sont disponibles uniquement pour les clientes et clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/fr/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-65)
>* [S’abonner aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)
