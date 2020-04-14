---
title: Recherche d’images et de ressources numériques dans AEM
description: Découvrez comment rechercher les ressources souhaitées dans AEM à l’aide du panneau Filtres et comment utiliser les ressources affichées dans la recherche.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: fc4d8f98047fe727c11aa7a932ecc46a1a60d076

---


# Recherche de ressources dans AEM    {#search-assets-in-aem}

Les ressources d’Adobe Experience Manager (AEM) fournissent des méthodes robustes de découverte de ressources qui vous aident à atteindre une vitesse de contenu supérieure. Vos équipes gagnent du temps à commercialiser grâce à une expérience de recherche intelligente et transparente, grâce à la fonctionnalité prête à l&#39;emploi et aux méthodes personnalisées. La recherche de ressources est essentielle pour l’utilisation d’un système de gestion des ressources numériques, que ce soit pour une utilisation plus poussée par les créatifs, pour une gestion robuste des ressources par les utilisateurs et spécialistes marketing ou pour l’administration par les administrateurs DAM. Les recherches simples, avancées et personnalisées que vous pouvez effectuer via l’interface utilisateur d’AEM Assets ou d’autres applications et surfaces permettent de répondre à ces cas d’utilisation.

AEM prend en charge les cas d’utilisation suivants dont cet article décrit l’utilisation, les concepts, les configurations, les limitations et le dépannage.

