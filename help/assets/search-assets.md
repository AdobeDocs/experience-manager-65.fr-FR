---
title: Recherche d’images et de ressources numériques dans [!DNL Adobe Experience Manager]
description: Découvrez comment rechercher les ressources souhaitées dans  [!DNL Adobe Experience Manager] à l’aide du panneau Filtres et comment utiliser les ressources affichées dans la recherche.
contentOwner: AG
mini-toc-levels: 1
feature: Search, Metadata
role: Business Practitioner
translation-type: tm+mt
source-git-commit: fd283b840830bef613689f81cf753e226fb834d7
workflow-type: tm+mt
source-wordcount: '5577'
ht-degree: 76%

---


# Recherche de ressources dans [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] fournit des méthodes robustes de découverte de ressources qui vous aident à atteindre une vitesse de contenu plus élevée. Vos équipes peuvent réduire les délais de mise sur le marché grâce à une expérience de recherche intelligente et transparente, aux fonctionnalités prêtes à l’emploi et aux méthodes personnalisées. La recherche de ressources est essentielle pour l’utilisation d’un système de gestion des ressources numériques, que ce soit pour une utilisation plus poussée par les créatifs, pour une gestion robuste des ressources par les utilisateurs et spécialistes marketing ou pour l’administration par les administrateurs DAM. Les recherches simples, avancées et personnalisées que vous pouvez effectuer via l’interface utilisateur [!DNL Assets] ou d’autres applications et surfaces permettent de répondre à ces cas d’utilisation.

[!DNL Experience Manager Assets] prend en charge les cas d’utilisation suivants dont cet article décrit l’utilisation, les concepts, les configurations, les limitations et le dépannage.

