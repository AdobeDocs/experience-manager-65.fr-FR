---
title: Recherche d’images et de ressources numériques dans [!DNL Adobe Experience Manager].
description: Learn how to find the required assets in [!DNL Adobe Experience Manager] by using Filters panel, and how to use the assets that show up in search.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 7b3282f086ba1f0a2f1e5430b90a6742ddf946d6
workflow-type: tm+mt
source-wordcount: '5955'
ht-degree: 52%

---


# Search assets in [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] fournit des méthodes robustes de découverte de ressources qui vous aident à atteindre une vitesse de contenu plus élevée. Vos équipes réduisent le temps de mise sur le marché grâce à une expérience de recherche intelligente et transparente, grâce à des fonctionnalités prêtes à l&#39;emploi et à des méthodes personnalisées. La recherche de ressources est essentielle pour l’utilisation d’un système de gestion des ressources numériques, que ce soit pour une utilisation plus poussée par les créatifs, pour une gestion robuste des ressources par les utilisateurs et spécialistes marketing ou pour l’administration par les administrateurs DAM. Simple, advanced, and custom searches that you can perform via [!DNL Assets] user interface or other apps and surfaces help fulfill these use cases.

[!DNL Experience Manager Assets] prend en charge les cas d’utilisation suivants dont cet article décrit l’utilisation, les concepts, les configurations, les limitations et le dépannage.