| Recherche de ressources | Configuration et administration | Utilisation des résultats de recherche |
|---|---|---|
| [Recherches de base](#searchbasics) | [Index de recherche](#searchindex) | [Tri des résultats](#sort) |
| [Présentation de l’interface utilisateur de recherche](#searchui) | [Recherche visuelle ou par analogie](#configvisualsearch) | [Vérification des propriétés et des métadonnées d’une ressource](#checkinfo) |
| [Suggestions de recherche](#searchsuggestions) | [Métadonnées obligatoires](#mandatorymetadata) | [Téléchargement](#download) |
| [Présentation des résultats de recherche et du comportement](#searchbehavior) | [Modification des facettes de recherche](#searchfacets) | [Mises à jour des métadonnées en masse](#metadataupdates) |
| [Classement et amplification des recherches](#searchrank) | [Extraction de texte](#extracttextupload) | [Collections dynamiques](#collections) |
| [Recherche avancée : filtrage et portée de la recherche](#scope) | [Prédicats personnalisés](#custompredicates) | [Présentation des résultats inattendus et dépannage](#troubleshoot-unexpected-search-results-and-issues) |
| [Rechercher à partir d’autres solutions et applications](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[Application de bureau AEM](#desktopapp)</li><li>[Images Adobe Stock](#adobestock)</li><li>[Ressources Dynamic Media](#dynamicmedia)</li></ul> |  |  |
| [Sélecteur de ressources](#assetselector) |  |  |
| [Limites](#limitations) et [conseils](#tips) |  |  |
| [Exemples illustrés](#samples) |  |  |

Recherchez des ressources à l’aide du champ Omnisearch en haut de l’interface Web d’AEM. Go to **[!UICONTROL Assets]** > **[!UICONTROL Files]** in AEM, click search icon in top bar, enter search keyword, and press return. Vous pouvez également utiliser le raccourci mot-clé / (barre oblique) pour ouvrir le champ Omnisearch. Emplacement : l’option Ressources est présélectionnée pour limiter les recherches aux ressources DAM. AEM fournit des suggestions lorsque votre  taper un mot-clé de recherche.

Utilisez le panneau **[!UICONTROL du]** pour restreindre votre recherche en filtrant les résultats de recherche en fonction des différentes options (prédicats), telles que le type de fichier, la taille du fichier, la date de dernière modification, l’état du fichier, les données d’informations et les licences Adobe Stock. Vos administrateurs peuvent personnaliser le panneau  du et ajouter ou supprimer des prédicats de recherche à l’aide des facettes de recherche. Le filtre Type [!UICONTROL de] fichier du panneau [!UICONTROL de] comporte des cases à cocher à états mixtes. Par conséquent, à moins que vous ne sélectionniez tous les prédicats imbriqués (ou formats), les cases à cocher du premier niveau sont partiellement cochées.

La fonctionnalité de recherche AEM prend en charge la recherche de collections et la recherche de ressources dans une collection. Voir [Recherche de collections](/help/assets/managing-collections-touch-ui.md).

## Présentation de l’interface de recherche {#searchui}

Familiarisez-vous avec l’interface de recherche et les actions disponibles.

![Présentation des parties de l’interface des résultats de la recherche Ressources](assets/aem_search_results.png)

*Figure : Présentation des parties de l’interface des résultats de la recherche Ressources*

**A.** Enregistrer la recherche en tant que collection dynamique. **B.** Filtres (prédicats) pour limiter les résultats de recherche. **C.** Afficher les fichiers, les dossiers ou les deux dans les résultats de recherche. **D.** Cliquer sur Filtres pour ouvrir ou fermer le rail de gauche. **E.** L’emplacement de recherche est la gestion des ressources numériques. **F.** Champ Omnisearch avec mot-clé de recherche fourni par l’utilisateur. **G.** Cochez cette case pour sélectionner tous les résultats de la recherche. **H.** Nombre de résultats de recherche affichés par rapport au total des résultats de recherche. **I.** Ferme la recherche **J.** Basculez entre les  de carte et les  de .

### Facettes de recherche dynamique {#dynamicfacets}

Vous pouvez découvrir plus rapidement les ressources de votre choix à partir de la page des résultats de recherche en utilisant le nombre de résultats de recherche attendus mis à jour dynamiquement dans les facettes de recherche. Le nombre prévu de ressources est mis à jour avant même d’appliquer le filtre de recherche. L’affichage du nombre prévu par rapport au filtre vous aide à parcourir rapidement et efficacement les résultats de la recherche. Pour plus d’informations, voir [Recherche de ressources dans AEM](search-assets.md).

![Affichage du nombre approximatif de ressources sans filtrer les résultats de la recherche dans les facettes de recherche.](assets/asset_search_results_in_facets_filters.png)

*Figure : Afficher le nombre approximatif de fichiers sans filtrer les résultats de recherche dans les facettes de recherche*

## Présentation des résultats de recherche et du comportement {#searchbehavior}

### Termes et résultats de recherche de base {#searchbasics}

Vous pouvez exécuter des recherches de mots-clés à partir du champ Omni-recherche. La recherche de mots-clés n’est pas sensible à la casse et il s’agit d’une recherche en texte intégral (dans les champs de métadonnées courants. Si plusieurs mots-clés sont recherchés, l’opérateur par défaut entre les mots-clés correspond `AND` à la recherche par défaut et `OR` lorsque les ressources sont balisées intelligemment.

Les résultats sont triés par pertinence, en commençant par les correspondances les plus proches. Pour plusieurs mots-clés, les ressources qui contiennent les deux termes dans leurs métadonnées génèrent des résultats plus pertinents. Dans les métadonnées, les mots-clés qui apparaissent sous forme de balises intelligentes sont classés plus haut que les mots-clés qui apparaissent dans d’autres champs de métadonnées. AEM permet de donner plus de poids à un terme de recherche particulier. Also, it is possible to [boost the rank](#searchrank) of a few targeted assets for specific search terms.

Pour rechercher rapidement les ressources appropriées, l’interface riche fournit des mécanismes de filtrage, de tri et de sélection. Vous pouvez filtrer les résultats selon plusieurs critères et afficher le nombre de ressources recherchées pour différents filtres. Vous pouvez également réexécuter la recherche en modifiant la requête dans le champ Omni-recherche. Lorsque vous modifiez les termes ou filtres de recherche, les autres filtres restent appliqués pour préserver le contexte de la recherche.

Lorsque les résultats sont de nombreux actifs, AEM affiche les 100 premiers dans le de cartes et 200 premiers dans le  de. Lorsque les utilisateurs font défiler le contenu, d’autres fichiers sont chargés. Ceci est pour améliorer les performances.

>[!VIDEO](https://www.youtube.com/watch?v=LcrGPDLDf4o)

Il arrive que des ressources inattendues apparaissent dans les résultats de la recherche. Pour plus d’informations, voir [Résultats inattendus](#troubleshoot-unexpected-search-results-and-issues).

AEM peut effectuer des recherches dans de nombreux formats de fichiers et les filtres de recherche peuvent être personnalisés en fonction des besoins de votre entreprise. Contactez votre administrateur pour connaître les options de recherche disponibles pour votre référentiel DAM et les restrictions de votre compte.

### Résultats avec et sans balises actives améliorées {#withsmarttags}

Par défaut, la recherche AEM associe les termes de recherche avec une clause ET. Par exemple, pensez à rechercher des mots-clés en cours d’exécution. Par défaut, seuls les fichiers contenant des mots-clés de femme et des mots-clés en cours d’exécution dans les métadonnées apparaissent dans les résultats de la recherche. Le même comportement est conservé lorsque des caractères spéciaux (points, traits de soulignement ou tirets) sont utilisés avec les mots-clés. Le de recherche suivant  les mêmes résultats :

* `woman running`
* `woman.running`
* `woman-running`

Toutefois, le `woman -running` renvoie des fichiers sans `running` les métadonnées.
Using smart tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. Les résultats de la recherche sont donc une combinaison de

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Actifs balisés avec l’un ou l’autre des mots-clés (comportement Balises dynamiques).

### Suggestions de recherche en cours de frappe {#searchsuggestions}

Lorsque vous  taper des mots-clés, AEM suggère les mots-clés ou expressions de recherche possibles. Les suggestions sont basées sur les métadonnées des ressources existantes. AEM indexe tous les champs de métadonnées pour faciliter la recherche. Pour fournir des suggestions de recherche, le système utilise les valeurs des quelques champs de métadonnées suivants. Pour fournir des suggestions de recherche, pensez à renseigner les champs suivants avec les mots-clés appropriés :

* Balises de ressources. (mappage avec `jcr:content/metadata/cq:tags`)
* Titre de la ressource. (mappage avec `jcr:content/metadata/dc:title`)
* Description de la ressource. (mappage avec `jcr:content/metadata/dc:description`)
* Titre dans le référentiel JCR. La valeur peut être mappée au titre de la ressource. (mappage avec `jcr:content/jcr:title`)
* Description dans le référentiel JCR. La valeur peut être mappée à la description de la ressource. (mappage avec `jcr:content/jcr:description`)

Pour recevoir des suggestions pour plusieurs mots-clés de recherche, continuez à taper tous les mots-clés sans sélectionner aucune suggestion pour un seul mot-clé.

![Tapez plusieurs mots-clés pour  suggestions qui les adaptent tous.](assets/search_suggestionsmanykeywords.gif)

*Figure : Tapez plusieurs mots-clés pour  suggestions qui les adaptent tous.*

### Classement et amplification des recherches {#searchrank}

Les résultats de recherche qui correspondent à tous les termes de recherche dans les champs de métadonnées s’affichent en premier, suivis des résultats de recherche correspondant à l’un des termes de recherche des balises dynamiques. Dans l’exemple ci-dessus, l’ordre approximatif de l’affichage des résultats de recherche est le suivant :

1. Correspondances de `woman running` dans les différents champs de métadonnées.
1. Correspondances de `woman running` dans les balises intelligentes.
1. Correspondances de `woman` ou de `running` dans les balises intelligentes.

Vous pouvez améliorer la pertinence des mots-clés pour des ressources données afin d’améliorer les résultats de recherches basées sur ces mots-clés. En d’autres termes, les images pour lesquelles vous faites la promotion de mots-clés spécifiques apparaissent en haut des résultats lorsque vous lancez une recherche basée sur ces mots-clés.

1. Dans l’interface utilisateur d’Assets, ouvrez la page des propriétés de la ressource. Cliquez sur **[!UICONTROL Avancé]** et cliquez/appuyez sur **[!UICONTROL Ajouter]** sous **[!UICONTROL Élever pour les mots-clés de recherche]**.
1. Dans la boîte de dialogue **[!UICONTROL Rechercher une promotion]**, indiquez un mot-clé pour lequel vous souhaitez améliorer la recherche d’image, puis cliquez/appuyez sur **[!UICONTROL Ajouter]**. Vous pouvez indiquer plusieurs mots-clés de la même manière.
1. Cliquez/appuyez sur **[!UICONTROL Enregistrer et fermer]**. La ressource pour laquelle vous avez promu ce mot-clé apparaît en tête des résultats de recherche.

Vous pouvez l’utiliser à votre avantage en améliorant le classement de certaines ressources dans les résultats de recherche du mot-clé ciblé. Voir la vidéo d’exemple ci-dessous. Pour plus d’informations, voir [Recherche dans AEM](https://helpx.adobe.com/experience-manager/kt/assets/using/search-feature-video-use.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Découvrez comment les résultats de recherche sont classés et comment le classement peut être influencé.*

## Recherche avancée {#scope}

AEM fournit diverses méthodes, telles que des filtres qui s’appliquent aux ressources recherchées, pour vous aider à localiser plus rapidement les ressources qu’il vous faut. Quelques méthodes fréquemment utilisées sont décrites ci-dessous. Vous trouverez ci-dessous plusieurs [exemples illustrés](#samples).

**Recherche de fichiers ou de dossiers** : dans les résultats de recherche, reportez-vous aux fichiers, aux dossiers ou aux deux. Dans le panneau **[!UICONTROL Filtres]**, vous pouvez sélectionner l’option appropriée. Voir [Interface de recherche](#searchui).

**Recherche de ressources dans un dossier** : vous pouvez limiter la recherche à un dossier spécifique. Dans le panneau **[!UICONTROL Filtres]**, ajoutez le chemin d’un dossier. Vous ne pouvez sélectionner qu’un dossier à la fois.

![Limitation des résultats de recherche à un dossier en ajoutant un chemin de dossier dans le panneau Filtres](assets/search_folder_select.gif)

*Figure : Limiter les résultats de recherche à un dossier en ajoutant un chemin de dossier dans le panneau  de*

### Rechercher des images similaires {#visualsearch}

Pour rechercher des images visuellement similaires à une image sélectionnée par l’utilisateur, cliquez sur l’option **[!UICONTROL Rechercher des images similaires]** dans le mode Carte d’une image ou dans la barre d’outils. AEM affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. Voir [Configuration de la recherche par analogie](#configvisualsearch).

![Recherchez des images similaires à l’aide de l’option du de cartes](assets/search_find_similar.png)

*Figure : Recherchez des images similaires à l’aide de l’option du de cartes*

### Images Adobe Stock {#adobestock}

Dans l’interface utilisateur AEM, les utilisateurs peuvent rechercher des [ressources Adobe Stock](/help/assets/aem-assets-adobe-stock.md) et obtenir des licences pour les ressources requises. Ajoutez `Location: Adobe Stock` dans la barre Omni-recherche. Vous pouvez également utiliser le panneau Filtres pour trouver toutes les ressources qui sont ou non sous licence, ou effectuer des recherches dans une ressource spécifique à l’aide du numéro de fichier Adobe Stock.

### Ressources Dynamic Media {#dmassets}

Vous pouvez filtrer les images Dynamic Media en sélectionnant **[!UICONTROL Dynamic Media]** > **[!UICONTROL Visionneuses]** dans le panneau **[!UICONTROL Filtres]**. Il filtre et affiche des ressources telles que des visionneuses d’images, des carrousels, des visionneuses de supports variés et des visionneuses à 360°.

### Recherche de valeurs spécifiques dans les champs de métadonnées {#gqlsearch}

Vous pouvez rechercher des fichiers en fonction des valeurs exactes de champs de métadonnées spécifiques, tels que le titre, la description et l’auteur. La fonction de recherche en texte intégral GQL récupère uniquement les ressources dont la valeur de métadonnées correspond exactement à votre requête. Les noms des propriétés (auteur, titre, etc.) et les valeurs sont sensibles à la casse.

| Champ de métadonnées | Valeur et utilisation des facettes |
|---|---|
| Titre | title:John |
| Créateur | creator:John |
| Emplacement | location:NA |
| Description | description:&quot;Sample Image&quot; |
| Outil créateur | creatortool:&quot;Adobe Photoshop CC 2015&quot; |
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

Les propriétés path, limit, size et orderby ne peuvent pas être combinées à une autre propriété avec un opérateur OU.

Le mot-clé d’une propriété générée par un utilisateur correspond au libellé de son champ dans l’éditeur de propriétés en minuscules et sans espace.

Voici quelques exemples de formats de recherche pour des requêtes complexes :

* Pour afficher toutes les ressources avec plusieurs champs de facettes (par exemple : title=John Doe et creator tool=Adobe Photoshop) :    `tiltle:"John Doe" creatortool : Adobe*`
* Pour afficher toutes les ressources lorsque la valeur de la facette est une expression et non un seul mot (par exemple : le titre est Scott Reynolds) : `title:"Scott Reynolds"`
* Pour afficher les ressources avec plusieurs valeurs d’une seule propriété (le titre est Scott Reynolds ou John Doe, par exemple) : `title:"Scott Reynolds" OR "John Doe"`
* Pour afficher les ressources avec des valeurs de propriété commençant par une chaîne spécifique (par exemple : le titre est Scott Reynolds) : `title:Scott*`
* Pour afficher les ressources avec des valeurs de propriété se terminant par une chaîne spécifique (par exemple : le titre est Scott Reynolds) : `title:*Reynolds`
* Pour afficher les ressources avec une valeur de propriété contenant une chaîne spécifique (par exemple : le titre est Basel Meeting Room) : `title:*Meeting*`
* Pour afficher les ressources qui contiennent une chaîne spécifique et qui possèdent une valeur de propriété en particulier (par exemple : rechercher une chaîne Adobe parmi les ressources dont le titre est John Doe) : `*Adobe* title:"John Doe"`

## Recherche de ressources à partir d’autres offres ou interfaces AEM {#beyondomnisearch}

Adobe Experience Manager (AEM) connecte le référentiel de gestion des ressources numériques à d’autres solutions AEM afin de fournir un accès plus rapide aux ressources numériques et de rationaliser les workflows de création. Toute découverte de ressources commence par la navigation ou la recherche. Le comportement de recherche reste largement le même sur les différentes surfaces et solutions. Certaines méthodes de recherche changent lorsque le public cible, les cas d’utilisation et l’interface utilisateur varient d’une solution AEM à l’autre. Les méthodes spécifiques sont documentées pour les solutions individuelles dans les liens ci-dessous. Les conseils et comportements universellement applicables sont décrits dans cet article.

### Recherche de ressources à partir du panneau Adobe Asset Link {#aal}

Grâce à Adobe Asset Link, les professionnels de la création peuvent désormais accéder au contenu stocké dans AEM Assets, sans quitter les applications Adobe Creative Cloud prises en charge. Ils peuvent parcourir, rechercher, extraire et archiver des ressources de manière transparente à l’aide du panneau intégré à l’application dans les applications Creative Cloud : Photoshop, Illustrator et InDesign. Asset Link permet également aux utilisateurs de rechercher des résultats visuellement similaires. Les résultats d’affichage de la recherche visuelle sont optimisés par les algorithmes d’apprentissage automatique d’Adobe Sensei et aident les utilisateurs à trouver des images à l’esthétique similaire. Voir [Rechercher et parcourir des ressources](https://helpx.adobe.com/fr/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) à l’aide d’Adobe Asset Link.

### Recherche de ressources dans l’application de bureau AEM {#desktopapp}

Les professionnels de la création utilisent l’application de bureau pour rendre les ressources AEM facilement consultables et disponibles sur leur bureau local (Windows ou Mac). Les créatifs peuvent facilement afficher les ressources souhaitées dans le Finder du Mac ou l’Explorateur Windows, ouvertes dans des applications de bureau et modifiées localement ; les modifications sont réenregistrées dans AEM avec une nouvelle version créée dans le référentiel. L’application prend en charge les recherches de base à l’aide d’un ou de plusieurs mots-clés, les caractères génériques * et ? et l’opérateur ET. Voir [Navigation, recherche et prévisualisation des ressources](https://docs.adobe.com/content/help/fr-FR/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) dans l’application de bureau.

### Recherche de ressources dans Brand Portal {#brandportal}

Les utilisateurs métiers et les spécialistes marketing utilisent Brand Portal pour partager efficacement et en toute sécurité les ressources numériques approuvées avec leurs équipes internes étendues, partenaires et revendeurs. Voir [Recherche de ressources sur Brand Portal](https://docs.adobe.com/content/help/fr-FR/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Recherche d’images Adobe Stock {#adobestock-1}

Dans l’interface utilisateur AEM, les utilisateurs peuvent rechercher des ressources Adobe Stock et obtenir des licences pour les ressources requises. Ajoutez `Location: Adobe Stock` dans le champ Omni-recherche. Vous pouvez également utiliser le panneau **[!UICONTROL Filtres]** pour trouver toutes les ressources qui sont ou non sous licence, ou effectuer des recherches dans une ressource spécifique à l’aide du numéro de fichier Adobe Stock. Voir [Gestion des images Adobe Stock dans AEM](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Recherche de ressources Dynamic Media {#dynamicmedia}

Vous pouvez filtrer les images Dynamic Media en sélectionnant **[!UICONTROL Dynamic Media]** > **[!UICONTROL Visionneuses]** dans le panneau **[!UICONTROL Filtres]**. Il filtre et affiche des ressources telles que des visionneuses d’images, des carrousels, des visionneuses de supports variés et des visionneuses à 360°. Lors de la création de pages web, les auteurs peuvent rechercher des visionneuses dans l’outil de recherche de contenu. Un filtre est disponible pour les visionneuses dans un menu contextuel.

### Recherche de ressources dans l’outil de recherche de contenu lors de la création de pages web {#contentfinder}

Les auteurs peuvent utiliser l’outil de recherche de contenu pour rechercher les ressources appropriées dans le référentiel de gestion des ressources numériques et les utiliser dans les pages web qu’ils créent. Les auteurs peuvent également utiliser la fonctionnalité Ressources connectées pour rechercher des ressources disponibles sur un déploiement AEM distant. Les auteurs peuvent alors utiliser ces ressources dans des pages Web sur un déploiement local d’AEM. See [use remote assets](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Recherche de collections {#collections}

La fonctionnalité de recherche AEM prend en charge la recherche de collections et la recherche de ressources dans une collection. Voir [Recherche de collections](/help/assets/managing-collections-touch-ui.md).

## Sélecteur de ressources {#assetselector}

Le sélecteur de ressources vous permet de rechercher, filtrer et parcourir les ressources DAM d’une manière spéciale. Asset Picker is available at `https://[aem-server]:[port]/aem/assetpicker.html`. Vous pouvez récupérer les métadonnées des fichiers que vous sélectionnez à l’aide de cette fonctionnalité. Vous pouvez le lancer avec les paramètres de requête pris en charge, tels que le type de ressource (image, vidéo, texte) et le mode de sélection (sélections simples ou multiples). Ces paramètres définissent le contexte du sélecteur de ressources pour une instance de recherche particulière et restent inchangés tout au long de la sélection.

The asset Picker uses the HTML5 `Window.postMessage` message to send data for the selected asset to the recipient. Le sélecteur de ressources fonctionne uniquement en mode de navigation et ne fonctionne qu’avec la page de résultats d’Omniture.

Vous pouvez transmettre les paramètres de requête suivants dans une URL pour lancer le sélecteur de ressources dans un contexte particulier :

| Nom | Valeurs | Exemple | Objectif |
|---|---|---|---|
| suffixe de la ressource (B) | Chemin d’accès au dossier indiqué comme suffixe de la ressource dans l’URL :[https://localhost:4502/aem/assetpicker.html/&lt;chemin_dossier>](https://localhost:4502/aem/assetpicker.html) | To launch the asset Picker with a particular folder selected, for example with the folder `/content/dam/we-retail/en/activities` selected, the URL should be of the form: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | Si vous avez besoin de sélectionner un dossier en particulier au démarrage du sélecteur de ressources, vous pouvez l’indiquer comme suffixe de ressource. |
| mode | single, multiple | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | En mode multiple, vous pouvez sélectionner plusieurs ressources simultanément à l’aide du sélecteur de ressources. |
| mimetype | Type(s) MIME (`/jcr:content/metadata/dc:format`) d’une ressource (le caractère générique est également pris en charge) | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png)</li></ul> | Utilisez-le pour filtrer les ressources basées sur le(s) type(s) de MIME |
| dialog | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Utilisez ces paramètres pour ouvrir le sélecteur de ressources en tant que boîte de dialogue Granite. Cette option ne peut être appliquée qu’au démarrage du sélecteur de ressources via le champ Chemin de Granite, en la configurant comme URL pickerSrc. |
| assettype (S) | images, documents, multimedia, archives | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | Utilisez cette option pour filtrer les types de ressources en fonction de la valeur indiquée. |
| root | &lt;chemin_dossier> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | Utilisez cette option pour spécifier le dossier racine du sélecteur de ressources. Ici, le sélecteur de ressources ne vous permet de sélectionner qu’une seule ressource enfant (directe/indirecte) sous le dossier racine. |

To access the asset Picker interface, go to `https://[aem_server]:[port]/aem/assetpicker`. Recherchez le dossier souhaité, puis sélectionnez une ou plusieurs ressources. Vous pouvez également rechercher la ressource souhaitée dans la zone Omni-recherche, appliquer un filtre selon vos besoins, puis la sélectionner.

![Parcourir et sélectionner une ressource dans le sélecteur de ressources](assets/assetpicker.png)

*Figure : Parcourir et sélectionner un fichier dans le sélecteur de ressources*

## Restrictions {#limitations}

La fonctionnalité de recherche dans AEM Assets présente les restrictions suivantes :

* N’entrez pas d’espace de début dans la requête, sinon la recherche ne fonctionne pas.
* AEM peut continuer à afficher le terme de recherche une fois que vous avez sélectionné les propriétés d’une ressource à partir des résultats de recherche, puis annuler la recherche. <!-- (CQ-4273540) -->
* Lors de la recherche de dossiers ou de fichiers et de dossiers, les résultats de recherche ne peuvent être triés selon aucun paramètre.
* Si vous appuyez sur Entrée sans taper quoi que ce soit dans la barre Omnisearch, AEM renvoie un de fichiers uniquement et non de dossiers. Si vous recherchez spécifiquement des dossiers sans utiliser de mot-clé, AEM ne renvoie aucun résultat.
* A l’aide de la [!UICONTROL case à cocher Tout] sélectionner, vous pouvez uniquement sélectionner les 100 premiers fichiers recherchés dans les  de carte et les 200 premiers fichiers recherchés dans les  de. Si vous faites défiler et chargez plus de fichiers dans l’interface utilisateur, vous pouvez en sélectionner plus à l’aide de l’option [!UICONTROL Sélectionner tout] .

La recherche visuelle ou par analogie présente les restrictions suivantes :

* La recherche visuelle fonctionne mieux avec les référentiels plus volumineux. Bien qu’il n’y ait pas de nombre minimal d’images requis pour obtenir de bons résultats, la qualité des correspondances avec quelques images peut ne pas être aussi bonne qu’avec un référentiel de taille plus conséquente.
* Vous ne pouvez pas modifier le modèle ni entraîner AEM à rechercher des images similaires. Par exemple, l’ajout ou la suppression de balises intelligentes dans quelques ressources ne modifie pas le modèle. Les ressources sont exclues des résultats de recherche visuellement similaires.

La fonctionnalité de recherche peut présenter des limitations de performances dans les cas suivants :

* Le temps de chargement du de cartes est plus rapide par rapport au pour afficher les résultats de la recherche.

## Conseils de recherche {#tips}

* Si vous surveillez l’état de révision des ressources, utilisez l’option appropriée pour trouver les ressources qui sont approuvées ou en attente d’approbation.
* Utilisez le prédicat Statistiques pour rechercher les ressources prises en charge en fonction de leurs statistiques d’utilisation obtenues auprès de diverses applications Creative. Les données d’utilisation sont regroupées sous Note d’utilisation, Impressions, Clics et Canaux de médias où les ressources apparaissent dans des catégories.
* Cochez la case **[!UICONTROL Sélectionner tout]** pour sélectionner les fichiers recherchés. Il sélectionne les 100 premiers actifs dans les  de carte et les 200 premiers actifs dans les  de . Vous pouvez agir sur la sélection, par exemple, télécharger les fichiers sélectionnés, mettre à jour les propriétés de métadonnées en bloc pour les fichiers sélectionnés ou ajouter les fichiers sélectionnés à une collection.
* Pour rechercher les ressources qui ne contiennent pas les métadonnées obligatoires, voir [Métadonnées obligatoires](#mandatorymetadata).
* La recherche utilise tous les champs de métadonnées. Une recherche générique, telle que la recherche du nombre 12, renvoie généralement de nombreux résultats. Pour de meilleurs résultats, utilisez des guillemets doubles (et non des guillemets simples) ou assurez-vous que le nombre est attaché à un mot sans caractère spécial (par exemple, *chaussure12*).
* La recherche de texte intégral prend en charge des opérateurs tels que -, ^, etc. Pour rechercher des informations sous forme de chaînes littérales, indiquez la phrase de recherche entre guillemets. Par exemple, entrez « Notebook - Beauté » au lieu de Notebook - Beauté.
* Si les résultats de recherche sont trop nombreux, limitez la [portée de la recherche](#scope) pour trouver les ressources souhaitées. Cela fonctionne mieux lorsque vous avez une idée de la meilleure manière de rechercher les ressources que vous recherchez, par exemple un type de fichier, un emplacement ou des métadonnées spécifiques.

* **Balisage** : les balises permettent de classer les ressources pour une navigation et une recherche plus efficaces. Le balisage permet de propager la taxonomie appropriée à d’autres utilisateurs et workflows. AEM propose des méthodes pour baliser automatiquement les ressources à l’aide des services d’intelligence artificielle d’Adobe Sensei, qui améliorent constamment le balisage de vos ressources au fil de l’utilisation et de l’entraînement. Lorsque vous recherchez des ressources, les balises intelligentes sont prises en compte si la fonction est activée sur votre compte. Il fonctionne avec la fonctionnalité de recherche intégrée d’AEM. Voir [Comportement de la recherche](#searchbehavior). Pour optimiser l’ordre d’affichage des résultats de recherche, vous pouvez [améliorer le classement](#searchrank) de quelques ressources sélectionnées.

* **Indexation** : seules les métadonnées et les ressources indexées sont renvoyées dans les résultats de recherche. Pour une meilleure couverture et de meilleures performances, veillez à une indexation appropriée et suivez les bonnes pratiques. Voir [Indexation](#searchindex).

## Quelques exemples illustrant la recherche {#samples}

Utilisez des guillemets doubles autour des mots-clés pour rechercher des ressources contenant exactement l’expression dans l’ordre exact spécifié par l’utilisateur.

![Comportement de recherche avec et sans guillemets](assets/search_with_quotes.gif)

*Figure : Comportement de recherche avec et sans guillemets*

**Recherche avec un caractère générique (astérisque)** : pour élargir la recherche, utilisez un astérisque avant ou après le mot recherché afin de faire correspondre n’importe quel nombre de caractères. Par exemple, la recherche du mot run sans astérisque ne renvoie pas les ressources contenant une variante du mot (y compris dans les métadonnées). L’astérisque remplace n’importe quel nombre de caractères. Par exemple :

* `run` renvoie les ressources contenant exactement le mot-clé « run ».
* `run*` renvoie les ressources concernant « running », « run », « runaway », etc.
* `*run` renvoie « outrun », « rerun », etc.
* `*run*` renvoie toutes les combinaisons possibles.

![Exemple d’utilisation d’un caractère générique (astérisque) dans la recherche de ressources](assets/search_with_asterisk_run.gif)

*Figure : Illustration de l’utilisation d’un caractère générique d’astérisque dans la recherche de ressources à l’aide d’un exemple*

**Recherche avec un caractère générique (point d’interrogation)** : pour élargir la recherche, utilisez un ou plusieurs caractères « ? » pour correspondre au nombre exact de caractères. Par exemple, dans l’illustration suivante :

* la requête `run???` ne correspond à aucune ressource ;

* la requête `run????` correspond au mot `running` avec quatre caractères après `run` ;

* la requête `??run` correspond au mot `rerun` avec deux caractères avant `run`.

![Exemple d’utilisation d’un caractère générique (point d’interrogation) dans la recherche de ressources](assets/search_with_questionmark_run.gif)

*Figure : Illustration de l’utilisation du caractère générique de point d’interrogation dans la recherche de ressources à l’aide d’un exemple*

**Exclusion d’un mot-clé** : utilisez le tiret pour rechercher des ressources qui ne contiennent pas de mot-clé. Par exemple, la requête `running -shoe` renvoie les ressources qui contiennent `running`, mais pas `shoe`. De même, la requête `camp -night` renvoie les ressources qui contiennent `camp`, mais pas `night`. Notez que la requête `camp-night` renvoie les ressources qui contiennent à la fois `camp` et `night`.

![Utilisation du tiret pour rechercher des fichiers ne contenant pas de mot-clé exclu](assets/search_dash_exclude_keyword.gif)

*Figure : Utilisation du tiret pour rechercher des fichiers ne contenant pas de mot-clé exclu*

## de configuration et d’administration lié à la fonctionnalité de recherche {#configadmin}

### Rechercher des configurations d’index {#searchindex}

La découverte des ressources repose sur l’indexation du contenu de la gestion des actifs numériques, y compris des métadonnées. La découverte plus rapide et plus précise des ressources repose sur une indexation optimisée et des configurations appropriées. Reportez-vous à la page Index [de](/help/assets/performance-tuning-guidelines.md#search-indexes)recherche,  de [chêne et indexation](/help/sites-deploying/queries-and-indexing.md), ainsi qu’aux [meilleures pratiques](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Recherche visuelle ou par analogie {#configvisualsearch}

La recherche visuelle utilise le balisage intelligent et requiert AEM 6.5.2.0 ou version ultérieure. Après avoir configuré la fonctionnalité de balisage intelligent, procédez comme suit.

1. Dans AEM CRXDE, dans `/oak:index/lucene` le noeud, ajoutez les propriétés et valeurs suivantes et enregistrez les modifications.

   * `costPerEntry` de type `Double` avec la valeur `10`.

   * `costPerExecution` de type `Double` avec la valeur `2`.

   * `refresh` de type `Boolean` avec la valeur `true`.
   Cette configuration permet d&#39;effectuer des recherches à partir de l&#39;index approprié.

1. Pour créer l’index Lucene, dans CRXDE, à `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, créez un noeud nommé `imageFeatures` de type `nt-unstructured`. Dans `imageFeatures` le noeud,

   * Ajouter `name` propriété de type `String` avec la valeur `jcr:content/metadata/imageFeatures/haystack0`.

   * Ajouter `nodeScopeIndex` propriété de type `Boolean` avec la valeur de `true`.

   * Ajouter `propertyIndex` propriété de type `Boolean` avec la valeur de `true`.

   * Ajouter `useInSimilarity` propriété de type `Boolean` avec la valeur `true`.
   Enregistrez les modifications.

1. Accédez `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` à une propriété de type `similarityTags` et ajoutez-la avec la valeur `Boolean` `true`.
1. Appliquez des balises intelligentes aux ressources de votre référentiel AEM. Voir [comment configurer les balises](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)dynamiques.
1. Dans CRXDE, dans le `/oak-index/damAssetLucene` noeud, définissez la `reindex` propriété sur `true`. Enregistrez les modifications.
1. (Facultatif) Si vous avez personnalisé le formulaire de recherche, copiez le `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` noeud dans `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Enregistrez toutes les modifications.

Pour plus d’informations, reportez-vous à la page [Comprendre les balises actives dans AEM](https://helpx.adobe.com/experience-manager/kt/assets/using/smart-tags-feature-video-understand.html) et [comment gérer les balises](/help/assets/managing-smart-tags.md)actives.

### Métadonnées obligatoires {#mandatorymetadata}

Les utilisateurs professionnels, les administrateurs ou les bibliothécaires DAM peuvent définir certaines métadonnées comme des métadonnées obligatoires indispensables au fonctionnement des processus d’entreprise. Pour diverses raisons, il se peut que certaines ressources manquent de ces métadonnées, comme les ressources héritées ou les ressources migrées en bloc. Les fichiers contenant des métadonnées manquantes ou non valides sont détectés et signalés en fonction de la propriété de métadonnées indexées. Pour le configurer, voir Métadonnées [](/help/assets/metadata-schemas.md#define-mandatory-metadata)obligatoires.

### Modification des facettes de recherche {#searchfacets}

Pour accélérer la découverte, AEM Assets  les facettes de recherche  à l’aide desquelles vous pouvez filtrer les résultats de la recherche. Le panneau  de l’comprend quelques facettes standard par défaut. Les administrateurs peuvent personnaliser le panneau  du pour modifier les facettes par défaut à l’aide des prédicats intégrés. AEM fournit une bonne collection de prédicats intégrés et un éditeur pour personnaliser les facettes. Voir Facettes [de recherche](/help/assets/search-facets.md).

### Extraction de texte lors du téléchargement de fichiers {#extracttextupload}

Vous pouvez configurer AEM pour extraire le texte des ressources lorsque les utilisateurs téléchargent des ressources, telles que des fichiers PSD ou PDF. AEM indexe le texte extrait et aide les utilisateurs à rechercher ces ressources en fonction du texte extrait. See [upload assets](/help/assets/managing-assets-touch-ui.md#uploading-assets).

### Prédicats personnalisés pour filtrer les résultats de la recherche {#custompredicates}

Les prédicats sont utilisés pour créer des facettes. Les administrateurs peuvent personnaliser les facettes de recherche dans le panneau  du à l’aide de prédicats préconfigurés. Ces prédicats peuvent être personnalisés à l’aide d’incrustations. Voir [Création de prédicats](/help/assets/searchx.md)personnalisés.

Vous pouvez rechercher des ressources numériques en fonction d’une ou de plusieurs des propriétés suivantes. Les  qui s’appliquent à certaines de ces propriétés sont disponibles par défaut et d’autres  de peuvent être créées sur mesure pour s’appliquer aux autres propriétés.

| Champ de recherche | Valeurs de propriété de recherche |
|---|---|
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
| Codec audio | Libvorbis, Lame MP3, Codage AAC. La valeur est stockée uniquement dans les métadonnées des rendus vidéo. |
| Débit audio    | Indiqué sous la forme d’une valeur minimale et d’une valeur maximale. La valeur est stockée uniquement dans les métadonnées des rendus vidéo. |

## Utilisation des résultats de recherche de ressources {#aftersearch}

Une fois que vous voyez des ressources recherchées qui correspondent à vos critères, vous pouvez effectuer les tâches standard suivantes avec les résultats de recherche ou entreprendre les actions suivantes :

* Afficher les propriétés de métadonnées et d’autres informations
* Télécharger une ou plusieurs ressources
* Utiliser les actions de bureau pour ouvrir ces ressources dans l’application de bureau
* Créer des collections dynamiques

### Tri des résultats de recherche {#sort}

Le tri des résultats de recherche vous permet de trouver plus rapidement les ressources requises. Le tri des résultats de recherche fonctionne en mode Liste et uniquement lorsque vous sélectionnez **[!UICONTROL [Fichiers](#searchui)]**dans le panneau**[!UICONTROL  Filtres ]**. AEM Assets utilise le tri côté serveur pour trier rapidement toutes les ressources (quel que soit leur nombre) dans un dossier ou les résultats d’une requête. Le tri côté serveur fournit des résultats plus rapides et plus précis que le tri côté client.

En mode Liste, vous pouvez trier les résultats de recherche tout comme vous pouvez trier les ressources de n’importe quel dossier. Le tri fonctionne sur ces colonnes — Nom, Titre, État, Dimensions, Taille, Évaluation, Utilisation, (Date) Créée, (Date) Modifiée, (Date) Publiée, Processus et Extrait.

Pour connaître les restrictions de la fonctionnalité de tri, voir [Restrictions](#limitations).

### Consultation des informations détaillées d’une ressource {#checkinfo}

Vous pouvez consulter les informations détaillées d’une ressource recherchée à partir de la page des résultats de recherche.

Pour afficher toutes les métadonnées d’une ressource, sélectionnez-la, puis cliquez sur **[!UICONTROL Propriétés]** dans la barre d’outils.

Pour consulter les commentaires sur une ressource ou son historique de versions, cliquez sur la ressource afin d’ouvrir l’aperçu de grande taille. Ouvrez la chronologie dans le rail de gauche et sélectionnez **[!UICONTROL Commentaires]** ou **[!UICONTROL Versions]**. Vous pouvez également trier l’activité de la chronologie comme les commentaires ou les versions dans un ordre chronologique.

![Tri des entrées de chronologie d’une ressource recherchée](assets/sort_timeline_search_results.gif)

*Figure : Tri des entrées de chronologie d’un fichier de recherche*

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
| Résultats incorrects lors de la recherche de fichiers avec des métadonnées manquantes | Lors de la recherche de fichiers qui ne contiennent pas les métadonnées obligatoires, AEM peut afficher certains fichiers qui possèdent des métadonnées valides. Les résultats sont basés sur la propriété de métadonnées indexées. | Une fois les métadonnées mises à jour, la réindexation est nécessaire pour refléter l’état correct des métadonnées des fichiers. Voir [Métadonnées obligatoires](metadata-schemas.md#define-mandatory-metadata). |
| Trop de résultats de recherche | Paramètre de recherche large. | Envisagez de limiter la [portée de la recherche](#scope). L’utilisation de balises intelligentes peut vous donner plus de résultats de recherche que prévu. Reportez-vous à la page Comportement [de la recherche avec les balises](#withsmarttags)actives. |
| Résultats de recherche non liés ou partiellement liés | Le comportement de recherche change avec le balisage intelligent. | Comprenez [comment la recherche change après un balisage](#withsmarttags)intelligent. |
| Aucune suggestion de saisie semi-automatique pour les ressources | Les fichiers nouvellement téléchargés ne sont pas encore indexés. Les métadonnées ne sont pas immédiatement disponibles en tant que suggestions lorsque vous à taper un mot-clé de recherche dans la barre d&#39;Omniture. | AEM Assets attend jusqu’à l’expiration d’un délai d’attente (par défaut, une heure) avant d’effectuer une tâche en arrière-plan afin d’indexer les métadonnées pour toutes les ressources chargées/mises à jour dernièrement et de les ajouter à la liste de suggestions. |
| Aucun résultat de recherche | <ul><li>Il n’existe aucune ressource correspondant à votre requête.</li><li>Vous avez ajouté un espace blanc avant le  de recherche.</li><li>Un champ de métadonnées non pris en charge contient le mot-clé que vous recherchez.</li><li>L’heure d’activation et de désactivation est configurée pour la ressource et la recherche a été effectuée pendant l’heure de désactivation de la ressource.</li></ul> | <ul><li>Effectuez une recherche à l’aide d’un autre mot-clé. Vous pouvez également utiliser le balisage (intelligent) pour améliorer les résultats de la recherche.</li><li>C’est une [limitation connue](#limitations).</li><li>Les champs de métadonnées ne sont pas tous pris en compte pour les recherches. Voir [Portée](#scope).</li><li>Recherchez les ressources requises ultérieurement ou modifiez leur heure d’activation et de désactivation.</li></ul> |
| Le filtre/prédicat de recherche n&#39;est pas disponible | <ul><li>Le filtre de recherche n&#39;est pas configuré.</li><li>Il n’est pas disponible pour votre connexion.</li><li>(Moins probable) Les options de recherche ne sont pas personnalisées sur le déploiement que vous utilisez.</li></ul> | <ul><li>Contactez l’administrateur pour vérifier si les personnalisations de recherche sont disponibles ou non.</li><li>Contactez l’administrateur pour vérifier si votre compte dispose des droits/autorisations nécessaires pour utiliser la personnalisation.</li><li>Contactez l’administrateur et vérifiez les personnalisations disponibles pour le déploiement d’AEM Assets que vous utilisez.</li></ul> |
| Lors de la recherche d’images visuellement similaires, il manque une image attendue. | <ul><li>Image non disponible dans AEM.</li><li>L’image n’est pas indexée. Généralement, lorsqu’il est récemment téléchargé.</li><li>L’image n’est pas balisée de manière intelligente.</li></ul> | <ul><li>Ajouter l’image aux ressources AEM.</li><li>Contactez votre administrateur pour réindexer le référentiel. Veillez également à utiliser l’index approprié.</li><li>Contactez votre administrateur pour baliser intelligemment les ressources appropriées.</li></ul> |
| Lors de la recherche d’images visuellement similaires, une image non pertinente s’affiche. | Comportement de recherche visuelle. | AEM affiche autant de ressources potentiellement pertinentes que possible. Les images moins pertinentes, le cas échéant, sont ajoutées aux résultats, mais avec un classement inférieur dans les résultats de recherche. La qualité des correspondances et la pertinence des ressources recherchées diminuent à mesure que vous descendez dans les résultats de la recherche. |
| Lors de la sélection et du fonctionnement des résultats de la recherche, toutes les ressources recherchées ne sont pas exploitées. | L’option [!UICONTROL Sélectionner tout] sélectionne uniquement les 100 premiers résultats de recherche dans le  de carte et les 200 premiers résultats de recherche dans le  de. |  |

>[!MORELIKETHIS]
>
>* [Guide de mise en oeuvre des recherches AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Configuration avancée des prédicats de recherche de plusieurs valeurs et de balises](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/search-feature-video-use.html)
>* [Configuration de la recherche de traduction dynamique](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