| Recherche de ressources | Configurer et administrer la fonctionnalité de recherche | Utilisation des résultats de recherche |
|---|---|---|
| [Recherches de base](#searchbasics) | [Index de recherche](#searchindex) | [Tri des résultats](#sort) |
| [Présentation de l’interface utilisateur de recherche](#searchui) | [Recherche visuelle ou par analogie](#configvisualsearch) | [Vérification des propriétés et des métadonnées d’une ressource](#checkinfo) |
| [Suggestions de recherche](#searchsuggestions) | [Métadonnées obligatoires](#mandatorymetadata) | [Téléchargement](#download) |
| [Présentation des résultats de recherche et du comportement](#searchbehavior) | [Modification des facettes de recherche](#searchfacets) | [Mises à jour des métadonnées en masse](#metadataupdates) |
| [Classement et amplification des recherches](#searchrank) | [Extraction de texte](#extracttextupload) | [Collections dynamiques](#collections) |
| [Recherche avancée : filtrage et portée de la recherche](#scope) | [Prédicats personnalisés](#custompredicates) | [Explication et résolution des problèmes liés aux résultats inattendus](#unexpected-results) |
| [Recherche à partir d’autres solutions et applications](#search-assets-other-surfaces) :<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[Application de bureau Experience Manager](#desktop-app)</li><li>[Images Adobe Stock](#adobe-stock)</li><li>[Ressources Dynamic Media](#dynamic-media)</li></ul> |  |  |
| [Sélecteur de ressources](#assetpicker) |  |  |
| [Limites](#limitations) et [conseils](#tips) |  |  |
| [Exemples illustrés](#samples) |  |  |

Recherchez des ressources à l’aide du champ Omni-recherche situé en haut de l’interface web [!DNL Experience Manager]. Accédez à **[!UICONTROL Ressources]** > **[!UICONTROL Fichiers]** dans [!DNL Experience Manager], cliquez sur ![icône_recherche](assets/do-not-localize/search_icon.png) dans la barre supérieure, entrez le mot-clé de recherche et sélectionnez `Return`. Vous pouvez également utiliser le raccourci `/` (barre oblique) pour ouvrir le champ Omni-recherche. `Location:Assets` est présélectionné afin de limiter les recherches aux ressources de la gestion des ressources numériques. [!DNL Experience Manager] fournit des suggestions lorsque vous commencez à saisir un mot-clé de recherche.

Utilisez le panneau **[!UICONTROL Filtres]** pour rechercher des ressources, des dossiers, des balises et des métadonnées. Vous pouvez filtrer les résultats de recherche en fonction des différentes options (prédicats), telles que le type et la taille de fichier, la date de dernière modification, l’état de la ressource, les données de renseignement et les licences Adobe Stock. Vous pouvez personnaliser le panneau Filtres et ajouter ou supprimer des prédicats de recherche à l’aide des [facettes de recherche](/help/assets/search-facets.md). Le filtre [!UICONTROL Type de fichier] du panneau [!UICONTROL Filtres] comporte des cases à cocher à états mixtes. Les cases à cocher du premier niveau sont donc partiellement cochées à moins que vous ne sélectionniez tous les prédicats (ou formats) imbriqués.

La fonctionnalité de recherche [!DNL Experience Manager] prend en charge la recherche de collections et la recherche de ressources dans une collection. Voir [Recherche de collections](/help/assets/manage-collections.md).

## Présentation de l’interface de recherche {#searchui}

Familiarisez-vous avec l’interface de recherche et les actions disponibles.

![Présentation de l’interface des résultats de recherche des ressources Experience Manager](assets/aem_search_results.png)

*Figure : Présentation de l’interface des résultats de recherche [!DNL Experience Manager Assets].*

**A.** Enregistrer la recherche en tant que collection dynamique. **B.** Filtres ou prédicats pour limiter les résultats de recherche. **C.** Afficher les fichiers, les dossiers ou les deux. **D.** Cliquer sur Filtres pour ouvrir ou fermer le rail de gauche. **E.** L’emplacement de recherche est la gestion des ressources numériques. **F.** Champ Omni-recherche avec mot-clé de recherche fourni par l’utilisateur. **G.** Sélectionner les résultats de recherche chargés. **H.** Nombre de résultats de recherche affichés par rapport au nombre total de résultats de recherche. **I.** Fermer la recherche. **J.** Basculer entre le mode carte et le mode liste.

### Facettes de recherche dynamique {#dynamicfacets}

Vous pouvez découvrir plus rapidement les ressources de votre choix à partir de la page des résultats de recherche en utilisant le nombre de résultats de recherche attendus mis à jour dynamiquement dans les facettes de recherche. Le nombre prévu de ressources est mis à jour avant même d’appliquer le filtre de recherche. L’affichage du nombre prévu par rapport au filtre vous aide à parcourir rapidement et efficacement les résultats de la recherche.

![Affichage du nombre approximatif de ressources sans filtrer les résultats de la recherche dans les facettes de recherche.](assets/asset_search_results_in_facets_filters.png)

*Figure : Affichage du nombre approximatif de ressources sans filtrer les résultats de la recherche dans les facettes de recherche.*

## Présentation des résultats de recherche et du comportement {#searchbehavior}

### Termes et résultats de recherche de base {#searchbasics}

Vous pouvez exécuter des recherches de mots-clés à partir du champ Omni-recherche. La recherche de mots-clés n’est pas sensible à la casse et il s’agit d’une recherche en texte intégral (dans les champs de métadonnées courants). Si plusieurs mots-clés sont utilisés, `AND` est l’opérateur par défaut entre les mots-clés.

Les résultats sont triés par pertinence, en commençant par les correspondances les plus proches. Pour plusieurs mots-clés, les ressources qui contiennent les deux termes dans leurs métadonnées génèrent des résultats plus pertinents. Dans les métadonnées, les mots-clés qui apparaissent sous forme de balises intelligentes sont classés plus haut que les mots-clés qui apparaissent dans d’autres champs de métadonnées. [!DNL Experience Manager] permet de donner plus de poids à un terme de recherche particulier. Il est également possible d’[améliorer le classement](#searchrank) de quelques ressources ciblées pour des termes de recherche spécifiques.

Pour rechercher rapidement les ressources appropriées, l’interface riche fournit des mécanismes de filtrage, de tri et de sélection. Vous pouvez filtrer les résultats selon plusieurs critères et afficher le nombre de ressources recherchées pour différents filtres. Vous pouvez également réexécuter la recherche en modifiant la requête dans le champ Omni-recherche. Lorsque vous modifiez les termes ou filtres de recherche, les autres filtres restent appliqués pour préserver le contexte de la recherche.

Lorsque les résultats sont de nombreuses ressources, [!DNL Experience Manager] affiche les 100 premiers en mode carte et les 200 premiers en mode liste. Des ressources supplémentaires sont chargées lorsque l’utilisateur fait défiler le contenu. Il s’agit d’améliorer les performances. Regardez une démonstration vidéo du [nombre de ressources affichées](https://www.youtube.com/watch?v=LcrGPDLDf4o).

Il arrive que des ressources inattendues apparaissent dans les résultats de la recherche. Pour plus d’informations, voir [Résultats inattendus](#unexpected-results).

[!DNL Experience Manager] peut effectuer des recherches dans de nombreux formats de fichiers et les filtres de recherche peuvent être personnalisés en fonction des besoins de votre entreprise. Contactez votre administrateur pour connaître les options de recherche disponibles pour votre référentiel DAM et les restrictions de votre compte.

### Résultats avec et sans balises actives améliorées {#withsmarttags}

Par défaut, la recherche [!DNL Experience Manager] combine les termes recherchés avec une clause ET. Par exemple, pensez à rechercher les mots-clés femme en cours d’exécution. Par défaut, seuls les fichiers contenant à la fois des mots-clés féminins et en cours d’exécution dans les métadonnées apparaissent dans les résultats de recherche. Le même comportement est conservé lorsque des caractères spéciaux (points, traits de soulignement ou tirets) sont utilisés avec les mots-clés. Les requêtes de recherche suivantes renvoient les mêmes résultats :

* `woman running`
* `woman.running`
* `woman-running`

Cependant, la requête `woman -running` renvoie des fichiers sans `running` dans leurs métadonnées.
L’utilisation de balises actives ajoute une clause `OR` supplémentaire pour rechercher les termes de recherche en tant que balises actives appliquées. Une ressource balisée avec `woman` ou `running` à l’aide de balises actives apparaît également dans cette requête de recherche. Les résultats de la recherche sont donc une combinaison de :

* Actifs contenant des mots-clés `woman` et `running` dans les métadonnées (comportement par défaut).

* Actifs balisés avec l’un des mots-clés (comportement Balises dynamiques).

### Suggestions de recherche en cours de frappe {#searchsuggestions}

Lorsque vous début de saisir des mots-clés, [!DNL Experience Manager] suggère les mots-clés ou expressions de recherche possibles. Les suggestions sont basées sur les métadonnées des ressources existantes. [!DNL Experience Manager] indexe tous les champs de métadonnées pour faciliter la recherche. Pour fournir des suggestions de recherche, le système utilise les valeurs des quelques champs de métadonnées suivants. Pour fournir des suggestions de recherche, pensez à renseigner les champs suivants avec les mots-clés appropriés :

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

1. Dans l’interface utilisateur [!DNL Assets], ouvrez la page des propriétés de la ressource. Cliquez sur **[!UICONTROL Avancé]** et cliquez sur **[!UICONTROL Ajouter]** sous **[!UICONTROL Élever pour les mots-clés de recherche]**.
1. Dans la boîte de dialogue **[!UICONTROL Rechercher une promotion]**, indiquez un mot-clé pour lequel vous souhaitez améliorer la recherche d’image, puis cliquez sur **[!UICONTROL Ajouter]**. Vous pouvez indiquer plusieurs mots-clés de la même manière.
1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**. La ressource pour laquelle vous avez promu ce mot-clé apparaît en tête des résultats de recherche.

Vous pouvez l’utiliser à votre avantage en améliorant le classement de certaines ressources dans les résultats de recherche du mot-clé ciblé. Voir la vidéo d’exemple ci-dessous. Pour plus d’informations, voir [Recherche dans [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html?lang=fr).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Vidéo : Découvrez comment les résultats de recherche sont classés et comment le classement peut être influencé.*

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

### Images Adobe Stock {#adobe-stock}

Dans l&#39;interface utilisateur [!DNL Experience Manager], les utilisateurs peuvent rechercher [des ressources Adobe Stock](/help/assets/aem-assets-adobe-stock.md) et activer la licence des ressources requises. Ajoutez `Location: Adobe Stock` dans la barre Omni-recherche. Vous pouvez également utiliser le panneau Filtres pour trouver toutes les ressources qui sont ou non sous licence, ou effectuer des recherches dans une ressource spécifique à l’aide du numéro de fichier Adobe Stock.

### Ressources Dynamic Media {#dmassets}

Vous pouvez filtrer les images Dynamic Media en sélectionnant **[!UICONTROL Dynamic Media]** > **[!UICONTROL Visionneuses]** dans le panneau **[!UICONTROL Filtres]**. Il filtre et affiche des ressources telles que des visionneuses d’images, des carrousels, des visionneuses de supports variés et des visionneuses à 360°.

### Recherche GQL à l’aide de valeurs spécifiques dans les champs de métadonnées {#gql-search}

Vous pouvez rechercher des fichiers en fonction des valeurs exactes des champs de métadonnées, tels que le titre, la description et le créateur. La fonction de recherche en texte intégral GQL récupère uniquement les ressources dont la valeur de métadonnées correspond exactement à votre requête. Les noms des propriétés (Créateur, Titre, etc.) et des valeurs sont sensibles à la casse.

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
| Largeur de l’image | width:lowerboundsupérieur |
| Hauteur de l’image | height:lowerboundsupérieur |
| Personne | person:John |

Les propriétés `path`, `limit`, `size` et `orderby` ne peuvent pas être combinées à l&#39;aide de l&#39;opérateur `OR` avec une autre propriété.

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

Le mot-clé d’une propriété générée par un utilisateur correspond au libellé de son champ dans l’éditeur de propriétés en minuscules et sans espace.

Voici quelques exemples de formats de recherche pour des requêtes complexes :

* Pour afficher toutes les ressources avec plusieurs champs de facettes (par exemple : title=John Doe et creator tool=Adobe Photoshop) : `title:"John Doe" creatortool:Adobe*`
* Pour afficher toutes les ressources lorsque la valeur de la facette est une expression et non un seul mot (par exemple : le titre est Scott Reynolds) : `title:"Scott Reynolds"`
* Pour afficher les ressources avec plusieurs valeurs d’une seule propriété (le titre est Scott Reynolds ou John Doe, par exemple) : `title:"Scott Reynolds" OR "John Doe"`
* Pour afficher les ressources avec des valeurs de propriété commençant par une chaîne spécifique (par exemple : le titre est Scott Reynolds) : `title:Scott*`
* Pour afficher les ressources avec des valeurs de propriété se terminant par une chaîne spécifique (par exemple : le titre est Scott Reynolds) : `title:*Reynolds`
* Pour afficher les ressources avec une valeur de propriété contenant une chaîne spécifique (par exemple : le titre est Basel Meeting Room) : `title:*Meeting*`
* Pour afficher les ressources qui contiennent une chaîne spécifique et qui possèdent une valeur de propriété en particulier (par exemple : rechercher une chaîne Adobe parmi les ressources dont le titre est John Doe) : `*Adobe* title:"John Doe"`

## Rechercher des ressources provenant d&#39;autres offres ou interfaces [!DNL Experience Manager] {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager] connecte le référentiel DAM à diverses autres  [!DNL Experience Manager] solutions afin de fournir un accès plus rapide aux ressources numériques et de rationaliser les workflows de création. Toute découverte de ressources commence par la navigation ou la recherche. Le comportement de recherche reste largement le même sur les différentes surfaces et solutions. Certaines méthodes de recherche changent à mesure que l&#39;audience des cibles, les cas d&#39;utilisation et l&#39;interface utilisateur varient selon les solutions [!DNL Experience Manager]. Les méthodes spécifiques sont documentées pour les solutions individuelles dans les liens ci-dessous. Les conseils et comportements universellement applicables sont décrits dans cet article.

### Recherche de ressources à partir du panneau Adobe Asset Link {#aal}

Grâce à Adobe Asset Link, les professionnels de la création peuvent désormais accéder au contenu stocké dans [!DNL Experience Manager Assets], sans quitter les applications Adobe Creative Cloud prises en charge. Les créatifs peuvent parcourir, rechercher, extraire et archiver facilement des ressources à l’aide du panneau intégré des applications [!DNL Adobe Creative Cloud] : [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] et [!DNL Adobe InDesign]. Asset Link permet également aux utilisateurs de rechercher des résultats visuellement similaires. Les résultats d’affichage de la recherche visuelle sont optimisés par les algorithmes d’apprentissage automatique d’Adobe Sensei et aident les utilisateurs à trouver des images à l’esthétique similaire. Voir [Rechercher et parcourir des ressources](https://helpx.adobe.com/fr/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) à l’aide d’Adobe Asset Link.

### Rechercher des ressources dans l&#39;application de bureau [!DNL Experience Manager] {#desktop-app}

Les professionnels de la création utilisent l&#39;application de bureau pour rendre les [!DNL Experience Manager Assets] facilement consultables et disponibles sur leur bureau local (Windows ou Mac). Les créatifs peuvent facilement révéler les ressources souhaitées dans Mac Finder ou Windows Explorer, ouverts dans les applications de bureau et modifiés localement - les modifications sont enregistrées à [!DNL Experience Manager] avec une nouvelle version créée dans le référentiel. L&#39;application prend en charge les recherches de base en utilisant un ou plusieurs mots-clés, des caractères génériques `*` et `?` et l&#39;opérateur `AND`. Voir [Navigation, recherche et prévisualisation des ressources](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr#browse-search-preview-assets) dans l’application de bureau.

### Recherche de ressources dans [!DNL Brand Portal] {#brand-portal}

Les utilisateurs métiers et les spécialistes marketing utilisent Brand Portal pour partager efficacement et en toute sécurité les ressources numériques approuvées avec leurs équipes internes étendues, partenaires et revendeurs. Voir [Recherche de ressources sur Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html?lang=fr).

### Rechercher [!DNL Adobe Stock] images {#adobe-stock1}

Dans l’interface utilisateur [!DNL Experience Manager], les utilisateurs peuvent rechercher des ressources Adobe Stock et activer la licence des ressources requises. Ajoutez `Location: Adobe Stock` dans le champ Omni-recherche. Vous pouvez également utiliser le panneau **[!UICONTROL Filtres]** pour trouver toutes les ressources qui sont ou non sous licence, ou effectuer des recherches dans une ressource spécifique à l’aide du numéro de fichier Adobe Stock. Voir [gérer [!DNL Adobe Stock] les images dans [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Rechercher [!DNL Dynamic Media] ressources {#dynamic-media}

Vous pouvez filtrer les images Dynamic Media en sélectionnant **[!UICONTROL Dynamic Media]** > **[!UICONTROL Visionneuses]** dans le panneau **[!UICONTROL Filtres]**. Il filtre et affiche des ressources telles que des visionneuses d’images, des carrousels, des visionneuses de supports variés et des visionneuses à 360°. Lors de la création de pages web, les auteurs peuvent rechercher des visionneuses dans l’outil de recherche de contenu. Un filtre est disponible pour les visionneuses dans un menu contextuel.

### Recherche de ressources dans l’outil de recherche de contenu lors de la création de pages web {#content-finder}

Les auteurs peuvent utiliser l’outil de recherche de contenu pour rechercher les ressources appropriées dans le référentiel de gestion des ressources numériques et les utiliser dans les pages web qu’ils créent. Les auteurs peuvent également utiliser la fonctionnalité Ressources connectées pour rechercher des ressources disponibles dans un déploiement distant [!DNL Experience Manager]. Les auteurs peuvent ensuite utiliser ces ressources dans des pages Web lors d’un déploiement local [!DNL Experience Manager]. Voir [utiliser des ressources distantes](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Recherche de collections {#collections}

La fonctionnalité de recherche [!DNL Experience Manager] prend en charge la recherche de collections et la recherche de ressources dans une collection. Voir [Recherche de collections](/help/assets/manage-collections.md).

## Sélecteur de ressources {#asset-picker}

>[!NOTE]
>
>Le sélecteur de ressources a été appelé [sélecteur de ressources](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) dans les versions antérieures de [!DNL Adobe Experience Manager].

Le sélecteur de ressources vous permet de rechercher, de filtrer et de parcourir les ressources de la gestion des ressources numériques de façon spéciale. Le sélecteur de ressources est disponible à l’adresse `https://[aem_server]:[port]/aem/assetpicker.html`. Vous pouvez récupérer les métadonnées des ressources sélectionnées à l’aide du sélecteur de ressources. Vous pouvez le lancer avec les paramètres de requête pris en charge, tels que le type de ressource (image, vidéo, texte) et le mode de sélection (sélections simples ou multiples). Ces paramètres définissent le contexte du sélecteur de ressources pour une instance de recherche particulière et restent inchangés tout au long de la sélection.

Le sélecteur de ressources utilise le message HTML5 `Window.postMessage` pour envoyer au destinataire les données correspondant à la ressource sélectionnée. Il fonctionne uniquement en mode Parcourir et uniquement avec la page de résultats d&#39;Omnisearch.

Transférez les paramètres de requête suivants dans une URL pour lancer le sélecteur de ressources dans un contexte particulier :

| Nom | Valeurs | Exemple | Objectif |
|---|---|---|---|
| suffixe de la ressource (B) | Chemin d’accès au dossier indiqué comme suffixe de la ressource dans l’URL : [https://localhost:4502/aem/assetpicker.html/&lt;chemin_dossier>](https://localhost:4502/aem/assetpicker.html) | Pour lancer le sélecteur de ressources avec un dossier particulier sélectionné, par exemple avec le dossier `/content/dam/we-retail/en/activities` sélectionné, l’URL doit se présenter comme suit : `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | Si vous avez besoin de sélectionner un dossier en particulier au démarrage du sélecteur de ressources, vous pouvez l’indiquer comme suffixe de ressource. |
| `mode` | single, multiple | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | En mode multiple, vous pouvez sélectionner plusieurs ressources simultanément à l’aide du sélecteur de ressources. |
| `dialog` | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Utilisez ces paramètres pour ouvrir le sélecteur de ressources en tant que boîte de dialogue Granite. Cette option ne peut être appliquée qu’au démarrage du sélecteur de ressources via le champ Chemin de Granite, en la configurant comme URL pickerSrc. |
| `root` | &lt;chemin_dossier> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | Utilisez cette option pour spécifier le dossier racine du sélecteur de ressources. Ici, le sélecteur de ressources ne vous permet de sélectionner qu’une seule ressource enfant (directe/indirecte) sous le dossier racine. |
| `viewmode` | de recherches |  | Pour lancer le sélecteur de ressources en mode de recherche, avec les paramètres `assettype` et `mimetype`. |
| `assettype` | Images, documents, multimédia, archives. | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | Utilisez l’option pour filtrer les types de fichier en fonction de la valeur fournie. |
| `mimetype` | Type MIME (`/jcr:content/metadata/dc:format`) d’une ressource (caractère générique également pris en charge). | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | Utilisez-la pour filtrer les fichiers en fonction du type MIME. |

Pour accéder à l’interface du sélecteur de ressources, accédez à `https://[aem_server]:[port]/aem/assetpicker`. Recherchez le dossier souhaité, puis sélectionnez une ou plusieurs ressources. Vous pouvez également rechercher la ressource souhaitée dans la zone Omni-recherche, appliquer un filtre selon vos besoins, puis la sélectionner.

![Parcourir et sélectionner un fichier dans le sélecteur de fichiers](assets/assetpicker.png)

*Figure : Recherchez et sélectionnez un fichier dans le sélecteur de ressources.*

## Restrictions {#limitations}

La fonctionnalité de recherche dans [!DNL Experience Manager Assets] présente les restrictions suivantes :

* N’entrez pas d’espace de début dans la requête, sinon la recherche ne fonctionne pas.
* [!DNL Experience Manager] peut continuer à afficher le terme de recherche une fois que vous avez sélectionné les propriétés d’une ressource à partir des résultats de recherche, puis annuler la recherche. <!-- (CQ-4273540) -->
* Lors de la recherche de dossiers ou de fichiers et de dossiers, les résultats de recherche ne peuvent être triés selon aucun paramètre.
* Si vous sélectionnez `Return` sans rien taper dans la barre Omni-recherche, [!DNL Experience Manager] renvoie une liste contenant uniquement des fichiers et non des dossiers. Si vous recherchez spécifiquement des dossiers sans utiliser de mot-clé, [!DNL Experience Manager] ne renvoie aucun résultat.
* Vous pouvez effectuer une recherche de texte intégral sur des dossiers. Spécifiez un terme de recherche pour que la recherche fonctionne.

La recherche visuelle ou par analogie présente les restrictions suivantes :

* La recherche visuelle fonctionne mieux avec un grand référentiel. Bien qu’il n’y ait pas de nombre minimal d’images requis pour obtenir de bons résultats, la qualité des correspondances avec quelques images n’est pas aussi bonne que les correspondances d’un grand référentiel.
* Vous ne pouvez pas modifier le modèle ni entraîner [!DNL Experience Manager] à rechercher des images similaires. Par exemple, l’ajout ou la suppression de balises intelligentes dans quelques ressources ne modifie pas le modèle. Les ressources sont exclues des résultats de recherche visuellement similaires.

La fonctionnalité de recherche peut présenter des limitations de performances dans les cas suivants :

* Le chargement pour l’affichage des résultats de la recherche est plus rapide en mode carte qu’en mode liste.

## Conseils de recherche {#tips}

* Si vous surveillez l’état de révision des ressources, utilisez l’option appropriée pour trouver les ressources qui sont approuvées ou en attente d’approbation.
* Utilisez le prédicat Statistiques pour rechercher les ressources prises en charge en fonction de leurs statistiques d’utilisation obtenues auprès de diverses applications Creative. Les données d’utilisation sont regroupées sous Note d’utilisation, Impressions, Clics et Canaux de médias où les ressources apparaissent dans des catégories.
* Cochez la case **[!UICONTROL Sélectionner tout]** pour sélectionner les ressources recherchées. [!DNL Experience Manager] affiche initialement 100 ressources en mode carte et 200 ressources en mode liste. Des ressources supplémentaires sont chargées lorsque vous faites défiler les résultats de la recherche. Vous pouvez sélectionner plus de ressources que les ressources chargées. Le nombre de ressources sélectionnées est affiché dans l’angle supérieur droit de la page des résultats de la recherche. Vous pouvez agir sur la sélection, par exemple télécharger les ressources sélectionnées, mettre à jour des propriétés de métadonnées en bloc pour les ressources sélectionnées ou ajouter les ressources sélectionnées à une collection. Lorsqu’il y a moins de ressources affichées que de ressources sélectionnées, une action est appliquée à toutes les ressources sélectionnées ou une boîte de dialogue affiche le nombre de ressources auxquelles elle est appliquée. Pour appliquer une action aux ressources qui n’ont pas été chargées, veillez à ce que toutes les ressources soient sélectionnées explicitement.
* Pour rechercher les ressources qui ne contiennent pas les métadonnées obligatoires, voir [Métadonnées obligatoires](#mandatorymetadata).
* La recherche utilise tous les champs de métadonnées. Une recherche générique, telle que la recherche du nombre 12, renvoie généralement de nombreux résultats. Pour de meilleurs résultats, utilisez des guillemets doubles (et non des guillemets simples) ou assurez-vous que le nombre est attaché à un mot sans caractère spécial (par exemple, `shoe12`).
* La recherche en texte intégral prend en charge les opérateurs tels que `-` et `^`. Pour rechercher des informations sous forme de chaînes littérales, indiquez la phrase de recherche entre guillemets. Par exemple, utilisez `"Notebook - Beauty"` au lieu de `Notebook - Beauty`.
* Si les résultats de recherche sont trop nombreux, limitez la [portée de la recherche](#scope) pour trouver les ressources souhaitées. Cela fonctionne mieux lorsque vous avez une idée de la meilleure manière de rechercher les ressources que vous recherchez, par exemple un type de fichier, un emplacement ou des métadonnées spécifiques.

* **Balisage** : les balises permettent de classer les ressources pour une navigation et une recherche plus efficaces. Le balisage permet de propager la taxonomie appropriée à d’autres utilisateurs et workflows. [!DNL Experience Manager] propose des méthodes pour baliser automatiquement les ressources à l’aide des services d’intelligence artificielle d’Adobe Sensei, qui améliorent constamment le balisage de vos ressources au fil de l’utilisation et de l’entraînement. Lorsque vous recherchez des ressources, les balises intelligentes sont prises en compte si la fonction est activée sur votre compte. Cela fonctionne avec la fonctionnalité de recherche intégrée. Voir [Comportement de la recherche](#searchbehavior). Pour optimiser l’ordre d’affichage des résultats de recherche, vous pouvez [améliorer le classement](#searchrank) de quelques ressources sélectionnées.

* **Indexation** : seules les métadonnées et les ressources indexées sont renvoyées dans les résultats de recherche. Pour une meilleure couverture et de meilleures performances, veillez à une indexation appropriée et suivez les bonnes pratiques. Voir [Indexation](#searchindex).

* Pour exclure des ressources spécifiques des résultats de la recherche, utilisez la propriété `excludedPath` dans l&#39;index Lucene.

## Quelques exemples illustrant la recherche {#samples}

Utilisez des guillemets doubles autour des mots-clés pour rechercher des ressources contenant exactement l’expression dans l’ordre exact spécifié par l’utilisateur.

![Comportement de recherche avec et sans guillemets](assets/search_with_quotes.gif)

*Figure : Comportement de recherche avec et sans guillemets.*

**Recherche avec un caractère générique (astérisque)** : pour élargir la recherche, utilisez un astérisque avant ou après le mot recherché afin de faire correspondre n’importe quel nombre de caractères. Par exemple, la recherche du mot run sans astérisque ne renvoie pas les ressources contenant une variante du mot (y compris dans les métadonnées). L’astérisque remplace n’importe quel nombre de caractères. Par exemple,

* `run` renvoie les ressources contenant exactement le mot-clé « run ».
* `run*` renvoie des ressources avec  `running`,  `run`,  `runaway`, etc.
* `*run` renvoie des ressources avec  `outrun`,  `rerun`, etc.
* `*run*` renvoie toutes les combinaisons possibles.

![Illustration de l’utilisation d’un caractère générique d’astérisque dans la recherche de ressources à l’aide d’un exemple](assets/search_with_asterisk_run.gif)

*Figure : Exemple d’utilisation d’un caractère générique (astérisque) dans la recherche de ressources.*

**Recherche avec un caractère générique (point d’interrogation)** : pour élargir la recherche, utilisez un ou plusieurs caractères « ? » pour correspondre au nombre exact de caractères. Par exemple, dans l’illustration suivante :

* la requête `run???` ne correspond à aucune ressource ;

* la requête `run????` correspond au mot `running` avec quatre caractères après `run` ;

* la requête `??run` correspond au mot `rerun` avec deux caractères avant `run`.

![Exemple d’utilisation d’un caractère générique (point d’interrogation) dans la recherche de ressources](assets/search_with_questionmark_run.gif)

*Figure : Exemple d’utilisation d’un caractère générique (point d’interrogation) dans la recherche de ressources.*

**Exclusion d’un mot-clé** : utilisez le tiret pour rechercher des ressources qui ne contiennent pas de mot-clé. Par exemple, la requête `running -shoe` renvoie les ressources qui contiennent `running`, mais pas `shoe`. De même, la requête `camp -night` renvoie les ressources qui contiennent `camp`, mais pas `night`. La requête `camp-night` renvoie des ressources contenant `camp` et `night`.

![Utilisation du tiret pour rechercher des ressources ne contenant pas de mot-clé exclu](assets/search_dash_exclude_keyword.gif)

*Figure : Utilisation du tiret pour rechercher des ressources ne contenant pas de mot-clé exclu.*

## Tâches de configuration et d&#39;administration relatives à la fonctionnalité de recherche {#configadmin}

### Configurations d&#39;index de recherche {#searchindex}

La découverte des ressources repose sur l’indexation du contenu de la gestion des actifs numériques, y compris les métadonnées. La découverte plus rapide et précise des ressources repose sur une indexation optimisée et des configurations appropriées. Voir [index de recherche](/help/assets/performance-tuning-guidelines.md#search-indexes), [requêtes de chêne et indexation](/help/sites-deploying/queries-and-indexing.md) et [meilleures pratiques](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

Pour exclure des ressources spécifiques des résultats de la recherche, utilisez la propriété `excludedPath` dans l&#39;index Lucene.

### Recherche visuelle ou de similarité {#configvisualsearch}

La recherche visuelle utilise des balises actives. Après avoir configuré la fonctionnalité de balisage intelligent, procédez comme suit.

1. Dans [!DNL Experience Manager] CRXDE, dans le noeud `/oak:index/lucene`, ajoutez les propriétés et valeurs suivantes et enregistrez les modifications.

   * `costPerEntry` de type  `Double` avec la valeur  `10`.
   * `costPerExecution` de type  `Double` avec la valeur  `2`.
   * `refresh` de type  `Boolean` avec la valeur  `true`.

   Cette configuration permet d&#39;effectuer des recherches à partir de l&#39;index approprié.

1. Pour créer un index Lucene, dans CRXDE, à `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, créez un noeud nommé `imageFeatures` de type `nt-unstructured`. Dans le noeud `imageFeatures`,

   * Ajoutez la propriété `name` de type `String` avec la valeur `jcr:content/metadata/imageFeatures/haystack0`.
   * Ajoutez la propriété `nodeScopeIndex` de type `Boolean` avec la valeur `true`.
   * Ajoutez la propriété `propertyIndex` de type `Boolean` avec la valeur `true`.
   * Ajoutez la propriété `useInSimilarity` de type `Boolean` avec la valeur `true`.

   Enregistrez les modifications.

1. Accédez à `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` et ajoutez la propriété `similarityTags` de type `Boolean` avec la valeur `true`.
1. Appliquez des balises actives aux actifs de votre référentiel [!DNL Experience Manager]. Voir [comment configurer les balises actives](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html?lang=en#configuring).
1. Dans CRXDE, dans le noeud `/oak-index/damAssetLucene`, définissez la propriété `reindex` sur `true`. Enregistrez les modifications.
1. (Facultatif) Si vous avez personnalisé le formulaire de recherche, copiez le noeud `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` dans `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Enregistrez les modifications.

Pour plus d’informations, voir [comprendre les balises actives en Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) et [comment gérer les balises actives](/help/assets/enhanced-smart-tags.md).

>[!CAUTION]
>
>Si l&#39;indexation Lucene est effectuée à partir de [!DNL Adobe Experience Manager], la recherche basée sur les balises actives ne fonctionne pas comme prévu.

### Métadonnées obligatoires {#mandatorymetadata}

Les utilisateurs professionnels, les administrateurs ou les bibliothécaires de gestion des actifs numériques peuvent définir certaines métadonnées comme des métadonnées obligatoires indispensables au fonctionnement des processus d’entreprise. Pour diverses raisons, certaines ressources peuvent ne pas disposer de ces métadonnées, telles que les ressources héritées ou les ressources migrées en bloc. Les ressources contenant des métadonnées manquantes ou non valides sont détectées et rapportées en fonction de la propriété de métadonnées indexées. Pour le configurer, voir [métadonnées obligatoires](/help/assets/metadata-schemas.md#define-mandatory-metadata).

### Modification des facettes de recherche {#searchfacets}

Pour accélérer la découverte, [!DNL Experience Manager Assets] offre les facettes de recherche à l&#39;aide desquelles vous pouvez filtrer les résultats de la recherche. Par défaut, le panneau Filtres comprend quelques facettes standard. Les administrateurs peuvent personnaliser le panneau Filtres pour modifier les facettes par défaut à l’aide des prédicats intégrés. [!DNL Experience Manager] fournit une bonne collection de prédicats intégrés et un éditeur pour personnaliser les facettes. Voir [facettes de recherche](/help/assets/search-facets.md).

### Extraire du texte lors du téléchargement de fichiers {#extracttextupload}

Vous pouvez configurer [!DNL Experience Manager] pour extraire le texte des ressources lorsque les utilisateurs téléchargent des ressources, telles que des fichiers PSD ou PDF. [!DNL Experience Manager] indexe le texte extrait et aide les utilisateurs à rechercher ces ressources en fonction du texte extrait. Voir [télécharger des ressources](/help/assets/manage-assets.md#uploading-assets).

Si l’extraction de texte nécessite trop de ressources pour votre déploiement, envisagez de [désactiver l’extraction de texte](https://helpx.adobe.com/experience-manager/kb/Disable-binary-text-extraction-to-optimize-Lucene-indexing-AEM.html).

### Prédicats personnalisés pour filtrer les résultats de la recherche {#custompredicates}

Les prédicats sont utilisés pour créer des facettes. Les administrateurs peuvent personnaliser les facettes de recherche dans le panneau Filtres à l’aide de prédicats préconfigurés. Ces prédicats peuvent être personnalisés à l’aide d’incrustations. Voir [créer des prédicats personnalisés](/help/assets/searchx.md).

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
| Débit audio | Indiqué sous la forme d’une valeur minimale et d’une valeur maximale. La valeur est stockée uniquement dans les métadonnées des rendus vidéo. |

## Utilisation des résultats de recherche de ressources {#aftersearch}

Vous pouvez effectuer les opérations suivantes avec les ressources que vous avez recherchées dans [!DNL Experience Manager] :

* Afficher les propriétés de métadonnées et d’autres informations
* Télécharger une ou plusieurs ressources
* Utiliser les actions de bureau pour ouvrir ces ressources dans l’application de bureau
* Créer des collections dynamiques

### Tri des résultats de la recherche {#sort}

Trier les résultats de la recherche pour découvrir plus rapidement les ressources requises. Vous pouvez trier les résultats de recherche en mode liste et uniquement lorsque vous sélectionnez **[[!UICONTROL Fichiers]](#searchui)** dans le panneau **[!UICONTROL Filtres]**. [!DNL Assets] utilise le tri côté serveur pour trier rapidement toutes les ressources (quel que soit leur nombre) dans un dossier ou les résultats d’une requête. Le tri côté serveur fournit des résultats plus rapides et plus précis que le tri côté client.

En mode Liste, vous pouvez trier les résultats de recherche tout comme vous pouvez trier les ressources de n’importe quel dossier. Le tri fonctionne sur ces colonnes : Nom, Titre, État, Dimensions, Taille, Évaluation, Utilisation, (Date de) création, (Date de) publication, Workflow et Extraits.

Pour connaître les restrictions de la fonctionnalité de tri, voir [Restrictions](#limitations).

### Consultation des informations détaillées d’une ressource {#checkinfo}

Vous pouvez consulter les informations détaillées d’une ressource recherchée à partir de la page des résultats de recherche.

Pour afficher toutes les métadonnées d’une ressource, sélectionnez-la, puis cliquez sur **[!UICONTROL Propriétés]** dans la barre d’outils.

Pour consulter les commentaires sur une ressource ou son historique de versions, cliquez sur la ressource afin d’ouvrir l’aperçu de grande taille. Ouvrez la chronologie dans le rail de gauche et sélectionnez **[!UICONTROL Commentaires]** ou **[!UICONTROL Versions]**. Vous pouvez également trier l’activité de la chronologie comme les commentaires ou les versions dans un ordre chronologique.

![Tri des entrées de chronologie d’une ressource recherchée](assets/sort_timeline_search_results.gif)

*Figure : Tri des entrées de chronologie d’une ressource recherchée.*

### Téléchargement des ressources recherchées {#download}

Vous pouvez télécharger les ressources recherchées et leurs rendus de la même façon que vous téléchargez des ressources ordinaires à partir de dossiers. Sélectionnez une ou plusieurs ressources dans les résultats de recherche, puis cliquez sur **[!UICONTROL Télécharger]** dans la barre d’outils.

### Mise à jour des propriétés de métadonnées en masse {#metadataupdates}

Il est possible d’effectuer des mises à jour en masse des champs de métadonnées courants de plusieurs ressources. Dans les résultats de recherche, sélectionnez une ou plusieurs ressources. Cliquez sur **[!UICONTROL Propriétés]** dans la barre d’outils et mettez à jour les métadonnées selon les besoins. Cliquez sur **[!UICONTROL Enregistrer et fermer]** lorsque vous avez terminé. Les métadonnées figurant précédemment dans les champs mis à jour sont remplacées.

Pour les ressources se trouvant dans un dossier ou une collection unique, il est plus facile de [mettre à jour les métadonnées en masse](/help/assets/metadata.md) sans utiliser la fonction de recherche. Pour les ressources disponibles dans plusieurs dossiers ou correspondant à un critère commun, il est plus rapide de mettre à jour les métadonnées en masse par l’intermédiaire d’une recherche.

### Collections dynamiques {#smart-collections}

Une collection est un ensemble ordonné de ressources pouvant inclure des ressources provenant de différents emplacements, car les collections ne contiennent que des références à ces ressources. Les collections sont de deux types :

* Une liste de référence statique de ressources, dossiers et autres collections
* Une liste dynamique (collection dynamique) qui peuple la collection de ressources en fonction de critères de recherche

Vous pouvez créer des collections dynamiques en fonction des critères de recherche. Dans le panneau **[!UICONTROL Filtres]**, sélectionnez **[!UICONTROL Fichiers]** et cliquez sur **[!UICONTROL Enregistrer la collection dynamique]**. Voir [Gestion des collections](/help/assets/manage-collections.md).

## Résultats de recherche inattendus et problèmes {#unexpected-results}

| Erreur, problèmes, symptômes | Raison possible | Solution possible ou explication du problème |
|---|---|---|
| Résultats incorrects lors de la recherche de ressources avec des métadonnées manquantes. | Lors de la recherche de ressources qui ne contiennent pas les métadonnées obligatoires, [!DNL Experience Manager] peut afficher certaines ressources qui ont des métadonnées valides. Les résultats reposent sur la propriété de métadonnées indexées. | Une fois les métadonnées mises à jour, une nouvelle indexation est nécessaire pour refléter l’état correct des métadonnées des ressources. Voir [Métadonnées obligatoires](metadata-schemas.md#define-mandatory-metadata). |
| Trop de résultats de recherche. | Paramètre de recherche étendu. | Envisagez de limiter la [portée de la recherche](#scope). L’utilisation de balises intelligentes peut produire plus de résultats de recherche que vous ne le pensiez. Voir [Comportement de la recherche avec des balises intelligentes](#withsmarttags). |
| Résultats de recherche sans rapport ou partiellement liés. | Le comportement de la recherche change avec le balisage intelligent. | Comprendre [comment change la recherche après le balisage intelligent](#withsmarttags). |
| Aucune suggestion de saisie semi-automatique pour les ressources. | Les ressources qui viennent d’être chargées ne sont pas encore indexées. Les métadonnées ne sont pas immédiatement disponibles comme suggestions lorsque vous commencez à saisir un mot-clé de recherche dans la barre Omni-recherche. | [!DNL Experience Manager] attend jusqu’à l’expiration d’un délai d’attente (par défaut, une heure) avant d’effectuer une tâche en arrière-plan afin d’indexer les métadonnées pour toutes les ressources chargées/mises à jour dernièrement et de les ajouter à la liste de suggestions. |
| Aucun résultat de recherche. | <ul><li>Les ressources correspondant à votre requête n’existent pas. </li><li> Espace ajouté avant la requête de recherche. </li><li> Un champ de métadonnées non pris en charge contient le mot-clé que vous avez recherché.</li><li> Recherche effectuée pendant qu’une ressource était désactivée. </li></ul> | <ul><li>Rechercher avec un autre mot-clé. Vous pouvez également utiliser le balisage intelligent ou la recherche par analogie pour améliorer les résultats de la recherche. </li><li>[Limite connue](#limitations).</li><li>Certains champs de métadonnées ne sont pas pris en compte pour les recherches. Voir [Portée](#scope).</li><li>Effectuer une recherche plus tard ou modifier l’heure d’activation et de désactivation des ressources requises.</li></ul> |
| Aucun filtre de recherche ou prédicat n’est disponible. | <ul><li>Le filtre de recherche n’est pas configuré.</li><li>Il n’est pas disponible pour votre connexion.</li><li>(Moins probable) Les options de recherche ne sont pas personnalisées sur le déploiement que vous utilisez.</li></ul> | <ul><li>Contacter l’administrateur pour vérifier la disponibilité de personnalisations de la recherche.</li><li>Contacter l’administrateur pour vérifier si votre compte dispose du privilège ou d’autorisations permettant d’utiliser la personnalisation.</li><li>Contacter l’administrateur et vérifier les personnalisations disponibles pour le déploiement [!DNL Assets] que vous utilisez.</li></ul> |
| Lors de la recherche d’images similaires visuellement, une image attendue est manquante. | <ul><li>L’image n’est pas disponible dans [!DNL Experience Manager].</li><li>L’image n’est pas indexée. Généralement lorsqu’elle a été téléchargée récemment.</li><li>L’image ne présente pas de balisage intelligent.</li></ul> | <ul><li>Ajoutez l’image à [!DNL Assets].</li><li>Contactez votre administrateur pour indexer à nouveau le référentiel. Veillez également à utiliser l’index approprié.</li><li>Contactez votre administrateur pour procéder au balisage intelligent des ressources appropriées.</li></ul> |
| Lors de la recherche d’images similaires visuellement, une image inappropriée est affichée. | Comportement de recherche visuelle. | [!DNL Experience Manager] affiche autant de ressources potentiellement pertinentes que possible. Les images moins pertinentes, le cas échéant, sont ajoutées aux résultats, mais avec un classement inférieur dans les résultats de recherche. La qualité des correspondances et la pertinence des ressources recherchées diminuent à mesure que vous descendez dans les résultats de la recherche. |
| Lors de la sélection de résultats de la recherche et d’action sur ces résultats, aucune action n’est réalisée sur certaines ressources recherchées. | L’option [!UICONTROL Sélectionner tout] ne sélectionne que les 100 premiers résultats de recherche en mode carte et les 200 premiers résultats de recherche en mode liste. |  |

>[!MORELIKETHIS]
>
>* Guide de mise en œuvre des recherches[[!DNL Experience Manager] ](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html?lang=fr)
>* [Configuration avancée pour améliorer les résultats de recherche](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [Configuration de la recherche de traduction intelligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html?lang=fr)

