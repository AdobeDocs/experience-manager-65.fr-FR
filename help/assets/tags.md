---
title: Intégration de visionneuses Dynamic Media à Adobe Analytics et Experience Platform Tags
description: Découvrez-en plus sur l’extension Visionneuses Dynamic Media pour Experience Platform Tags et les visionneuses Dynamic Media 5.13. Elle permet aux clients d’Adobe Analytics et aux utilisateurs d’Experience Platform Tags d’utiliser des événements et des données spécifiques aux visionneuses dans leur configuration Experience Platform Tags.
mini-toc-levels: 3
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Viewers
role: User, Admin,Developer,Data Engineer,Data Architect
exl-id: 161dfe22-bc1c-4b60-8ab6-a19407a39e2e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '6664'
ht-degree: 99%

---

# Intégration de visionneuses Dynamic Media à Adobe Analytics et Experience Platform Tags {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## En quoi consiste l’intégration des visionneuses Dynamic Media à Adobe Analytics et à Experience Platform Tags ? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch -->

L’extension *Visionneuses Dynamic Media* pour les Experience Platform Tags et les visionneuses Dynamic Media 5.13, permet aux clients Adobe Analytics et Experience Platform Tags d’utiliser des événements et des données spécifiques aux visionneuses Dynamic Media dans leur configuration Experience Platform Tags.

Cette intégration signifie que vous pouvez suivre l’utilisation des visionneuses Dynamic Media sur votre site web avec Adobe Analytics. Dans le même temps, vous pouvez utiliser les événements et les données exposés par les visiteurs avec toute autre extension Experience Platform Tags provenant d’Adobe ou d’un tiers.

Pour en savoir plus sur les extensions d’Adobe ou les extensions tierces, voir [Extensions d’Adobe](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html?lang=fr) dans le Guide de l’utilisateur Experience Platform Tags.

**Cette rubrique est destinée** à l’équipe d’administration de site, à l’équipe de développement d’Experience Platform et aux personnes qui participent à son exploitation.

### Restrictions de l’intégration {#limitations-of-the-integration}

* L’intégration Experience Platform Tags pour les visionneuses Dynamic Media ne fonctionne pas dans le nœud d’auteur d’Experience Manager. Vous ne pouvez pas afficher de suivi à partir d’une page WCM tant qu’elle n’est pas publiée.
* L’intégration Experience Platform Tags pour les visionneuses Dynamic Media n’est pas prise en charge pour le mode de fonctionnement « pop-up », où l’URL de la visionneuse est obtenue à l’aide du bouton URL de la page de détails de la ressource.
* L’intégration Experience Platform Tags ne peut pas être utilisée simultanément avec l’intégration des visionneuses Analytics héritées (au moyen du paramètre `config2=`).
* La prise en charge du suivi vidéo se limite au suivi de la lecture principale uniquement, comme décrit dans la section [Présentation du suivi](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-core-overview.html?lang=fr). En particulier, le suivi de la qualité de service, des publicités, des chapitres/segments et des erreurs n’est pas pris en charge.
* La configuration de la durée de stockage n’est pas prise en charge pour les éléments de données à l’aide de l’extension *Visionneuses Dynamic Media*. La durée de stockage doit être définie sur **[!UICONTROL Aucune]**.

### Cas d’utilisation de l’intégration {#use-cases-for-the-integration}

Le principal cas d’utilisation d’intégration avec Experience Platform Tags concerne les clients qui utilisent à la fois Adobe Experience Manager Assets et Adobe Experience Manager Sites. Dans de tels scénarios, vous pouvez configurer une intégration standard entre le nœud d’auteur Experience Manager et Experience Platform Tags, puis associer votre instance Sites à la propriété Experience Platform Tags. Ensuite, tout composant WCM Dynamic Media ajouté à une page Sites suit les données et les événements des visiteurs.