| Recherche de ressources | Configuration et administration | Utilisation des résultats de recherche |
|---|---|---|
| [Recherches de base](#searchbasics) | [Index de recherche](#searchindex) | [Tri des résultats](#sort) |
| [Présentation de l’interface utilisateur de recherche](#searchui) | [Recherche visuelle ou par analogie](#configvisualsearch) | [Vérification des propriétés et des métadonnées d’une ressource](#checkinfo) |
| [Suggestions de recherche](#searchsuggestions) | [Métadonnées obligatoires](#mandatorymetadata) | [Téléchargement](#download) |
| [Présentation des résultats de recherche et du comportement](#searchbehavior) | [Modification des facettes de recherche](#searchfacets) | [Mises à jour des métadonnées en masse](#metadataupdates) |
| [Classement et amplification des recherches](#searchrank) | [Extraction de texte](#extracttextupload) | [Collections dynamiques](#collections) |
| [Recherche avancée : filtrage et portée de la recherche](#scope) | [Prédicats personnalisés](#custompredicates) | [Présentation des résultats inattendus et dépannage](#troubleshoot-unexpected-search-results-and-issues) |
| [Recherche à partir d’autres solutions et applications](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[Application de bureau Experience Manager](#desktopapp)</li><li>[Images Adobe Stock](#adobestock)</li><li>[Ressources Dynamic Media](#dynamicmedia)</li></ul> |  |  |
| [Sélecteur de ressources](#assetpicker) |  |  |
| [Limites](#limitations) et [conseils](#tips) |  |  |
| [Exemples illustrés](#samples) |  |  |

Search for assets using the Omnisearch field at the top of the [!DNL Experience Manager] web interface. Go to **[!UICONTROL Assets]** > **[!UICONTROL Files]** in [!DNL Experience Manager], click search in top bar, enter search keyword, and press return. Vous pouvez également utiliser le raccourci clavier / (barre oblique) pour ouvrir le champ Omnisearch. `Location:Assets` est présélectionné afin de limiter les recherches aux ressources de la gestion des ressources numériques. [!DNL Experience Manager] fournit des suggestions en tant que début en saisissant un mot-clé de recherche.

Utilisez le panneau **[!UICONTROL Filtres]** pour restreindre votre recherche en filtrant les résultats de recherche en fonction des différentes options (prédicats), telles que le type de fichier, la taille de fichier, la date de dernière modification, l’état du fichier, les données d’informations et la licence Adobe Stock. Vos administrateurs peuvent personnaliser le panneau Filtres et ajouter ou supprimer des prédicats de recherche à l’aide de facettes de recherche. Le filtre Type [!UICONTROL de] fichier du panneau [!UICONTROL Filtres] comporte des cases à cocher à états mixtes. Par conséquent, à moins que vous ne sélectionniez tous les prédicats imbriqués (ou formats), les cases à cocher de premier niveau sont partiellement cochées.

[!DNL Experience Manager]La fonctionnalité de recherche prend en charge la recherche de collections et la recherche de ressources dans une collection. Voir [Recherche de collections](/help/assets/managing-collections-touch-ui.md).

## Présentation de l’interface de recherche {#searchui}

Familiarisez-vous avec l’interface de recherche et les actions disponibles.

![Comprendre l&#39;interface des résultats de la recherche des ressources du Experience Manager](assets/aem_search_results.png)

*Figure : Comprendre l&#39;interface des résultats de[!DNL Experience Manager Assets]la recherche.*

**R.** Enregistrez la recherche en tant que collection dynamique. **B.** Filtres ou prédicats pour limiter les résultats de la recherche. **C.** Affiche les fichiers, les dossiers ou les deux. **D.** Cliquer sur Filtres pour ouvrir ou fermer le rail de gauche. **E.** L’emplacement de recherche est la gestion des ressources numériques. **F.** Champ Omnisearch avec mot-clé de recherche fourni par l&#39;utilisateur. **G.** Sélectionnez les résultats de recherche chargés. **H.** Nombre de résultats de recherche affichés sur l&#39;ensemble des résultats de recherche. **I.** Fermer la recherche **J.** Basculer entre la vue de carte et la vue de liste.

### Facettes de recherche dynamique {#dynamicfacets}

Vous pouvez découvrir plus rapidement les ressources de votre choix à partir de la page des résultats de recherche en utilisant le nombre de résultats de recherche attendus mis à jour dynamiquement dans les facettes de recherche. Le nombre prévu de ressources est mis à jour avant même d’appliquer le filtre de recherche. L’affichage du nombre prévu par rapport au filtre vous aide à parcourir rapidement et efficacement les résultats de la recherche. For more info, see [Search assets in Experience Manager](search-assets.md).

![Affichage du nombre approximatif de ressources sans filtrer les résultats de la recherche dans les facettes de recherche.](assets/asset_search_results_in_facets_filters.png)

*Figure : Affichez le nombre approximatif de fichiers sans filtrer les résultats de la recherche dans les facettes de recherche.*

## Présentation des résultats de recherche et du comportement {#searchbehavior}

### Termes et résultats de recherche de base {#searchbasics}

Vous pouvez exécuter des recherches de mots-clés à partir du champ Omni-recherche. La recherche de mots-clés n’est pas sensible à la casse et est une recherche de texte intégral (dans les champs de métadonnées les plus utilisés). Si plusieurs mots-clés sont recherchés, l’opérateur par défaut entre les mots-clés correspond à la recherche par défaut et c’est `AND` `OR` lorsque les ressources sont balisées intelligemment.

Les résultats sont triés par pertinence, en commençant par les correspondances les plus proches. Pour plusieurs mots-clés, les ressources qui contiennent les deux termes dans leurs métadonnées génèrent des résultats plus pertinents. Dans les métadonnées, les mots-clés qui apparaissent sous forme de balises intelligentes sont classés plus haut que les mots-clés qui apparaissent dans d’autres champs de métadonnées. [!DNL Experience Manager] permet de donner plus de poids à un terme de recherche particulier. Also, it is possible to [boost the rank](#searchrank) of a few targeted assets for specific search terms.

Pour rechercher rapidement les ressources appropriées, l’interface riche fournit des mécanismes de filtrage, de tri et de sélection. Vous pouvez filtrer les résultats selon plusieurs critères et afficher le nombre de ressources recherchées pour différents filtres. Vous pouvez également réexécuter la recherche en modifiant la requête dans le champ Omni-recherche. Lorsque vous modifiez les termes ou filtres de recherche, les autres filtres restent appliqués pour préserver le contexte de la recherche.

Lorsque les résultats sont de nombreux actifs, [!DNL Experience Manager] affiche les 100 premiers dans la vue de cartes et les 200 premiers dans la vue de listes. Au fur et à mesure que les utilisateurs font défiler le contenu, d’autres ressources sont chargées. Il s&#39;agit d&#39;améliorer les performances. Regardez une démonstration vidéo du [nombre de ressources affichées](https://www.youtube.com/watch?v=LcrGPDLDf4o).

Il arrive que des ressources inattendues apparaissent dans les résultats de la recherche. Pour plus d’informations, voir [Résultats inattendus](#troubleshoot-unexpected-search-results-and-issues).

[!DNL Experience Manager] peut effectuer des recherches dans de nombreux formats de fichiers et les filtres de recherche peuvent être personnalisés en fonction des besoins de votre entreprise. Contactez votre administrateur pour connaître les options de recherche disponibles pour votre référentiel DAM et les restrictions de votre compte.

### Résultats avec et sans balises actives améliorées {#withsmarttags}

By default, [!DNL Experience Manager] search combines the search terms with an AND clause. Par exemple, pensez à rechercher les mots-clés femme en cours d’exécution. Par défaut, seuls les fichiers contenant à la fois des mots-clés féminins et en cours d’exécution dans les métadonnées apparaissent dans les résultats de recherche. Le même comportement est conservé lorsque des caractères spéciaux (points, traits de soulignement ou tirets) sont utilisés avec les mots-clés. Les requêtes de recherche suivantes renvoient les mêmes résultats :

* `woman running`
* `woman.running`
* `woman-running`

Cependant, la requête `woman -running` renvoie des fichiers sans `running` les métadonnées.
Using smart tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using smart tags also appear in such a search query. Les résultats de la recherche sont donc une combinaison de

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Actifs balisés avec l’un des mots-clés (comportement des balises actives).

### Suggestions de recherche en cours de frappe {#searchsuggestions}

When you start typing keywords, [!DNL Experience Manager] suggests the possible search keywords or phrases. Les suggestions sont basées sur les métadonnées des ressources existantes. [!DNL Experience Manager] indexe tous les champs de métadonnées pour faciliter la recherche. Pour fournir des suggestions de recherche, le système utilise les valeurs des quelques champs de métadonnées suivants. Pour fournir des suggestions de recherche, pensez à renseigner les champs suivants avec les mots-clés appropriés :

* Balises de ressources. (mappage avec `jcr:content/metadata/cq:tags`)
* Titre de la ressource. (mappage avec `jcr:content/metadata/dc:title`)
* Description de la ressource. (mappage avec `jcr:content/metadata/dc:description`)
* Titre dans le référentiel JCR. La valeur peut être mappée au titre de la ressource. (mappage avec `jcr:content/jcr:title`)
* Description dans le référentiel JCR. La valeur peut être mappée à la description de la ressource. (mappage avec `jcr:content/jcr:description`)

Pour recevoir des suggestions pour plusieurs mots-clés de recherche, continuez à taper tous les mots-clés sans sélectionner aucune suggestion pour un seul mot-clé.

![Tapez plusieurs mots-clés pour les suggestions de vue qui les tiennent toutes](assets/search_suggestionsmanykeywords.gif)

*Figure : Tapez plusieurs mots-clés pour les suggestions de vue qui conviennent à tous.*

### Classement et amplification des recherches {#searchrank}

Les résultats de recherche qui correspondent à tous les termes de recherche dans les champs de métadonnées s’affichent en premier, suivis des résultats de recherche correspondant à l’un des termes de recherche des balises dynamiques. Dans l’exemple ci-dessus, l’ordre approximatif de l’affichage des résultats de recherche est le suivant :

1. Correspondances de `woman running` dans les différents champs de métadonnées.
1. Correspondances de `woman running` dans les balises intelligentes.
1. Correspondances de `woman` ou de `running` dans les balises intelligentes.

Vous pouvez améliorer la pertinence des mots-clés pour des ressources données afin d’améliorer les résultats de recherches basées sur ces mots-clés. En d’autres termes, les images pour lesquelles vous faites la promotion de mots-clés spécifiques apparaissent en haut des résultats lorsque vous lancez une recherche basée sur ces mots-clés.

1. From the [!DNL Assets] user interface, open the properties page for the asset. Click **[!UICONTROL Advanced]** and click **[!UICONTROL Add]** under **[!UICONTROL Elevate for search keywords]**.
1. In the **[!UICONTROL Search Promote]** box, specify a keyword for which you want to boost the search for the image and then click **[!UICONTROL Add]**. Vous pouvez indiquer plusieurs mots-clés de la même manière.
1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**. La ressource pour laquelle vous avez promu ce mot-clé apparaît en tête des résultats de recherche.

Vous pouvez l’utiliser à votre avantage en améliorant le classement de certaines ressources dans les résultats de recherche du mot-clé ciblé. Voir la vidéo d’exemple ci-dessous. For detailed info, see [search in Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/search-and-discovery/search.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Découvrez comment les résultats de recherche sont classés et comment le classement peut être influencé.*

## Recherche avancée {#scope}

[!DNL Experience Manager] fournit diverses méthodes, telles que des filtres qui s’appliquent aux ressources recherchées, pour vous aider à localiser plus rapidement les ressources qu’il vous faut. Quelques méthodes fréquemment utilisées sont décrites ci-dessous. Vous trouverez ci-dessous plusieurs [exemples illustrés](#samples).

**Recherche de fichiers ou de dossiers** : dans les résultats de recherche, reportez-vous aux fichiers, aux dossiers ou aux deux. Dans le panneau **[!UICONTROL Filtres]**, vous pouvez sélectionner l’option appropriée. Voir [Interface de recherche](#searchui).

**Recherche de ressources dans un dossier** : vous pouvez limiter la recherche à un dossier spécifique. Dans le panneau **[!UICONTROL Filtres]**, ajoutez le chemin d’un dossier. Vous ne pouvez sélectionner qu’un dossier à la fois.

![Limitation des résultats de recherche à un dossier en ajoutant un chemin de dossier dans le panneau Filtres](assets/search_folder_select.gif)

*Figure : Limitez les résultats de la recherche à un dossier en ajoutant un chemin de dossier dans le panneau Filtres.*

### Rechercher des images similaires {#visualsearch}

Pour rechercher des images visuellement similaires à une image sélectionnée par l’utilisateur, cliquez sur l’option **[!UICONTROL Rechercher des images similaires]** dans le mode Carte d’une image ou dans la barre d’outils. [!DNL Experience Manager] affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. Voir [Configuration de la recherche par analogie](#configvisualsearch).

![Rechercher des images similaires à l’aide de l’option de la vue de carte](assets/search_find_similar.png)

*Figure : Recherchez des images similaires à l’aide de l’option de la vue de carte.*

### Images Adobe Stock {#adobestock}

From within the [!DNL Experience Manager] user interface, users can search [Adobe Stock assets](/help/assets/aem-assets-adobe-stock.md) and license the required assets. Ajoutez `Location: Adobe Stock` dans la barre Omni-recherche. Vous pouvez également utiliser le panneau Filtres pour trouver toutes les ressources qui sont ou non sous licence, ou effectuer des recherches dans une ressource spécifique à l’aide du numéro de fichier Adobe Stock.

### Ressources Dynamic Media {#dmassets}

Vous pouvez filtrer les images Dynamic Media en sélectionnant **[!UICONTROL Dynamic Media]** > **[!UICONTROL Visionneuses]** dans le panneau **[!UICONTROL Filtres]**. Il filtre et affiche des ressources telles que des visionneuses d’images, des carrousels, des visionneuses de supports variés et des visionneuses à 360°.

### Recherche de valeurs spécifiques dans les champs de métadonnées {#gqlsearch}

Vous pouvez rechercher des fichiers en fonction des valeurs exactes de champs de métadonnées spécifiques, tels que le titre, la description et l’auteur. La fonction de recherche en texte intégral GQL récupère uniquement les ressources dont la valeur de métadonnées correspond exactement à votre requête. Les noms des propriétés (auteur, titre, etc.) et les valeurs sont sensibles à la casse.

| Champ de métadonnées | Valeur et utilisation des facettes |
| ----------------------------------------- | ------------------------------------- |
| Titre | title:John |
| Créateur | creator:John |
| Emplacement | location:NA |
| Description | description:&quot;Sample Image&quot; |
| Outil créateur | creatortool:&quot;Adobe Photoshop CC 2020&quot; |
| Détenteur de copyright | copyrightowner:&quot;Adobe Systems&quot; |
| Contributeur | contributor:John |
| Conditions d’utilisation | usageterms:&quot;CopyRights Reserved&quot; |
| Créé | created:AAAA-MM-JJTHH |
| Date d’expiration | expires:AAAA-MM-JJTHH |
| Heure d’activation | ontime:AAAA-MM-JJTHH |
| Heure de désactivation | offtime:AAAA-MM-JJTHH |
| Intervalle de temps (expires dateontime, offtime) | facet field : lowerboundupperbound |
| Chemin | /content/dam/&lt;nom_dossier> |
| Titre du PDF | pdftitle:&quot;Adobe Document&quot; |
| Objet | subject:&quot;Training&quot; |
| Balises | tags:&quot;Location And Travel&quot; |
| Type | type:&quot;image\png&quot; |
| Largeur de l’image | width:lowerboundupperbound |
| Hauteur de l’image | height:lowerboundupperbound |
| Personne | person:John |

The properties `path`, `limit`, `size`, and `orderby` cannot be *ORed* with any other property.

Le mot-clé d’une propriété générée par un utilisateur correspond au libellé de son champ dans l’éditeur de propriétés en minuscules et sans espace.

Voici quelques exemples de formats de recherche pour des requêtes complexes :

* Pour afficher toutes les ressources avec plusieurs champs de facettes (par exemple : title=John Doe et creator tool=Adobe Photoshop) :  `tiltle:"John Doe" creatortool:Adobe*`
* Pour afficher toutes les ressources lorsque la valeur de la facette est une expression et non un seul mot (par exemple : le titre est Scott Reynolds) : `title:"Scott Reynolds"`
* Pour afficher les ressources avec plusieurs valeurs d’une seule propriété (le titre est Scott Reynolds ou John Doe, par exemple) : `title:"Scott Reynolds" OR "John Doe"`
* Pour afficher les ressources avec des valeurs de propriété commençant par une chaîne spécifique (par exemple : le titre est Scott Reynolds) : `title:Scott*`
* Pour afficher les ressources avec des valeurs de propriété se terminant par une chaîne spécifique (par exemple : le titre est Scott Reynolds) : `title:*Reynolds`
* Pour afficher les ressources avec une valeur de propriété contenant une chaîne spécifique (par exemple : le titre est Basel Meeting Room) : `title:*Meeting*`
* Pour afficher les ressources qui contiennent une chaîne spécifique et qui possèdent une valeur de propriété en particulier (par exemple : rechercher une chaîne Adobe parmi les ressources dont le titre est John Doe) : `*Adobe* title:"John Doe"`

## Search assets from other [!DNL Experience Manager] offerings or interfaces {#beyondomnisearch}

[!DNL Adobe Experience Manager] connecte le référentiel DAM à diverses autres [!DNL Experience Manager] solutions afin de fournir un accès plus rapide aux ressources numériques et de rationaliser les workflows de création. Toute découverte de ressources commence par la navigation ou la recherche. Le comportement de recherche reste largement le même sur les différentes surfaces et solutions. Some search methods change as the target audience, the use cases, and the user interface vary across the [!DNL Experience Manager] solutions. Les méthodes spécifiques sont documentées pour les solutions individuelles dans les liens ci-dessous. Les conseils et comportements universellement applicables sont décrits dans cet article.

### Recherche de ressources à partir du panneau Adobe Asset Link {#aal}

Using Adobe Asset Link, the creative professionals can now access content stored in [!DNL Experience Manager Assets], without leaving the supported Adobe Creative Cloud apps. Creatives can seamlessly browse, search, check out, and check in assets using the in-app panel in the [!DNL Adobe Creative Cloud apps]: [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], and [!DNL Adobe InDesign]. Asset Link permet également aux utilisateurs de rechercher des résultats visuellement similaires. Les résultats d’affichage de la recherche visuelle sont optimisés par les algorithmes d’apprentissage automatique d’Adobe Sensei et aident les utilisateurs à trouver des images à l’esthétique similaire. Voir [Rechercher et parcourir des ressources](https://helpx.adobe.com/fr/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) à l’aide d’Adobe Asset Link.

### Search assets in [!DNL Experience Manager] desktop app {#desktopapp}

Creative professionals use the desktop app to make the [!DNL Experience Manager Assets] easily searchable and available on their local desktop (Win or Mac). Creatives can easily reveal the desired assets in Mac Finder or Windows Explorer, opened in desktop applications, and changed locally - the changes are saved back to [!DNL Experience Manager] with a new version created in the repository. The application supports basic searches using one or more keywords, `*` and `?` wildcards, and `AND` operator. Voir [Navigation, recherche et prévisualisation des ressources](https://docs.adobe.com/content/help/fr-FR/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) dans l’application de bureau.

### Search assets in [!DNL Brand Portal] {#brandportal}

Les utilisateurs métiers et les spécialistes marketing utilisent Brand Portal pour partager efficacement et en toute sécurité les ressources numériques approuvées avec leurs équipes internes étendues, partenaires et revendeurs. Voir [Recherche de ressources sur Brand Portal](https://docs.adobe.com/content/help/fr-FR/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Rechercher [!DNL Adobe Stock] des images {#adobestock-1}

From within the [!DNL Experience Manager] user interface, users can search Adobe Stock assets and license the required assets. Ajoutez `Location: Adobe Stock` dans le champ Omni-recherche. Vous pouvez également utiliser le panneau **[!UICONTROL Filtres]** pour trouver toutes les ressources qui sont ou non sous licence, ou effectuer des recherches dans une ressource spécifique à l’aide du numéro de fichier Adobe Stock. See [manage Adobe Stock images in Experience Manager](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Recherche de ressources Dynamic Media {#dynamicmedia}

Vous pouvez filtrer les images Dynamic Media en sélectionnant **[!UICONTROL Dynamic Media]** > **[!UICONTROL Visionneuses]** dans le panneau **[!UICONTROL Filtres]**. Il filtre et affiche des ressources telles que des visionneuses d’images, des carrousels, des visionneuses de supports variés et des visionneuses à 360°. Lors de la création de pages web, les auteurs peuvent rechercher des visionneuses dans l’outil de recherche de contenu. Un filtre est disponible pour les visionneuses dans un menu contextuel.

### Recherche de ressources dans l’outil de recherche de contenu lors de la création de pages web {#contentfinder}

Les auteurs peuvent utiliser l’outil de recherche de contenu pour rechercher les ressources appropriées dans le référentiel de gestion des ressources numériques et les utiliser dans les pages web qu’ils créent. Les auteurs peuvent également utiliser la fonctionnalité Ressources connectées pour rechercher des ressources disponibles dans un [!DNL Experience Manager] déploiement distant. Les auteurs peuvent alors utiliser ces ressources dans des pages Web lors d’un [!DNL Experience Manager] déploiement local. See [use remote assets](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Recherche de collections {#collections}

[!DNL Experience Manager]La fonctionnalité de recherche prend en charge la recherche de collections et la recherche de ressources dans une collection. Voir [Recherche de collections](/help/assets/managing-collections-touch-ui.md).

## Sélecteur de ressources {#assetpicker}

>[!NOTE]
>
>Asset selector was called [asset picker](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) in prior versions of [!DNL Adobe Experience Manager].

Le sélecteur de ressources vous permet de parcourir, de rechercher et de filtrer les ressources DAM d’une manière spéciale. Vous pouvez lancer le sélecteur de ressources dans votre [!DNL Experience Manager] instance à l’aide `https://[aem-server]:[port]/aem/assetpicker.html`. Cette URL ouvre le sélecteur de ressources en mode de navigation. Utilisez les paramètres de requête pris en charge comme suffixe, par exemple `mode` (sélections uniques ou multiples), ou `viewmode` avec `assettype` (image, vidéo, texte) et `mimetype`. Ces paramètres définissent le contexte du sélecteur de ressources pour une instance de recherche particulière et restent inchangés tout au long de la sélection. Vous pouvez également récupérer les métadonnées des fichiers que vous sélectionnez à l’aide de cette fonctionnalité.

Le sélecteur de ressources utilise le message HTML5 `Window.postMessage` pour envoyer au destinataire les données correspondant à la ressource sélectionnée. Il fonctionne uniquement en mode Parcourir et uniquement avec la page de résultats d&#39;Omnisearch.

Transférez les paramètres de requête suivants dans une URL pour lancer le sélecteur de ressources dans un contexte particulier :

| Nom | Valeurs | Exemple | Objectif |
|---|---|---|---|
| suffixe de la ressource (B) | Chemin d’accès au dossier indiqué comme suffixe de la ressource dans l’URL :[https://localhost:4502/aem/assetpicker.html/&lt;chemin_dossier>](https://localhost:4502/aem/assetpicker.html) | To launch the asset selector with a particular folder selected, for example with the folder `/content/dam/we-retail/en/activities` selected, the URL should be of the form: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | Si vous avez besoin de sélectionner un dossier en particulier au démarrage du sélecteur de ressources, vous pouvez l’indiquer comme suffixe de ressource. |
| mode | single, multiple | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | En mode multiple, vous pouvez sélectionner plusieurs ressources simultanément à l’aide du sélecteur de ressources. |
| dialog | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Utilisez ces paramètres pour ouvrir le sélecteur de ressources en tant que boîte de dialogue Granite. Cette option ne peut être appliquée qu’au démarrage du sélecteur de ressources via le champ Chemin de Granite, en la configurant comme URL pickerSrc. |
| root | &lt;chemin_dossier> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-commerce/fr/activités) | Utilisez cette option pour spécifier le dossier racine du sélecteur de ressources. Ici, le sélecteur de ressources ne vous permet de sélectionner qu’une seule ressource enfant (directe/indirecte) sous le dossier racine. |
| viewmode | de recherches |  | Pour lancer le sélecteur de ressources en mode de recherche, avec les paramètres de type et de type de ressource. |
| assettype | images, documents, multimedia, archives | <ul><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=images](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=multimedia](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=archives](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=archives)</li></ul> | Utilisez cette option pour filtrer les types de ressources en fonction de la valeur indiquée. |
| mimetype | Type(s) MIME (`/jcr:content/metadata/dc:format`) d’une ressource (le caractère générique est également pris en charge) | <ul><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=image/png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation&amp;mimetype=*png)</li></ul> | Utilisez-le pour filtrer les ressources basées sur le(s) type(s) de MIME |

Pour accéder à l’interface du sélecteur de ressources, accédez à `https://[aem_server]:[port]/aem/assetpicker`. Recherchez le dossier souhaité, puis sélectionnez une ou plusieurs ressources. Vous pouvez également rechercher la ressource souhaitée dans la zone Omni-recherche, appliquer un filtre selon vos besoins, puis la sélectionner.

![Parcourir et sélectionner un fichier dans le sélecteur de fichiers](assets/assetpicker.png)

*Figure : Recherchez et sélectionnez un fichier dans le sélecteur de ressources.*

## Restrictions {#limitations}

The search capability in [!DNL Experience Manager Assets] has the following limitations:

* N’entrez pas d’espace de début dans la requête, sinon la recherche ne fonctionne pas.
* [!DNL Experience Manager] peut continuer à afficher le terme de recherche une fois que vous avez sélectionné les propriétés d’une ressource à partir des résultats de recherche, puis annuler la recherche. <!-- (CQ-4273540) -->
* Lors de la recherche de dossiers ou de fichiers et de dossiers, les résultats de recherche ne peuvent être triés selon aucun paramètre.
* If you press return without typing anything in Omnisearch bar, [!DNL Experience Manager] returns a list of only files and not folders. If you search specifically for folders without using a keyword, [!DNL Experience Manager] does not return any results.
* Utilisez l’option **[!UICONTROL Sélectionner tout]** dans le coin supérieur droit de la page de recherche pour sélectionner les fichiers recherchés. [!DNL Experience Manager] affiche initialement 100 actifs dans la vue de cartes et 200 actifs dans la vue de listes. D’autres ressources sont chargées lorsque vous faites défiler les résultats de la recherche. Vous pouvez sélectionner plus de ressources que les ressources chargées. Le décompte des ressources sélectionnées s’affiche dans le coin supérieur droit de la page des résultats de la recherche. Vous pouvez effectuer des opérations sur la sélection, par exemple télécharger les fichiers sélectionnés, mettre à jour les propriétés de métadonnées en bloc pour les fichiers sélectionnés ou ajouter les fichiers sélectionnés à une collection. Lorsque plus de ressources sont sélectionnées que affichées, une action est appliquée à toutes les ressources sélectionnées ou une boîte de dialogue affiche le nombre de ressources sur lesquelles elle est appliquée. Pour appliquer une action aux ressources qui n’ont pas été chargées, assurez-vous que toutes les ressources sont explicitement sélectionnées.

La recherche visuelle ou par analogie présente les restrictions suivantes :

* La recherche visuelle fonctionne mieux avec les référentiels plus volumineux. Bien qu’il n’y ait pas de nombre minimal d’images requis pour obtenir de bons résultats, la qualité des correspondances avec quelques images peut ne pas être aussi bonne qu’avec un référentiel de taille plus conséquente.
* You cannot change the model or train [!DNL Experience Manager] to find similar images. Par exemple, l’ajout ou la suppression de balises intelligentes dans quelques ressources ne modifie pas le modèle. Les ressources sont exclues des résultats de recherche visuellement similaires.

Les performances de la fonctionnalité de recherche peuvent être limitées dans les cas suivants :

* La vue de cartes a un temps de chargement plus rapide que la vue de listes pour afficher les résultats de la recherche.

## Conseils de recherche {#tips}

* Si vous surveillez l’état de révision des ressources, utilisez l’option appropriée pour trouver les ressources qui sont approuvées ou en attente d’approbation.
* Utilisez le prédicat Statistiques pour rechercher les ressources prises en charge en fonction de leurs statistiques d’utilisation obtenues auprès de diverses applications Creative. Les données d’utilisation sont regroupées sous Note d’utilisation, Impressions, Clics et Canaux de médias où les ressources apparaissent dans des catégories.
* Cochez la case **[!UICONTROL Sélectionner tout]** pour sélectionner les fichiers recherchés. [!DNL Experience Manager] affiche initialement 100 actifs dans la vue de cartes et 200 actifs dans la vue de listes. D’autres ressources sont chargées lorsque vous faites défiler les résultats de la recherche. Vous pouvez sélectionner plus de ressources que les ressources chargées. Le décompte des ressources sélectionnées s’affiche dans le coin supérieur droit de la page des résultats de la recherche. Vous pouvez effectuer des opérations sur la sélection, par exemple télécharger les fichiers sélectionnés, mettre à jour les propriétés de métadonnées en bloc pour les fichiers sélectionnés ou ajouter les fichiers sélectionnés à une collection. Lorsque plus de ressources sont sélectionnées que affichées, une action est appliquée à toutes les ressources sélectionnées ou une boîte de dialogue affiche le nombre de ressources sur lesquelles elle est appliquée. Pour appliquer une action aux ressources qui n’ont pas été chargées, assurez-vous que toutes les ressources sont explicitement sélectionnées.
* Pour rechercher les ressources qui ne contiennent pas les métadonnées obligatoires, voir [Métadonnées obligatoires](#mandatorymetadata).
* La recherche utilise tous les champs de métadonnées. Une recherche générique, telle que la recherche du nombre 12, renvoie généralement de nombreux résultats. Pour de meilleurs résultats, utilisez des guillemets doubles (et non des guillemets simples) ou assurez-vous que le nombre est attaché à un mot sans caractère spécial (par exemple, *chaussure12*).
* La recherche de texte intégral prend en charge les opérateurs tels que - et ^. Pour rechercher des informations sous forme de chaînes littérales, indiquez la phrase de recherche entre guillemets. Par exemple, entrez « Notebook - Beauté » au lieu de Notebook - Beauté.
* Si les résultats de recherche sont trop nombreux, limitez la [portée de la recherche](#scope) pour trouver les ressources souhaitées. Cela fonctionne mieux lorsque vous avez une idée de la meilleure manière de rechercher les ressources que vous recherchez, par exemple un type de fichier, un emplacement ou des métadonnées spécifiques.

* **Balisage**: Les balises vous aident à classer les fichiers qui peuvent être parcourus et recherchés plus efficacement. Le balisage permet de propager la taxonomie appropriée à d’autres utilisateurs et workflows. [!DNL Experience Manager] propose des méthodes pour baliser automatiquement les ressources à l’aide des services d’intelligence artificielle d’Adobe Sensei, qui améliorent constamment le balisage de vos ressources au fil de l’utilisation et de l’entraînement. Lorsque vous recherchez des ressources, les balises intelligentes sont prises en compte si la fonction est activée sur votre compte. Cela fonctionne avec la fonctionnalité de recherche intégrée. Voir [Comportement de la recherche](#searchbehavior). Pour optimiser l’ordre d’affichage des résultats de recherche, vous pouvez [améliorer le classement](#searchrank) de quelques ressources sélectionnées.

* **Indexation** : seules les métadonnées et les ressources indexées sont renvoyées dans les résultats de recherche. Pour une meilleure couverture et de meilleures performances, veillez à une indexation appropriée et suivez les bonnes pratiques. Voir [Indexation](#searchindex).

## Quelques exemples illustrant la recherche {#samples}

Utilisez des guillemets doubles autour des mots-clés pour rechercher des ressources contenant exactement l’expression dans l’ordre exact spécifié par l’utilisateur.

![Comportement de recherche avec et sans guillemets](assets/search_with_quotes.gif)

*Figure : Comportement de recherche avec et sans guillemets.*

**Recherche avec un caractère générique (astérisque)** : pour élargir la recherche, utilisez un astérisque avant ou après le mot recherché afin de faire correspondre n’importe quel nombre de caractères. Par exemple, la recherche du mot run sans astérisque ne renvoie pas les ressources contenant une variante du mot (y compris dans les métadonnées). L’astérisque remplace n’importe quel nombre de caractères. Par exemple :

* `run` renvoie les ressources contenant exactement le mot-clé « run ».
* `run*` renvoie les ressources concernant « running », « run », « runaway », etc.
* `*run` renvoie « outrun », « rerun », etc.
* `*run*` renvoie toutes les combinaisons possibles.

![Exemple d’utilisation d’un caractère générique (astérisque) dans la recherche de ressources](assets/search_with_asterisk_run.gif)

*Figure : Illustration de l’utilisation d’un caractère générique d’astérisque dans la recherche de ressources à l’aide d’un exemple.*

**Recherche avec un caractère générique (point d’interrogation)** : pour élargir la recherche, utilisez un ou plusieurs caractères « ? » pour correspondre au nombre exact de caractères. Par exemple, dans l’illustration suivante :

* la requête `run???` ne correspond à aucune ressource ;

* la requête `run????` correspond au mot `running` avec quatre caractères après `run` ;

* la requête `??run` correspond au mot `rerun` avec deux caractères avant `run`.

![Exemple d’utilisation d’un caractère générique (point d’interrogation) dans la recherche de ressources](assets/search_with_questionmark_run.gif)

*Figure : Illustration de l’utilisation d’un caractère générique de point d’interrogation dans la recherche de ressources à l’aide d’un exemple.*

**Exclusion d’un mot-clé** : utilisez le tiret pour rechercher des ressources qui ne contiennent pas de mot-clé. Par exemple, la requête `running -shoe` renvoie les ressources qui contiennent `running`, mais pas `shoe`. De même, la requête `camp -night` renvoie les ressources qui contiennent `camp`, mais pas `night`. The query `camp-night` returns assets that contain both `camp` and `night`.

![Utilisation du tiret pour rechercher des ressources ne contenant pas de mot-clé exclu](assets/search_dash_exclude_keyword.gif)

*Figure : Utilisation du tiret pour rechercher des ressources ne contenant pas de mot-clé exclu.*

## Tâches de configuration et d’administration liées aux fonctionnalités de recherche {#configadmin}

### Rechercher les configurations d&#39;index {#searchindex}

La découverte des ressources repose sur l’indexation du contenu de la gestion des actifs numériques, y compris les métadonnées. La découverte plus rapide et précise des ressources repose sur une indexation optimisée et des configurations appropriées. Voir index [de](/help/assets/performance-tuning-guidelines.md#search-indexes)recherche, requêtes de [chêne et indexation](/help/sites-deploying/queries-and-indexing.md), et [bonnes pratiques](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

Pour exclure des ressources spécifiques des résultats de la recherche, utilisez `excludedPath` la propriété de l’index Lucene.

### Recherche visuelle ou par analogie {#configvisualsearch}

La recherche visuelle utilise un balisage intelligent et requiert la version [!DNL Experience Manager] 6.5.2.0 ou ultérieure. Après avoir configuré la fonctionnalité de balisage intelligent, procédez comme suit :

1. Dans [!DNL Experience Manager] CRXDE, dans le `/oak:index/lucene` noeud, ajoutez les propriétés et valeurs suivantes et enregistrez les modifications.

   * `costPerEntry` de type `Double` avec la valeur `10`.
   * `costPerExecution` de type `Double` avec la valeur `2`.
   * `refresh` de type `Boolean` avec la valeur `true`.

   Cette configuration permet d&#39;effectuer des recherches à partir de l&#39;index approprié.

1. Pour créer un index Lucene, dans CRXDE, à `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, créez un noeud nommé `imageFeatures` de type `nt-unstructured`. Dans le `imageFeatures` noeud,

   * ajouter `name` la propriété de type `String` avec la valeur `jcr:content/metadata/imageFeatures/haystack0`.
   * ajouter `nodeScopeIndex` la propriété de type `Boolean` avec la valeur de `true`.
   * ajouter `propertyIndex` la propriété de type `Boolean` avec la valeur de `true`.
   * ajouter `useInSimilarity` la propriété de type `Boolean` avec la valeur `true`.

   Enregistrez les modifications.

1. Accédez `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` à la propriété `similarityTags` de type `Boolean` et ajoutez-la avec la valeur `true`de.
1. Appliquez des balises actives aux actifs de votre [!DNL Experience Manager] référentiel. Voir [comment configurer des balises](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)actives.
1. Dans CRXDE, dans le `/oak-index/damAssetLucene` noeud, définissez la `reindex` propriété sur `true`. Enregistrez les modifications.
1. (Facultatif) Si vous avez personnalisé le formulaire de recherche, copiez le `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` noeud dans `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Enregistrez les modifications.

Pour plus d’informations, voir [Comprendre les balises actives en Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-feature-video-use.html) et [comment gérer les balises](/help/assets/managing-smart-tags.md)actives.

>[!CAUTION]
>
>Si l’indexation Lucene est désactivée [!DNL Adobe Experience Manager], la recherche basée sur des balises actives ne fonctionne pas comme prévu.

### Métadonnées obligatoires {#mandatorymetadata}

Les utilisateurs professionnels, les administrateurs ou les bibliothécaires de gestion des actifs numériques peuvent définir certaines métadonnées comme des métadonnées obligatoires indispensables au fonctionnement des processus d’entreprise. Pour diverses raisons, certaines ressources peuvent ne pas disposer de ces métadonnées, telles que les ressources héritées ou les ressources migrées en bloc. Les ressources contenant des métadonnées manquantes ou non valides sont détectées et rapportées en fonction de la propriété de métadonnées indexées. Pour le configurer, voir Métadonnées [](/help/assets/metadata-schemas.md#define-mandatory-metadata)obligatoires.

### Modification des facettes de recherche {#searchfacets}

Pour accélérer la découverte, [!DNL Experience Manager Assets] offres les facettes de recherche à l’aide desquelles vous pouvez filtrer les résultats de la recherche. Par défaut, le panneau Filtres comprend quelques facettes standard. Les administrateurs peuvent personnaliser le panneau Filtres pour modifier les facettes par défaut à l’aide des prédicats intégrés. [!DNL Experience Manager] fournit une bonne collection de prédicats intégrés et un éditeur pour personnaliser les facettes. Voir Facettes [de](/help/assets/search-facets.md)recherche.

### Extraire du texte lors du téléchargement de fichiers {#extracttextupload}

Vous pouvez configurer [!DNL Experience Manager] l’extraction du texte des fichiers lorsque les utilisateurs téléchargent des fichiers, tels que des fichiers PSD ou PDF. [!DNL Experience Manager] indexe le texte extrait et aide les utilisateurs à rechercher ces ressources en fonction du texte extrait. See [upload assets](/help/assets/managing-assets-touch-ui.md#uploading-assets).

Si l’extraction de texte devient trop gourmande en ressources pour votre déploiement, pensez à [désactiver l’extraction](https://helpx.adobe.com/experience-manager/kb/Disable-binary-text-extraction-to-optimize-Lucene-indexing-AEM.html)de texte.

### Prédicats personnalisés pour filtrer les résultats de la recherche {#custompredicates}

Les prédicats sont utilisés pour créer des facettes. Les administrateurs peuvent personnaliser les facettes de recherche dans le panneau Filtres à l’aide de prédicats préconfigurés. Ces prédicats peuvent être personnalisés à l’aide d’incrustations. Voir [Création de prédicats](/help/assets/searchx.md)personnalisés.

Vous pouvez rechercher des ressources numériques en fonction d’une ou de plusieurs des propriétés suivantes. Les filtres qui s’appliquent à certaines de ces propriétés sont disponibles par défaut et certains autres filtres peuvent être créés sur mesure pour s’appliquer aux autres propriétés.

| Champ de recherche | Valeurs de propriété de recherche |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Types MIME  | Images, Documents, Multimédia, Archives ou Autre. |
| Dernière modification | Heure, Jour, Semaine, Mois ou Année. |
| Taille de fichier | Petit, Moyen ou Grand. |
| État de publication | Publiée ou Publication annulée. |
| État d’approbation | Accepté ou Rejeté. |
| Orientation | Horizontal, Vertical ou Carré. |
| Style | Couleur ou Noir et blanc |
| Hauteur de la vidéo | Indiqué sous la forme d’une valeur minimale et d’une valeur maximale. La valeur est stockée uniquement dans les métadonnées des rendus vidéo. |
| Largeur de la vidéo | Indiqué sous la forme d’une valeur minimale et d’une valeur maximale. La valeur est stockée uniquement dans les métadonnées des rendus vidéo. |
| Format vidéo | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. La valeur est stockée dans les métadonnées de la vidéo source et dans les rendus éventuels. |
| Codec vidéo | x264. La valeur est stockée uniquement dans les métadonnées des rendus vidéo. |
| Débit vidéo | Indiqué sous la forme d’une valeur minimale et d’une valeur maximale. La valeur est stockée uniquement dans les métadonnées des rendus vidéo. |
| Codec audio | Libvorbis, Lame MP3, encodage AAC. La valeur est stockée uniquement dans les métadonnées des rendus vidéo. |
| Débit audio  | Indiqué sous la forme d’une valeur minimale et d’une valeur maximale. La valeur est stockée uniquement dans les métadonnées des rendus vidéo. |

## Utilisation des résultats de recherche de ressources {#aftersearch}

Vous pouvez effectuer les opérations suivantes avec les ressources que vous avez recherchées dans le Experience Manager :

* Afficher les propriétés de métadonnées et d’autres informations
* Télécharger une ou plusieurs ressources
* Utiliser les actions de bureau pour ouvrir ces ressources dans l’application de bureau
* Créer des collections dynamiques

### Tri des résultats de recherche {#sort}

Triez les résultats de la recherche pour découvrir plus rapidement les ressources requises. You can sort the search results in list view and only when you select **[[!UICONTROL Files]](#searchui)** from the **[!UICONTROL Filters]** panel. [!DNL Experience Manager Assets] utilise le tri côté serveur pour trier rapidement toutes les ressources (quel que soit leur nombre) dans un dossier ou les résultats d’une requête. Le tri côté serveur fournit des résultats plus rapides et plus précis que le tri côté client.

En mode Liste, vous pouvez trier les résultats de recherche tout comme vous pouvez trier les ressources de n’importe quel dossier. Le tri fonctionne sur ces colonnes : Nom, Titre, État, Dimensions, Taille, Évaluation, Utilisation, (Date de) création, (Date de) publication, Workflow et Extraits.

Pour connaître les restrictions de la fonctionnalité de tri, voir [Restrictions](#limitations).

### Consultation des informations détaillées d’une ressource {#checkinfo}

Vous pouvez consulter les informations détaillées d’une ressource recherchée à partir de la page des résultats de recherche.

Pour afficher toutes les métadonnées d’une ressource, sélectionnez-la, puis cliquez sur **[!UICONTROL Propriétés]** dans la barre d’outils.

Pour consulter les commentaires sur une ressource ou son historique de versions, cliquez sur la ressource afin d’ouvrir l’aperçu de grande taille. Ouvrez la chronologie dans le rail de gauche et sélectionnez **[!UICONTROL Commentaires]** ou **[!UICONTROL Versions]**. Vous pouvez également trier l’activité de la chronologie comme les commentaires ou les versions dans un ordre chronologique.

![Tri des entrées de chronologie d’une ressource recherchée](assets/sort_timeline_search_results.gif)

*Figure : Tri des entrées de chronologie pour une ressource de recherche.*

### Téléchargement des ressources recherchées {#download}

Vous pouvez télécharger les ressources recherchées et leurs rendus de la même façon que vous téléchargez des ressources ordinaires à partir de dossiers. Sélectionnez une ou plusieurs ressources dans les résultats de recherche, puis cliquez sur **[!UICONTROL Télécharger]** dans la barre d’outils.

### Mise à jour des propriétés de métadonnées en masse {#metadataupdates}

Il est possible d’effectuer des mises à jour en masse des champs de métadonnées courants de plusieurs ressources. Dans les résultats de recherche, sélectionnez une ou plusieurs ressources. Cliquez sur **[!UICONTROL Propriétés]** dans la barre d’outils et mettez à jour les métadonnées selon les besoins. Cliquez sur **[!UICONTROL Enregistrer et fermer]** lorsque vous avez terminé. Les métadonnées figurant précédemment dans les champs mis à jour sont remplacées.

For the assets that are available in a single folder or a collection, it is easier to [update the metadata in bulk](/help/assets/managing-multiple-assets.md) without using the search functionality. Pour les ressources disponibles dans plusieurs dossiers ou correspondant à un critère commun, il est plus rapide de mettre à jour les métadonnées en masse par l’intermédiaire d’une recherche.

### Collections dynamiques {#collections-1}

Une collection est un ensemble ordonné de ressources pouvant inclure des ressources provenant de différents emplacements, car les collections ne contiennent que des références à ces ressources. Les collections sont de deux types :

* Une liste de référence statique de ressources, dossiers et autres collections
* Une liste dynamique (collection dynamique) qui peuple la collection de ressources en fonction de critères de recherche

Vous pouvez créer des collections dynamiques en fonction des critères de recherche. Dans le panneau **[!UICONTROL Filtres]**, sélectionnez **[!UICONTROL Fichiers]** et cliquez sur **[!UICONTROL Enregistrer la collection dynamique]**. Voir [Gestion des collections](/help/assets/managing-collections-touch-ui.md).

## Résolution des problèmes et des résultats de recherche inattendus {#troubleshoot-unexpected-search-results-and-issues}

| Erreur, problèmes, symptômes | Raison possible | Correction ou compréhension possible du problème |
|---|---|---|
| Résultats incorrects lors de la recherche de fichiers avec des métadonnées manquantes. | When searching for assets that are missing the mandatory metadata, [!DNL Experience Manager] may display some assets that have valid metadata. Les résultats sont basés sur la propriété de métadonnées indexées. | Une fois les métadonnées mises à jour, la réindexation est nécessaire pour refléter l’état correct des métadonnées des fichiers. Voir [Métadonnées obligatoires](metadata-schemas.md#define-mandatory-metadata). |
| Trop de résultats de recherche. | Paramètre de recherche étendu. | Envisagez de limiter la [portée de la recherche](#scope). L’utilisation de balises actives peut vous donner plus de résultats de recherche que vous ne le pensiez. Voir Comportement [de la recherche avec des balises](#withsmarttags)actives. |
| Résultats de recherche sans rapport ou partiellement liés. | Le comportement de recherche change avec le balisage intelligent. | Comprenez [comment la recherche change après un balisage](#withsmarttags)intelligent. |
| Aucune suggestion de saisie semi-automatique pour les ressources. | Les actifs nouvellement transférés ne sont pas encore indexés. Les métadonnées ne sont pas immédiatement disponibles en tant que suggestions lorsque vous début taper un mot-clé de recherche dans la barre de recherche d&#39;Omniture. | [!DNL Assets] attend jusqu’à l’expiration d’un délai d’attente (par défaut, une heure) avant d’effectuer une tâche en arrière-plan afin d’indexer les métadonnées pour toutes les ressources chargées/mises à jour dernièrement et de les ajouter à la liste de suggestions. |
| Aucun résultat de recherche. | <ul><li>Les ressources correspondant à votre requête n&#39;existent pas. </li><li> Espace blanc ajouté avant la requête de recherche. </li><li> Le champ de métadonnées non pris en charge contient le mot-clé que vous avez recherché.</li><li> Recherche effectuée pendant les heures d’arrêt d’une ressource. </li></ul> | <ul><li>Recherche à l’aide d’un autre mot-clé. Vous pouvez également utiliser le balisage intelligent ou la recherche par analogie pour améliorer les résultats de la recherche. </li><li>[Limite](#limitations)connue.</li><li>Tous les champs de métadonnées ne sont pas pris en compte pour les recherches. Voir [Portée](#scope).</li><li>Effectuez une recherche ultérieurement ou modifiez les ressources à l’heure et les heures d’arrêt pour les ressources requises.</li></ul> |
| Aucun filtre de recherche ou prédicat n&#39;est disponible. | <ul><li>Le filtre de recherche n&#39;est pas configuré.</li><li>Il n&#39;est pas disponible pour votre connexion.</li><li>(Moins probable) Les options de recherche ne sont pas personnalisées sur le déploiement que vous utilisez.</li></ul> | <ul><li>Contactez l’administrateur pour vérifier si les personnalisations de la recherche sont disponibles ou non.</li><li>Contactez l’administrateur pour vérifier si votre compte dispose des privilèges/autorisations nécessaires pour utiliser la personnalisation.</li><li>Contactez l’administrateur et vérifiez les personnalisations disponibles pour le [!DNL Assets] déploiement que vous utilisez.</li></ul> |
| Lors de la recherche d’images visuellement similaires, une image attendue est manquante. | <ul><li>L&#39;image n&#39;est pas disponible dans [!DNL Experience Manager].</li><li>L&#39;image n&#39;est pas indexée. En règle générale, lorsqu’il est récemment téléchargé.</li><li>L’image n’est pas balisée de manière intelligente.</li></ul> | <ul><li>ajoutez l’image à [!DNL Assets].</li><li>Contactez votre administrateur pour réindexer le référentiel. Veillez également à utiliser l’index approprié.</li><li>Contactez votre administrateur pour baliser intelligemment les ressources appropriées.</li></ul> |
| Lors de la recherche d’images visuellement similaires, une image non pertinente s’affiche. | Comportement de recherche visuelle. | [!DNL Experience Manager] affiche autant de ressources potentiellement pertinentes que possible. Les images moins pertinentes, le cas échéant, sont ajoutées aux résultats, mais avec un classement inférieur dans les résultats de recherche. La qualité des correspondances et la pertinence des ressources recherchées diminuent à mesure que vous descendez dans les résultats de la recherche. |
| Lors de la sélection et du fonctionnement des résultats de la recherche, tous les fichiers recherchés ne sont pas exploités. | L&#39;option [!UICONTROL Sélectionner tout] sélectionne uniquement les 100 premiers résultats de recherche dans la vue de cartes et les 200 premiers résultats de recherche dans la vue de listes. |  |

>[!MORELIKETHIS]
>
>* [Guide de mise en oeuvre de la recherche Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Configuration avancée pour améliorer les résultats de recherche](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [Configuration de la recherche de traduction intelligente](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