Consultez [Suivi des visionneuses Dynamic Media dans Experience Manager Sites](#tracking-dynamic-media-viewers-in-aem-sites).

Un autre cas d’utilisation pris en charge par l’intégration est celui des clients qui utilisent Experience Manager Assets uniquement ou également Dynamic Media Classic. Dans ce cas, vous obtenez le code intégré pour votre visionneuse et vous l’ajoutez à la page du site web. Ensuite, récupérez l’URL de production de la bibliothèque Experience Platform Tags et ajoutez-la manuellement au code de la page web.

Consultez [Suivre des visionneuses Dynamic Media à l’aide du code intégré](#tracking-dynamic-media-viewers-using-embed-code).

<!-- Path on internal wiki [About tracking Dynamic Media viewers using embed code](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode). -->

## Fonctionnement du suivi des données et des événements dans l’intégration {#how-data-and-event-tracking-works-in-the-integration}

L’intégration tire parti de deux types distincts et indépendants de suivi des visionneuses Dynamic Media : *Adobe Analytics* et *Adobe Analytics for Audio and Video*.

### À propos du suivi à l’aide d’Adobe Analytics   {#about-tracking-using-adobe-analytics}

Adobe Analytics vous permet d’effectuer le suivi des actions exécutées par l’utilisateur final lorsqu’il interagit avec les visionneuses Dynamic Media de votre site web. Adobe Analytics vous permet également d’effectuer le suivi des données propres à la visionneuse. Vous pouvez, par exemple, effectuer le suivi et enregistrer les événements de chargement des vues avec le nom de la ressource, les actions de zoom survenues et les actions de lecture vidéo.

Dans Experience Platform Tags, les concepts d’*éléments de données* et de *règles* fonctionnent ensemble pour activer le suivi Adobe Analytics.

#### À propos des éléments de données dans Experience Platform Tags {#about-data-elements-in-adobe-launch}

Un élément de données dans Experience Platform Tags est une propriété nommée dont la valeur est définie de manière statique ou calculée de manière dynamique en fonction du statut d’une page web ou des données des visionneuses Dynamic Media.

Les options disponibles pour une définition d’élément de données dépendent de la liste des extensions installées dans la propriété Experience Platform Tags. L’extension Core est préinstallée et prête à l’emploi dans n’importe quelle configuration. Cette extension Core permet de définir un élément de données dont la valeur provient d’un cookie, de code JavaScript, d’une chaîne de requête, ainsi que de nombreuses autres sources.

Pour le suivi d’Adobe Analytics, d’autres extensions doivent être installées, tel que décrit dans la section [Installation et configuration des extensions](#installing-and-setup-of-extensions). L’extension Visionneuses Dynamic Media permet de définir un élément de données qui est une valeur d’argument de l’événement Visionneuse dynamique. Par exemple, il est possible de faire référence au type de visionneuse ou au nom de ressource indiqué par la visionneuse lors du chargement, au niveau de zoom indiqué lorsque l’utilisateur effectue un zoom, etc.

L’extension Visionneuse Dynamic Media actualise automatiquement les valeurs de ses éléments de données.

Une fois défini, un élément de données peut être utilisé dans d’autres emplacements de l’interface utilisateur Experience Platform Tags, à l’aide du widget de sélecteur d’éléments de données. En particulier, les éléments de données définis à des fins de suivi des visionneuses Dynamic Media sont référencés par l’action Définir les variables de l’extension Adobe Analytics dans la règle (voir ci-dessous).

Consultez la section [Éléments de données](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html?lang=fr).

#### À propos des règles dans Experience Platform Tags {#about-rules-in-adobe-launch}

Une règle dans Experience Platform Tags est une configuration agnostique définissant trois zones qui constituent une règle : *Événements*, *Conditions* et *Actions* :

* Les *événements* (si) indiquent à Experience Platform Tags quand déclencher une règle.
* Les *conditions* (si) indiquent à Experience Platform Tags quelles restrictions supplémentaires autoriser ou non lors du déclenchement d’une règle.
* Les *actions* (alors) indiquent à Experience Platform Tags ce qu’il faut faire lorsqu’une règle est déclenchée.

Les options disponibles dans la section Événements, Conditions et Actions dépendent des extensions installées dans la propriété Experience Platform Tags. L’extension *Core* est préinstallée et prête à l’emploi dans n’importe quelle configuration. L’extension fournit plusieurs options pour les événements, telles que des actions de base au niveau du navigateur. Ces actions comprennent le changement de focus, les fonctions des touches et les envois de formulaire. Elle comprend également des options pour les conditions, telles que la valeur du cookie, le type de navigateur, etc. Pour les actions, seule l’option Code personnalisé est disponible.

Pour le suivi d’Adobe Analytics, d’autres extensions doivent être installées, tel que décrit dans [Installation et configuration des extensions](#installing-and-setup-of-extensions). Plus précisément :

* L’extension Visionneuses Dynamic Media étend la liste des événements pris en charge aux événements spécifiques aux visionneuses Dynamic Media, tels que le chargement de la visionneuse, l’échange de ressources, le zoom avant et la lecture vidéo.
* L’extension Adobe Analytics étend la liste des actions prises en charge avec deux actions requises pour envoyer des données aux serveurs de suivi : *Définir des variables* et *Envoyer une balise*.

Pour effectuer le suivi des visionneuses Dynamic Media, vous pouvez utiliser n’importe quel type des éléments suivants :

* Événements de l’extension Visionneuses Dynamic Media, de l’extension Core ou de toute autre extension.
* Conditions de la définition de règle. Vous pouvez également laisser la zone Conditions vide.

Dans la section Actions, vous devez disposer d’une action *Définir les variables*. Cette action indique à Adobe Analytics comment renseigner les variables de suivi avec des données. Parallèlement, l’action *Définir les variables* n’envoie rien au serveur de suivi.

L’action *Définir les variables* doit être suivie d’une action *Envoyer une balise*. L’action *Envoyer la balise* envoie en fait des données au serveur de suivi Analytics. Les deux actions, *Définir les variables* et *Envoyer une balise*, proviennent de l’extension Adobe Analytics.

Consultez la section [Règles](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html?lang=fr).

#### Exemple de configuration {#sample-configuration}

L’exemple de configuration suivant dans Experience Platform Tags montre comment effectuer le suivi d’un nom de ressource lors du chargement de la visionneuse.

1. Dans l’onglet **[!UICONTROL Éléments de données]**, définissez un élément de données `AssetName` qui référence le paramètre `asset` de l’événement `LOAD` à partir de l’extension Visionneuses Dynamic Media.

   ![image2019-11](assets/image2019-11.png)

1. Dans l’onglet **[!UICONTROL Règles]**, définissez une règle *TrackAssetOnLoad*.

   Dans cette règle, le champ **[!UICONTROL Événement]** utilise l’événement **[!UICONTROL LOAD]** de l’extension Visionneuses Dynamic Media.

   ![image2019-22](assets/image2019-22.png)

1. La configuration Action comporte deux types d’actions de l’extension Adobe Analytics :

   *Définissez des variables* qui mappent une variable Analytics de votre choix à la valeur de l’élément de données `AssetName`.

   *Envoyer une balise*, qui envoie les informations de suivi à Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. La configuration de règle résultante ressemble à ce qui suit :

   ![image2019-4](assets/image2019-4.png)

### À propos d’Adobe Analytics for Audio and Video {#about-adobe-analytics-for-audio-and-video}

Lorsqu’un compte Experience Cloud est abonné pour utiliser Adobe Analytics for Audio and Video, il suffit d’activer le suivi vidéo dans les paramètres d’extension *Visionneuses Dynamic Media*. Les mesures vidéo sont alors disponibles dans Adobe Analytics. Le suivi vidéo dépend de la présence de l’extension Adobe Media Analytics for Audio and Video.

Voir [Installation et configuration des extensions](#installing-and-setup-of-extensions).

À l’heure actuelle, la prise en charge du suivi vidéo se limite au suivi de la lecture principale uniquement, comme décrit dans la section [Présentation du suivi](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-core-overview.html?lang=fr). En particulier, le suivi de la qualité de service, des publicités, des chapitres/segments et des erreurs n’est pas pris en charge.

## Utilisation de l’extension Visionneuses Dynamic Media {#using-the-dynamic-media-viewers-extension}

Comme indiqué dans [Cas d’utilisation de l’intégration](#use-cases-for-the-integration), il est possible d’effectuer le suivi des visionneuses Dynamic Media avec la nouvelle intégration d’Experience Platform Tags dans Experience Manager Sites et à l’aide du code intégré.

### Suivi des visionneuses Dynamic Media dans Experience Manager Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Pour effectuer le suivi des visionneuses Dynamic Media dans Experience Manager Sites, toutes les étapes répertoriées sous la section [Configurer tous les composants d’intégration](#configuring-all-the-integration-pieces) doivent être réalisées. Plus précisément, vous devez créer la configuration IMS et la configuration du cloud Experience Platform Tags.

Une fois la configuration appropriée effectuée, toute visionneuse Dynamic Media que vous ajoutez à une page Sites, à l’aide d’un composant WCM pris en charge par Dynamic Media, effectue automatiquement le suivi des données vers Adobe Analytics ou Adobe Analytics for video, ou les deux.

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### Suivi des visionneuses Dynamic Media à l’aide du code intégré {#tracking-dynamic-media-viewers-using-embed-code}

Les clients qui n’utilisent pas Experience Manager Sites, ou n’incorporent pas les visionneuses Dynamic Media dans des pages web en dehors d’Experience Manager Sites, ou les deux, peuvent toujours utiliser l’intégration d’Experience Platform Tags.

Suivez les étapes de configuration des sections [Configurer Adobe Analytics](#configuring-adobe-analytics-for-the-integration) et [Configurer’Experience Platform Tags](#configuring-adobe-launch-for-the-integration). Toutefois, les étapes de configuration liées à Experience Manager ne sont pas nécessaires.

Une fois la configuration appropriée effectuée, vous pouvez ajouter la prise en charge d’Experience Platform Tags à une page web à l’aide d’une visionneuse Dynamic Media.

Consultez [Ajouter code intégré Experience Platform Tags](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-embed-code.html?lang=fr) pour en savoir plus sur l’utilisation du code intégré de la bibliothèque Experience Platform Tags.

<!-- To be reviewed and updated although this is found live in the Experience ManageraaCS version:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of Experience Manager Dynamic Media.
-->

**Suivi des visionneuses Dynamic Media à l’aide du code intégré :**

1. Préparez une page web sur laquelle vous voulez incorporer une visionneuse Dynamic Media.
1. Obtenez le code incorporé pour la bibliothèque Experience Platform Tags en vous connectant d’abord à Experience Platform Tags (consultez [Configurer Experience Platform Tags](#configuring-adobe-launch-for-the-integration)).
1. Sélectionnez **[!UICONTROL Propriété]**, puis l’onglet **[!UICONTROL Environnements]**.
1. Sélectionnez le niveau Environnement correspondant à l’environnement de la page web. Ensuite, dans la colonne **[!UICONTROL Installer]**, sélectionnez l’icône en forme de boîte.
1. Dans la boîte de dialogue **[!UICONTROL Instructions d’installation web]**, copiez le code intégré complet de la bibliothèque Experience Platform Tags, ainsi que les balises `<script/>` qui l’entourent.

## Guide de référence de l’extension Visionneuses Dynamic Media {#reference-guide-for-the-dynamic-media-viewers-extension}

### À propos de la configuration des visionneuses Dynamic Media {#about-the-dynamic-media-viewers-configuration}

L’extension Visionneuse Dynamic Media s’intègre automatiquement à la bibliothèque Experience Platform Tags si toutes les conditions suivantes sont réunies :

* L’objet global de la bibliothèque Experience Platform Tags (`_satellite`) est présent sur la page.
* La fonction d’extension Visionneuses Dynamic Media `_dmviewers_v001()` est définie sur `_satellite`.

* Le paramètre de visionneuse `config2=` n’est pas spécifié, ce qui signifie qu’elle n’utilise pas l’intégration Analytics héritée.

De plus, il existe une option pour désactiver explicitement l’intégration d’Experience Platform Tags dans la visionneuse en spécifiant un paramètre `launch=0` dans la configuration de la visionneuse. La valeur par défaut de ce paramètre est `1`.

### Configuration de l’extension Visionneuses Dynamic Media {#configuring-the-dynamic-media-viewers-extension}

La seule option de configuration de l’extension Visionneuses Dynamic Media est **[!UICONTROL Activer Adobe Media Analytics for Audio and Video]**.

Lorsque vous cochez (ou activez) cette option et si l’extension Adobe Media Analytics for Audio and Video est installée et configurée, les mesures de lecture vidéo sont envoyées à la solution Adobe Analytics for Audio and Video. La désactivation de cette option désactive le suivi vidéo.

Si vous activez cette option *sans* avoir installé Adobe Media Analytics for Audio and Video, elle n’aura aucun effet.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### À propos des éléments de données dans l’extension Visionneuses Dynamic Media {#about-data-elements-in-the-dynamic-media-viewers-extension}

Le seul type d’élément de données fourni par l’extension Visionneuses Dynamic Media est **[!UICONTROL Événement de visionneuse]** dans la liste déroulante **[!UICONTROL Type d’élément de données]**.

Lorsqu’il est sélectionné, l’éditeur d’éléments de données génère un formulaire avec deux champs :

* **[!UICONTROL Type de données d’événement de visionneuses DM]** : liste déroulante qui identifie tous les événements de visionneuse pris en charge par l’extension Visionneuses Dynamic Media qui comportent des arguments, ainsi qu’un élément **[!UICONTROL COMMON]** spécial. Un élément **[!UICONTROL COMMON]** représente une liste de paramètres d’événement communs à tous les types d’événements envoyés par les visionneuses.
* **[!UICONTROL Paramètre de suivi]** : argument de l’événement de visionneuse Dynamic Media sélectionné.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

Pour obtenir la liste des événements pris en charge par chaque type de visionneuse, reportez-vous au [Guide de référence des visionneuses Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html?lang=fr#viewers-aem-assets-dmc), accédez à la section spécifique à la visionneuse, puis sélectionnez la sous-section Prise en charge du suivi d’Adobe Analytics. À l’heure actuelle, le guide de référence des visionneuses Dynamic Media ne documente pas les arguments d’événement.

Examinons à présent le cycle de vie de l’*élément de données* Visionneuses Dynamic Media. La valeur de cet élément de données est renseignée après que l’événement de visionneuse Dynamic Media correspondant a lieu sur la page. Par exemple, supposons que l’élément de données pointe vers l’événement **[!UICONTROL LOAD]** et son argument « asset ». Dans de tels cas, la valeur de cet élément de données reçoit des données valides après la première exécution de l’événement **[!UICONTROL LOAD]** par la visionneuse. Si l’élément de données pointe vers l’événement **[!UICONTROL ZOOM]** et son argument « scale », la valeur de cet élément de données reste vide jusqu’à ce que la visionneuse envoie un événement **[!UICONTROL ZOOM]** pour la première fois.

De même, les valeurs des éléments de données sont automatiquement mises à jour lorsque la visionneuse envoie un événement correspondant sur la page. La mise à jour de la valeur se produit même si l’événement particulier n’est pas spécifié dans la configuration de la règle. Supposons, par exemple, que l’élément de données **[!UICONTROL ZoomScale]** soit défini pour le paramètre « scale » de l’événement ZOOM. Cependant, la seule règle présente dans la configuration de règle est déclenchée par l’événement **[!UICONTROL LOAD]**. La valeur de **[!UICONTROL ZoomScale]** reste mise à jour chaque fois qu’un utilisateur effectue un zoom dans la visionneuse.

Toute visionneuse Dynamic Media possède un identifiant unique sur la page web. L’élément de données effectue le suivi de la valeur elle-même et de la visionneuse qui a renseigné la valeur. Par exemple, supposons qu’il y ait plusieurs visionneuses sur la même page et un élément de données **[!UICONTROL AssetName]** qui pointe vers l’événement **[!UICONTROL LOAD]** et son argument « asset ». L’élément de données **[!UICONTROL AssetName]** conserve une collection de noms de ressources associés à chaque visionneuse chargée sur la page.

La valeur exacte renvoyée par l’élément de données dépend du contexte. Si l’élément de données est demandé dans une règle déclenchée par un événement de visionneuse Dynamic Media, la valeur de l’élément de données est renvoyée pour la visionneuse qui a lancé la règle. De plus, l’élément de données est demandé dans une règle qui a été déclenchée par un Événement provenant d’une autre extension d’Experience Platform Tags. À ce stade, la valeur de l’élément de données provient de la dernière visionneuse à mettre à jour cet élément de données.

**Examinons l’exemple de configuration suivant** :

* Une page web contenant deux visionneuses de zoom Dynamic Media : *visionneuse1* et *visionneuse2*.

* L’élément de données **[!UICONTROL ZoomScale]** pointe sur l’événement **[!UICONTROL ZOOM]** et son argument « scale ».
* Règle **[!UICONTROL TrackPan]** avec ce qui suit :

   * Utilise l’événement **[!UICONTROL PAN]** de la visionneuse Dynamic Media comme déclencheur.
   * Envoie la valeur de l’élément de données **[!UICONTROL ZoomScale]** à Adobe Analytics.

* Règle **[!UICONTROL TrackKey]** avec ce qui suit :

   * Utilise l’événement de pression de touche de l’extension Core d’Experience Platform Tags comme déclencheur.
   * Envoie la valeur de l’élément de données **[!UICONTROL ZoomScale]** à Adobe Analytics.

Supposons maintenant que l’utilisateur final charge la page web avec les deux visionneuses. Dans la *visionneuse1*, il effectue un zoom avant à une échelle de 50 % ; ensuite, dans la *visionneuse2*, il effectue un zoom avant à une échelle de 25 %. Dans la *visionneuse1*, il effectue un panoramique sur l’image et appuie sur une touche du clavier.

L’activité de l’utilisateur final génère les deux appels de suivi suivants vers Adobe Analytics :

* Le premier appel se produit, car la règle **[!UICONTROL TrackPan]** est déclenchée lorsque l’utilisateur effectue un panoramique dans la *visionneuse1*. Cet appel envoie 50 % en tant que valeur de l’élément de données **[!UICONTROL ZoomScale]** car l’élément de données sait que la règle est déclenchée par la *visionneuse1* et récupère la valeur d’échelle correspondante.
* Le second appel se produit, car la règle **[!UICONTROL TrackKey]** est déclenchée lorsque l’utilisateur appuie sur une touche du clavier. Cet appel envoie 25 % en tant que valeur de l’élément de données **[!UICONTROL ZoomScale]**, car la règle n’a pas été déclenchée par la visionneuse. L’élément de données renvoie donc la valeur la plus récente.

L’exemple de configuration ci-dessus affecte également la durée de vie de la valeur de l’élément de données. La valeur de l’élément de données géré par la visionneuse Dynamic Media est stockée dans le code de bibliothèque Experience Platform Tags, même après la suppression de la visionneuse de la page web. Cette fonctionnalité signifie que si une règle est déclenchée par une extension de lecteur autre que Dynamic Media et qu’elle fait référence à des élément de données, l’élément de données renvoie la dernière valeur connue. Même si la visionneuse n’est plus présente sur la page web.

Dans tous les cas, les valeurs des éléments de données pilotées par les visionneuses Dynamic Media ne sont pas stockées sur le stockage local ou sur le serveur ; elles sont conservées uniquement dans la bibliothèque Experience Platform Tags côté client. Les valeurs de cet élément de données disparaissent lors du rechargement de la page web.

En règle générale, l’éditeur d’éléments de données prend en charge la [sélection de la durée de stockage](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html?lang=fr#create-a-data-element). Toutefois, les éléments de données qui utilisent l’extension Visionneuses Dynamic Media ne prennent en charge que l’option de durée de stockage **[!UICONTROL Aucune]**. La définition d’une autre valeur est possible dans l’interface utilisateur, mais le comportement de l’élément de données n’est pas défini dans ce cas. L’extension gère elle-même la valeur de l’élément de données qui conserve la valeur de l’argument d’événement de visionneuse pendant tout le cycle de vie de la visionneuse.

### À propos des règles dans l’extension Visionneuses Dynamic Media {#about-rules-in-the-dynamic-media-viewers-extension}

Dans l’éditeur de règles, l’extension ajoute de nouvelles options de configuration pour l’éditeur d’événements. L’éditeur fournit également une option pour faire référence manuellement aux paramètres d’événement dans l’éditeur d’actions sous forme d’une option abrégée au lieu d’utiliser des éléments de données préconfigurés.

#### À propos de l’éditeur d’événements {#about-the-events-editor}

Dans l’éditeur d’événements, l’extension Visionneuses Dynamic Media ajoute un **[!UICONTROL type d’événement]** appelé **[!UICONTROL Événement de visionneuse]**.

Lorsqu’il est sélectionné, l’éditeur d’événements effectue le rendu du menu déroulant **[!UICONTROL Événements de visionneuse Dynamic Media]**, répertoriant tous les événements disponibles pris en charge par les visionneuses Dynamic Media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### À propos de l’éditeur d’actions {#about-the-actions-editor}

L’extension Visionneuses Dynamic Media vous permet d’utiliser les paramètres d’événement des visionneuses Dynamic Media pour mapper les variables Analytics dans l’éditeur Définir les variables de l’extension Adobe Analytics.

La méthode la plus simple consiste à effectuer le processus en deux étapes :

* Tout d’abord, définissez un ou plusieurs éléments de données, où chaque élément de données représente un paramètre d’un événement Visionneuse Dynamic Media.
* Enfin, dans l’éditeur Définir les variables de l’extension Adobe Analytics, sélectionnez l’icône du sélecteur d’**[!UICONTROL éléments de données]** (sous forme de trois disques empilés) pour ouvrir la boîte de dialogue Sélectionner un élément de données, puis sélectionnez un élément de données à partir de celle-ci.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

Il est toutefois possible d’utiliser une autre approche et d’éviter la création d’un élément de données. Vous pouvez référencer directement un argument à partir d’un événement de visionneuse Dynamic Media. Entrez le nom complet de l’argument d’événement dans le champ d’entrée **[!UICONTROL valeur]** de l’affectation de variable Analytics. Veillez à entourer votre entrée par des signes de pourcentage (%). Par exemple,

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Il existe une différence importante entre l’utilisation des éléments de données et la référence directe à l’argument d’événement. Pour l’élément de données, l’événement qui déclenche l’action Définir les variables importe peu. L’événement qui déclenche la règle peut ne pas être lié à la visionneuse dynamique. Par exemple, en sélectionnant la page web dans l’extension Core. Cependant, lorsque vous utilisez une référence directe à un argument, il est important de s’assurer que l’événement qui déclenche la règle correspond à l’argument d’événement auquel il fait référence.

Par exemple, la référence à `%event.detail.dm.LOAD.asset%` renvoie le nom de ressource correct si la règle est déclenchée par l’événement **[!UICONTROL LOAD]** de l’extension Visionneuse Dynamic Media. Cependant, elle renvoie une valeur vide pour tout autre événement.

Le tableau suivant répertorie les événements de visionneuse Dynamic Media et leurs arguments pris en charge :

<table>
 <tbody>
  <tr>
   <td>Nom de l’événement de visionneuse</td>
   <td>Référence de l’argument</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code><br /> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## Configuration de tous les composants d’intégration {#configuring-all-the-integration-pieces}

**AVANT DE COMMENCER**

Adobe vous recommande de passer en revue toute la documentation précédant cette section afin de comprendre l’intégration dans son ensemble.

Cette section décrit les étapes de configuration nécessaires pour intégrer des visionneuses Dynamic Media à Adobe Analytics et Adobe Analytics for Audio and Video. Bien que l’utilisation de l’extension Visionneuses Dynamic Media à d’autres fins dans Experience Platform Tags soit possible, ces scénarios ne sont pas abordés dans cette documentation.

Vous allez utiliser les produits Adobe suivants pour configurer votre intégration :

* Adobe Analytics : pour configurer les variables et les rapports de suivi.
* Experience Platform Tags : utilisé pour définir une propriété, une ou plusieurs règles, ainsi qu’un ou plusieurs éléments de données pour permettre le suivi des visionneuses.

En outre, si cette solution d’intégration est utilisée avec Experience Manager Sites, vous devez également effectuer la configuration suivante :

* [!DNL Adobe Developer Console] : l’intégration est créée pour les balises Experience Platform.
* Nœud d’auteur Experience Manager – Configuration IMS et configuration de cloud Experience Platform Tags.

Pour la configuration, assurez-vous d’avoir accès à une société dans Adobe Experience Cloud pour laquelle Adobe Analytics et Experience Platform Tags déjà activés.

## Configuration d’Adobe Analytics pour l’intégration {#configuring-adobe-analytics-for-the-integration}

Une fois Adobe Analytics configuré, les éléments suivants sont configurés pour l’intégration :

* Une suite de rapports est en place et sélectionnée.
* Les variables Analytics sont disponibles pour recevoir les données de suivi.
* Les rapports sont disponibles pour afficher les données collectées dans Adobe Analytics.

Voir aussi le [Guide de mise en œuvre d’Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr).

**Pour configurer Adobe Analytics en vue de l’intégration** :

1. Commencez par accéder à Adobe Analytics à partir de la [page d’accueil](https://experience.adobe.com/#/home) d’Experience Cloud. Dans la barre de menus, sélectionnez l’icône **[!UICONTROL Solutions]** (un tableau de trois points par trois) près du coin supérieur droit de la page, puis sélectionnez **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Sélectionnez maintenant une suite de rapports.

### Sélection d’une suite de rapports {#selecting-a-report-suite}

1. Près du coin supérieur droit de la page Adobe Analytics, à droite du champ **[!UICONTROL Rechercher des rapports]**, sélectionnez la suite de rapports appropriée dans la liste déroulante. Si plusieurs suites de rapports sont disponibles et que vous ne savez pas laquelle utiliser, contactez votre administrateur Adobe Analytics qui peut vous aider à sélectionner la suite de rapports adaptée.

   Dans la capture d’écran ci-dessous, un utilisateur a créé une suite de rapports nommée *DynamicMediaViewersExtensionDoc* et l’a sélectionnée dans la liste déroulante. Le nom de la suite de rapports n’est qu’un simple exemple. Le nom de la suite de rapports que vous sélectionnez en fin de compte dépend de vous.

   Si aucune suite de rapports n’est disponible, votre administrateur Adobe Analytics ou vous-même devez en créer une avant de poursuivre la configuration.

   Voir [Rapports et suites de rapports](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html?lang=fr) et [Création d’une suite de rapports](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite.html?lang=fr).

   Dans Adobe Analytics, les suites de rapports sont gérées sous **[!UICONTROL Admin]** > **[!UICONTROL Suites de rapports]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   Configurez maintenant les variables Adobe Analytics.

### Configuration des variables Adobe Analytics {#setting-up-adobe-analytics-variables}

1. Désignez une ou plusieurs variables Adobe Analytics à utiliser pour effectuer le suivi du comportement des visionneuses Dynamic Media sur la page web.

   Il est possible d’utiliser n’importe quel type de variable pris en charge par Adobe Analytics. La décision concernant le type de variable (tel que les [props] de trafic personnalisé et les [eVar] de conversion) doit être prise en fonction des besoins spécifiques à votre implémentation Analytics.

   Voir [Présentation de props et eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=fr#vars).

   Pour les besoins de cette documentation, seule une variable de trafic personnalisé (props) est utilisée car elle est disponible dans un rapport Analytics quelques minutes après qu’une action a lieu sur une page web.

   Pour activer une nouvelle variable de trafic personnalisé, dans Adobe Analytics, dans la barre d’outils, accédez à **[!UICONTROL Admin]** > **[!UICONTROL Suites de rapports]**.

1. Sur la page **[!UICONTROL Gestionnaire de suites de rapports]**, sélectionnez le rapport approprié, puis dans la barre d’outils, accédez à **[!UICONTROL Modifier les paramètres]** > **[!UICONTROL Trafic]** > **[!UICONTROL Variables de trafic]**.
1. Sélectionnez une variable qui n’est pas utilisée et attribuez-lui un nom explicite (**[!UICONTROL Ressource de visionneuse (prop 30)]**) et remplacez la zone de liste modifiable par « Activé » dans la colonne Activé.

   La capture d’écran suivante est un exemple de variable de trafic personnalisé (**[!UICONTROL prop30]**) pour le suivi d’un nom de ressource utilisé par la visionneuse :

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. Au bas de la liste des variables, sélectionnez **[!UICONTROL Enregistrer]**.

### Configuration d’un rapport {#setting-up-a-report}

1. En règle générale, la configuration d’un rapport dans Adobe Analytics dépend des besoins spécifiques au projet. La configuration détaillée des rapports dépasse donc le cadre de cette intégration.

   Il suffit toutefois de savoir que les rapports de trafic personnalisé sont automatiquement disponibles dans Adobe Analytics après avoir configuré les variables Trafic personnalisé dans [Configuration des variables Adobe Analytics](#setting-up-adobe-analytics-variables).

   Par exemple, le rapport pour la variable **[!UICONTROL Ressource de visionneuse (prop 30)]** est disponible dans le menu Rapports sous **[!UICONTROL Trafic personnalisé]** > **[!UICONTROL Trafic personnalisé 21-30]** > **[!UICONTROL Ressource de visionneuse (prop 30)]**.

   La consultation de ce rapport juste après la création de **[!UICONTROL Ressource de visionneuse (prop 30)]** ne montre aucune donnée ; c’est ce qui est attendu à ce stade de l’intégration.

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## Configuration d’Experience Platform Tags pour l’intégration {#configuring-adobe-launch-for-the-integration}

Une fois les balises Experience Platform configurées, les éléments suivants seront paramétrés pour l’intégration :

* Création d’une propriété pour conserver toutes vos configurations ensemble.
* Installation et configuration des extensions. Le code client de toutes les extensions installées dans la propriété est compilé dans une bibliothèque. Cette bibliothèque sera utilisée ultérieurement par la page web.
* Configuration des éléments de données et des règles. Cette configuration définit les données à capturer à partir des visionneuses Dynamic Media, le moment où déclencher la logique de suivi, ainsi que l’endroit où envoyer les données de la visionneuse dans Adobe Analytics.
* Publication de la bibliothèque.

**Pour configurer Experience Platform Tags en vue de l’intégration :**

1. Commencez par accéder à Experience Platform Tags à partir de la [page d’accueil](https://experience.adobe.com/#/home) d’Experience Cloud. Dans la barre de menus, sélectionnez l’icône **[!UICONTROL Solutions]** (un tableau de trois points par trois) près du coin supérieur droit de la page, puis sélectionnez **[!UICONTROL Balises]**.

   Vous pouvez également [ouvrir Experience Platform Tags directement](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Création d’une propriété dans Experience Platform Tags {#creating-a-property-in-adobe-launch}

Une propriété dans Experience Platform Tags est une configuration nommée qui conserve l’ensemble de vos paramètres. Une bibliothèque des paramètres de configuration est générée et publiée à différents niveaux d’environnement (développement, évaluation et production).

Consultez également [Création d’une propriété Tags](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/initial-configuration/configure-tags.html?lang=fr).

1. Dans Experience Platform Tags, sélectionnez **[!UICONTROL Nouvelle propriété]**.
1. Dans la boîte de dialogue **[!UICONTROL Créer une propriété]**, dans le champ **[!UICONTROL Nom]**, saisissez un nom descriptif, tel que le titre de votre site web. Par exemple, `DynamicMediaViewersProp.`
1. Dans le champ **[!UICONTROL Domaines]**, saisissez le domaine de votre site web.
1. Dans la liste déroulante **[!UICONTROL Options avancées]**, activez **[!UICONTROL Configurer pour le développement d’extensions (ne peut pas être modifié plus tard)]** au cas où l’extension que vous souhaitez utiliser (dans ce cas, *Visionneuses Dynamic Media*) n’est pas encore disponible.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   Sélectionnez la propriété que vous venez de créer, puis passez à *Installation et configuration des extensions*.

### Installation et configuration des extensions {#installing-and-setup-of-extensions}

Toutes les extensions disponibles dans Experience Platform Tags sont répertoriées sous **[!UICONTROL Extensions]** > **[!UICONTROL Catalogue]**.

Pour installer une extension, sélectionner **[!UICONTROL Installer]**. Si nécessaire, réalisez une configuration d’extension ponctuelle, puis sélectionnez **[!UICONTROL Enregistrer]**.

Le cas échéant, les extensions suivantes doivent être installées et configurées :

* (Obligatoire) *Service d’ID d’Experience Cloud* extension .

Aucune configuration supplémentaire n’est nécessaire, acceptez les valeurs proposées. Lorsque vous avez terminé, veillez à sélectionner **[!UICONTROL Enregistrer]**.

Consultez la section [Extension du service d’identités Adobe Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/id-service/overview.html?lang=fr).

* (Obligatoire) Extension *Adobe Analytics*

Pour configurer cette extension, vous devez connaître l’identifiant de suite de rapports figurant dans Adobe Analytics, sous **[!UICONTROL Admin]** > **[!UICONTROL Suite de rapports]**, sous l’en-tête de colonne **[!UICONTROL Identifiant de suite de rapports]**.

(À des fins de démonstration uniquement, l’identifiant de suite de rapports **[!UICONTROL DynamicMediaViewersExtensionDoc]** est utilisé dans les captures d’écran suivantes. Cet identifiant a été créé et utilisé dans [Sélection d’une suite de rapports](#selecting-a-report-suite) précédemment.)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

Sur la page Installer l’extension, saisissez l’identifiant de suite de rapports dans le champ **[!UICONTROL Suites de rapports de développement]**, le champ **[!UICONTROL Suites de rapports d’évaluation]** et le champ **[!UICONTROL Suites de rapport de production]**.

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Configurez l’élément suivant uniquement si vous prévoyez d’utiliser le suivi vidéo :*

Sur la page **[!UICONTROL Installer l’extension]**, développez **[!UICONTROL Général]**, puis spécifiez le serveur de suivi. Le serveur de suivi suit le modèle `<trackingNamespace>.sc.omtrdc.net`, où `<trackingNamespace>` représente les informations obtenues dans l’e-mail de mise en service.

Sélectionnez **[!UICONTROL Enregistrer]**.

Consultez la section [Extension d’Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/analytics/overview.html?lang=fr).

* (obligatoire uniquement si le suivi vidéo est nécessaire) extension *Adobe Media Analytics pour l’audio et la vidéo*

Renseignez le champ Serveur de suivi. Le serveur de suivi pour l’extension *Adobe Media Analytics for Audio and Video* est différent du serveur de suivi utilisé pour Adobe Analytics. Il suit le modèle `<trackingNamespace>.hb.omtrdc.net`, où `<trackingNamespace>` représente les informations provenant de l’e-mail de mise en service.

Tous les autres champs sont facultatifs.

Voir [Extension Adobe Media Analytics for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics/overview.html?lang=fr).

* (Obligatoire) Extension *Visionneuses Dynamic Media*

Sélectionnez **[!UICONTROL Activer Adobe Analytics for Video]** pour activer le suivi Video Heartbeat.

Au moment de la rédaction de cet article, l’extension *Visionneuses Dynamic Media* n’est disponible que si la propriété Experience Platform Tags a été créée pour le développement.

Consultez [Création d’une propriété dans Experience Platform Tags](#creating-a-property-in-adobe-launch).

Une fois les extensions installées et configurées, au minimum, les cinq extensions suivantes (quatre si vous n’effectuez pas le suivi vidéo) sont répertoriées dans la zone Extensions > Installées .

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Configuration des éléments de données et des règles {#setting-up-data-elements-and-rules}

Dans Experience Platform Tags, créez les éléments de données et les règles nécessaires au suivi des visionneuses Dynamic Media.

Consultez [Fonctionnement du suivi des données et des événements dans l’intégration](#how-data-and-event-tracking-works-in-the-integration) pour un aperçu du suivi avec Experience Platform Tags.

Consultez [Exemple de configuration](#sample-configuration) pour un exemple de configuration dans Experience Platform Tags qui montre comment effectuer le suivi d’un nom de ressource au moment du chargement de la visionneuse.

Voir [Configuration de l’extension Visionneuses Dynamic Media](#configuring-the-dynamic-media-viewers-extension) pour en savoir plus sur les fonctionnalités de l’extension.

### Publication d’une bibliothèque {#publishing-a-library}

Pour apporter des modifications à la configuration d’Experience Platform Tags (y compris la configuration de la propriété, des extensions, des règles et des éléments de données), vous devez *publier* ces modifications. La publication dans Experience Platform Tags est effectuée à partir de l’onglet Publication sous la configuration des propriétés.

Experience Platform Tags peut comporter plusieurs environnements de développement, un environnement d’évaluation et un environnement de production. Par défaut, la configuration cloud d’Experience Platform Tags dans Experience Manager pointe le nœud d’auteur Experience Manager vers l’environnement d’évaluation de Platform Tags. Le nœud de publication d’Experience Manager pointe vers l’environnement de production d’Experience Platform Tags. Cette disposition signifie qu’avec les paramètres par défaut d’Experience Manager, il est nécessaire de publier la bibliothèque Experience Platform Tags dans l’environnement d’évaluation. Cela vous permet de l’utiliser dans l’auteur Experience Manager. Vous pouvez ensuite le publier dans l’environnement de production afin de pouvoir l’utiliser dans la publication Experience Manager.

Consultez [Environnements](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=fr) pour plus d’informations sur les environnements Experience Platform Tags.

La publication d’une bibliothèque implique les deux étapes suivantes :

* Ajout et création d’une bibliothèque en incluant toutes les modifications nécessaires (nouvelles et mises à jour) dans la bibliothèque.
* Déplacement de la bibliothèque vers les différents niveaux d’environnement (du développement à l’évaluation et à la production).

#### Ajouter et créer une bibliothèque {#adding-and-building-a-new-library}

1. La première fois que vous ouvrez l’onglet Publication dans Experience Platform Tags, la liste des bibliothèques est vide.

   Dans la colonne de gauche, sélectionnez **[!UICONTROL Ajouter une nouvelle bibliothèque]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. Sur la page Créer une bibliothèque, dans le champ **[!UICONTROL Nom]**, saisissez un nom descriptif pour la nouvelle bibliothèque. Par exemple,

   *DynamicMediaViewersLib*

   Dans la liste déroulante Environnement, sélectionnez le niveau Environment. Au départ, seul le niveau Développement est disponible pour la sélection. Près du coin inférieur gauche de la page, sélectionnez **[!UICONTROL Ajouter toutes les ressources modifiées]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Dans le coin supérieur droit de la page, sélectionnez **[!UICONTROL Enregistrer et créer pour développement]**.

   En quelques minutes, la bibliothèque est créée et prête à être utilisée.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >La prochaine fois que vous apporterez des modifications à votre configuration Experience Platform Tags, accédez à l’onglet **[!UICONTROL Publication]** sous la configuration **[!UICONTROL Propriété]**, puis sélectionnez votre bibliothèque créée précédemment.
   >
   >
   >Dans l’écran de publication de la bibliothèque, sélectionnez **[!UICONTROL Ajouter toutes les ressources modifiées]**, puis **[!UICONTROL Enregistrer et créer pour développement]**.

#### Déplacement d’une bibliothèque à travers les niveaux d’environnement {#moving-a-library-up-through-environment-levels}

1. Une fois une bibliothèque ajoutée, elle se trouve dans l’environnement de développement. Pour la déplacer au niveau de l’environnement d’évaluation (qui correspond à la colonne Envoyé), dans le menu déroulant de la bibliothèque, sélectionnez **[!UICONTROL Envoyer pour approbation]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. Dans la boîte de dialogue de confirmation, sélectionnez **[!UICONTROL Envoyer]**.

   Une fois la bibliothèque déplacée vers la colonne Envoyé, dans le menu déroulant de la bibliothèque, sélectionnez **[!UICONTROL Créer pour l’évaluation]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Pour déplacer la bibliothèque de l’environnement d’évaluation vers l’environnement de production (c’est-à-dire dans la colonne Publié), suivez un processus similaire.

   Tout d’abord, dans le menu déroulant, sélectionnez **[!UICONTROL Approuver pour publication]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. Dans le menu déroulant, sélectionnez **[!UICONTROL Créer et publier en production]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Consultez [Publication](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=fr) pour plus d’informations sur le processus de publication dans Experience Platform Tags.

## Configuration d’Adobe Experience Manager pour l’intégration {#configuring-adobe-experience-manager-for-the-integration}

Conditions préalables :

* Experience Manager exécute les instances d’auteur comme de publication.
* Le nœud d’auteur d’Experience Manager est configuré dans Dynamic Media en mode d’exécution Scene7 (dynamicmedia_s7).
* Les composants WCM Dynamic Media sont activés dans Experience Manager Sites.

La configuration d’Experience Manager comprend les deux importantes étapes suivantes :

* Configuration du système IMS Experience Manager.
* Configuration du cloud Experience Platform Tags.

### Configuration d’IMS Experience Manager {#configuring-aem-ims}

1. Dans l’auteur Experience Manager, sélectionnez l’icône **[!UICONTROL Outils]** (en forme de marteau), puis **[!UICONTROL Sécurité]** > **[!UICONTROL Configurations d’Adobe IMS]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. Sur la page Configuration d’Adobe IMC, près du coin supérieur gauche, sélectionnez **[!UICONTROL Créer]**.
1. Sur la page **[!UICONTROL Configuration du compte technique Adobe IMS]**, dans la liste déroulante **[!UICONTROL Solution cloud]**, sélectionnez **[!UICONTROL Experience Platform Tags]**.
1. Activez **[!UICONTROL Créer un certificat]**, puis, dans le champ de texte, entrez une valeur pertinente pour votre certificat. Par exemple, *AdobeLaunchIMSCert*. Sélectionnez **[!UICONTROL Créer un certificat]**.

   Le message d’informations suivant s’affiche :

   *Afin de récupérer un jeton d’accès valide, la nouvelle clé publique du certificat doit être ajoutée au compte technique sur l’Adobe Developer Console.*

   Pour fermer la boîte de dialogue Info, sélectionnez **[!UICONTROL OK]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Pour télécharger un fichier de clé publique (&#42;.crt) sur votre système local, sélectionnez **[!UICONTROL Télécharger la clé publique]**.

   >[!NOTE]
   >
   >À ce stade, ***laissez ouverte*** la page **[!UICONTROL Configuration du compte technique Adobe IMS]** ; ***ne fermez pas*** la page et ***ne sélectionnez pas*** Suivant. Vous y reviendrez plus tard.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. Dans un nouvel onglet du navigateur, accédez à l’[[!DNL Adobe Developer Console]](https://developer.adobe.com/console/integrations).

1. Sur la page **[!UICONTROL intégrations de l’Adobe Developer Console]**, près du coin supérieur droit, sélectionnez **[!UICONTROL Nouvelle intégration]**.
1. Dans la boîte de dialogue **[!UICONTROL Créer une intégration]**, vérifiez que le bouton radio **[!UICONTROL Accès à une API]** est sélectionné, puis sélectionnez **[!UICONTROL Continuer]**.

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. Sur la deuxième page **[!UICONTROL Créer une intégration]**, activez le bouton radio **[!UICONTROL API Experience Platform Tags]**. Dans le coin inférieur droit de la page, sélectionnez **[!UICONTROL Continuer]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. Sur la troisième page **[!UICONTROL Créer une intégration]**, procédez comme suit :

   * Dans le champ **[!UICONTROL Nom]**, saisissez un nom explicite. Par exemple, *DynamicMediaViewersIO*.

   * Dans le champ **[!UICONTROL Description]**, saisissez la description de l’intégration.

   * Dans la zone **[!UICONTROL Certificats de clé publique]**, chargez votre fichier de clé publique (&#42;.crt) que vous avez précédemment téléchargé au cours de ces étapes.

   * Sous l’en-tête **[!UICONTROL Sélectionner un rôle pour l’API Experience Platform Tags]**, sélectionnez **[!UICONTROL Admin]**.

   * Sous l’en-tête **[!UICONTROL Sélectionner un ou plusieurs profils de produit pour l’API Experience Platform Tags]**, sélectionnez le profil de produit appelé **[!UICONTROL Tags – &lt;nom_de_votre_société>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Sélectionnez **[!UICONTROL Créer une intégration]**.
1. Sur la page **[!UICONTROL Intégration créée]**, sélectionnez **[!UICONTROL Continuer vers les informations concernant l’intégration]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. Une page Informations concernant l’intégration s’affiche, **** comme suit :

   >[!NOTE]
   >
   >***Laissez ouverte cette page Informations concernant l’intégration***. Vous aurez besoin de plusieurs informations figurant dans les onglets **[!UICONTROL Aperçu]** et **[!UICONTROL JWT]** dans un instant.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   Page Informations concernant l’intégration.

1. Revenez à la page **[!UICONTROL Configuration du compte technique Adobe IMS]** que vous avez laissée ouverte précédemment. Dans le coin supérieur droit de la page, sélectionnez **[!UICONTROL Suivant]** pour ouvrir la page **[!UICONTROL Compte]** dans la fenêtre **[!UICONTROL Configuration du compte technique Adobe IMS]**.

   (Si vous avez déjà fermé la page, revenez à l’auteur Experience Manager puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Configurations d’Adobe IMS]**. Sélectionnez **[!UICONTROL Créer]**. Dans la liste déroulante **[!UICONTROL Solution cloud]**, sélectionnez **[!UICONTROL Experience Platform Tags]**. Dans la liste déroulante **[!UICONTROL Certificat]**, sélectionnez le nom du certificat créé précédemment.)

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   Configuration du compte technique Adobe IMS – Page Certificat.

1. La page **[!UICONTROL Compte]** comporte cinq champs qui vous obligent à renseigner les informations de la page Informations concernant l’intégration de l’étape précédente.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   Configuration du compte technique Adobe IMS – Page Compte.

1. Sur la page **[!UICONTROL Compte]**, renseignez les champs suivants :

   * **[!UICONTROL Titre]** : entrez un titre de compte descriptif.
   * **[!UICONTROL Serveur d’autorisation]** : revenez à la page Informations concernant l’intégration que vous avez ouverte précédemment. Sélectionnez l’onglet **[!UICONTROL JWT]**. Copiez le nom du serveur (sans le chemin d’accès), comme indiqué ci-dessous.

   Revenez à la page **[!UICONTROL Compte]**, puis collez le nom dans le champ correspondant.
Par exemple : `https://ims-na1.adobelogin.com/`
(ce nom de serveur est seulement un exemple)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   Page Informations concernant l’intégration – Onglet JWT

1. **[!UICONTROL Clé API]** : revenez à la page Informations concernant l’intégration. Sélectionnez l’onglet **[!UICONTROL Aperçu]**, puis **[!UICONTROL Copier]** à droite du champ **[!UICONTROL Clé API (ID client)]**.

   Revenez à la page **[!UICONTROL Compte]**, puis collez la clé dans le champ correspondant.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   Page Informations concernant l’intégration.

1. **[!UICONTROL Secret client]** : revenez à la page Informations concernant l’intégration. Dans l’onglet **[!UICONTROL Aperçu]**, sélectionnez **[!UICONTROL Récupérer le secret client]**. À droite du champ **[!UICONTROL Secret client]**, sélectionnez **[!UICONTROL Copier]**.

   Revenez à la page **[!UICONTROL Compte]**, puis collez la clé dans le champ correspondant.

1. **[!UICONTROL Charge utile]** : revenez à la page Informations concernant l’intégration. Dans l’onglet **[!UICONTROL JWT]**, dans le champ Charge utile JWT, copiez le code d’objet JSON entier.

   Revenez à la page **[!UICONTROL Compte]**, puis collez le code dans le champ correspondant.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   Page Informations concernant l’intégration – Onglet JWT

   La page Compte, avec tous les champs remplis, se présente comme suit :

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Dans le coin supérieur droit de la page **[!UICONTROL Compte]**, sélectionnez **[!UICONTROL Créer]**.

   Une fois Experience Manager IMS configuré, vous disposez désormais d’un nouveau compte IMS répertorié sous **[!UICONTROL Configurations d’Adobe IMS]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Configuration d’Experience Platform Tags Cloud pour l’intégration {#configuring-adobe-launch-cloud-for-the-integration}

1. Dans l’auteur Experience Manager, près du coin supérieur gauche, sélectionnez l’icône **[!UICONTROL Outils]** (en forme de marteau), puis accédez à **[!UICONTROL Services cloud]** > **[!UICONTROL Configurations de balises Experience Platform]**.

   ![26/07/2019_12-10-38](assets/2019-07-26_12-10-38.png)

1. Sur la page **[!UICONTROL Configurations d’Experience Platform Tags]**, dans le panneau de gauche, sélectionnez un site Experience Manager auquel appliquer la configuration d’Experience Platform Tags.

   À titre d’exemple uniquement, le site **`We.Retail`** est sélectionné dans la capture d’écran ci-dessous.

   ![26/07/2019_12-20-06](assets/2019-07-26_12-20-06.png)

1. Dans le coin supérieur gauche de la page, sélectionnez **[!UICONTROL Créer]**.
1. Sur la page **[!UICONTROL Général]** (page 1/3) de la fenêtre **[!UICONTROL Créer une configuration Experience Platform Tags]**, renseignez les champs suivants :

   * **[!UICONTROL Titre]** : entrez un titre de configuration descriptif. Par exemple, `We.Retail Tags cloud configuration`.

   * **[!UICONTROL Configuration de l’IMS Adobe associée]** : sélectionnez la configuration IMS que vous avez créée précédemment dans [Configurer l’IMS Experience Manager](#configuring-aem-ims).

   * **[!UICONTROL Société]** : dans la liste déroulante **[!UICONTROL Société]**, sélectionnez votre société Experience Cloud. La liste est renseignée automatiquement.

   * **[!UICONTROL Propriété]** : dans la liste déroulante Propriété, sélectionnez la propriété Experience Platform Tags que vous avez créée précédemment. La liste est renseignée automatiquement.

   Après avoir rempli tous les champs, la page **[!UICONTROL Général]** se présente comme suit :

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Près du coin supérieur gauche, sélectionnez **[!UICONTROL Suivant]**.
1. Sur la page **[!UICONTROL Évaluation]** (page 2/3) de la fenêtre **[!UICONTROL Créer une configuration Experience Platform Tags]**, renseignez les champs suivants :

   Dans le champ **[!UICONTROL URI de bibliothèque]** (Uniform Resource Identifier), vérifiez l’emplacement de la version d’évaluation de votre bibliothèque Experience Platform Tags. Experience Manager remplit ce champ automatiquement.

   À titre d’exemple uniquement, cette étape utilise des bibliothèques de balises Experience Platform déployées sur le réseau de diffusion de contenu Adobe.

   >[!NOTE]
   >
   >Vérifiez que l’URI (Uniform Resource Identifier) de bibliothèque auto-renseigné n’est pas mal formé. Si nécessaire, corrigez-le de sorte qu’il soit relatif au protocole. C’est-à-dire qu’il commence par une double barre oblique.
   >
   >
   >Par exemple : `//assets.adobetm.com/launch-xxxx`.

   Votre page **[!UICONTROL Évaluation]** doit ressembler à ce qui suit. Les options **[!UICONTROL Archiver]** et **[!UICONTROL Charger la bibliothèque de manière asynchrone]** ne sont ***pas*** définies :

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Près du coin supérieur droit, sélectionnez **[!UICONTROL Suivant]**.
1. Sur la page **[!UICONTROL Production]** (page 3/3) de la fenêtre **[!UICONTROL Créer une configuration Experience Platform Tags]**, si nécessaire, corrigez l’URI de production auto-renseigné de la même manière que sur la page **[!UICONTROL Évaluation]** précédente.
1. Près du coin supérieur droit, sélectionnez **[!UICONTROL Créer]**.

   Votre nouvelle configuration du cloud Experience Platform Tags est maintenant créée et répertoriée à côté de votre site web :

1. Sélectionnez votre nouvelle configuration du cloud Experience Platform Tags (une coche apparaît à gauche du titre de la configuration lorsqu’elle est sélectionnée). Dans la barre d’outils, sélectionnez **[!UICONTROL Publier]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

À l’heure actuelle, l’auteur Experience Manager ne prend pas en charge l’intégration des visionneuses Dynamic Media avec Experience Platform Tags.

Elle est toutefois prise en charge dans le nœud de publication Experience Manager. En utilisant les paramètres par défaut de la configuration cloud d’Experience Platform Tags, le nœud de publication Experience Manager utilise l’environnement d’exploitation d’Experience Platform Tags. Par conséquent, il est nécessaire de transmettre les mises à jour de la bibliothèque Experience Platform Tags de l’environnement de développement vers celui de production chaque fois pendant le test.

Il est possible de contourner cette limitation. Spécifiez l’URL de développement ou d’évaluation de la bibliothèque Platform Tags dans la configuration cloud d’Experience Platform Tags pour la publication Experience Manager ci-dessus. Ainsi, le nœud de publication d’Experience Manager utilise la version de développement ou d’évaluation de la bibliothèque Experience Platform Tags.

Consultez la section [Intégration d’Experience Manager aux balises Experience Platform par le biais d’ [!DNL Adobe Developer Console]](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=fr) pour plus d’informations sur la configuration cloud des balises Experience Platform.
