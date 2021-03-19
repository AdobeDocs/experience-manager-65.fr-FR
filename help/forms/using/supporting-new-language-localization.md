---
title: Support de nouveaux paramètres régionaux pour la localisation de formulaires adaptatifs
seo-title: Support de nouveaux paramètres régionaux pour la localisation de formulaires adaptatifs
description: AEM Forms vous permet d’ajouter de nouveaux paramètres régionaux pour localiser les formulaires adaptatifs. Les paramètres régionaux offertes sont par défaut l’anglais, le français, l’allemand et le japonais.
seo-description: AEM Forms vous permet d’ajouter de nouveaux paramètres régionaux pour localiser les formulaires adaptatifs. Les paramètres régionaux offertes sont par défaut l’anglais, le français, l’allemand et le japonais.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
feature: Formulaires adaptatifs
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 50%

---


# Support de nouveaux paramètres régionaux pour la localisation de formulaires adaptatifs{#supporting-new-locales-for-adaptive-forms-localization}

## A propos des dictionnaires de paramètres régionaux{#about-locale-dictionaries} 

La localisation des formulaires adaptatifs repose sur deux types de dictionnaires de paramètres régionaux : 

**Dictionnaire spécifique au formulaireContient** des chaînes utilisées dans les formulaires adaptatifs. Par exemple, étiquettes, noms de champs, messages d’erreur, descriptions d’aide, et ainsi de suite. Il est géré sous la forme d’un ensemble de fichiers XLIFF pour chaque paramètre régional et vous pouvez y accéder à l’adresse `https://<host>:<port>/libs/cq/i18n/translator.html`.

**** dictionnaires globauxIl existe deux dictionnaires globaux, gérés en tant qu’objets JSON, dans AEM bibliothèque cliente. Ces dictionnaires contiennent les messages d’erreur par défaut, les noms des mois, les symboles de devise, les modèles de date et d’heure, et ainsi de suite. Vous pouvez trouver ces dictionnaires dans CRXDe Lite à l’adresse /libs/fd/xfaforms/clientlibs/I18N. Ces emplacements contiennent des dossiers distincts pour chaque jeu de paramètres régionaux. Étant donné que les dictionnaires globaux ne sont généralement pas mis à jour fréquemment, conserver des fichiers JavaScript distincts pour chaque jeu de paramètres régionaux permet aux navigateurs de les mettre en cache et de réduire l’utilisation de la bande passante du réseau lors de l’accès à différents formulaires adaptatifs sur le même serveur. 

### Comment fonctionne la localisation des formulaires adaptatifs{#how-localization-of-adaptive-form-works} 

Il existe deux méthodes pour identifier les paramètres régionaux du formulaire adaptatif. Lorsqu’un formulaire adaptatif est rendu, il identifie les paramètres régionaux requis par :

* consultez le sélecteur `[local]` dans l’URL du formulaire adaptatif. Le format de l’URL est `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`. L’utilisation du sélecteur `[local]` permet la mise en cache d’un formulaire adaptatif.

* en examinant les paramètres suivants dans l’ordre spécifié :

   * Paramètre de requête `afAcceptLang`
Pour remplacer les paramètres régionaux du navigateur des utilisateurs, vous pouvez transmettre la variable 
`afAcceptLang` pour forcer le paramètre régional. Par exemple, l’URL suivante force le rendu du formulaire dans les paramètres régionaux japonais :
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * Paramètre régional du navigateur défini pour l’utilisateur, qui est spécifié dans la requête à l’aide de l’en-tête `Accept-Language`.

   * Paramètre de langue de l’utilisateur spécifié dans AEM.  

   * Par défaut, les paramètres régionaux du navigateur sont activés. Pour modifier les paramètres régionaux du navigateur, procédez comme suit :
      * Ouvrez le gestionnaire de configuration. L’URL est `http://[server]:[port]/system/console/configMgr`
      * Recherchez et ouvrez la configuration **[!UICONTROL Formulaire adaptatif et Canal Web de communication interactive]**.
      * Modifiez l’état de l’option **[!UICONTROL Utiliser les paramètres régionaux du navigateur]** et **[!UICONTROL Enregistrer]** la configuration.

Une fois que le paramètre régional est identifié, le formulaire adaptatif sélectionne le dictionnaire qui lui est spécifique. Si le dictionnaire spécifique au formulaire pour les paramètres régionaux demandés est introuvable, il utilise le dictionnaire pour la langue dans laquelle le formulaire adaptatif a été créé.

Si aucune information de paramètre régional n’est présente, le formulaire adaptatif est distribué dans la langue d’origine du formulaire. La langue d’origine est la langue utilisée lors du développement du formulaire adaptatif.

S’il n’existe pas de bibliothèque client pour le paramètre régional requis, il recherche une bibliothèque client correspondant au code de langue présent dans le paramètre régional. Par exemple, si le paramètre régional requis est `en_ZA`  ( (anglais Afrique du sud) et qu’il n’existe pas de bibliothèque client correspondant à `en_ZA`, le formulaire adaptatif utilise la bibliothèque client correspondant à la langue `en` (anglais), si elle existe. Toutefois, si aucune de ces bibliothèques n’existe, le formulaire adaptatif utilise le dictionnaire correspondant au paramètre régional `en`.

## Ajoutez la localisation pour les paramètres régionaux non pris en charge{#add-localization-support-for-non-supported-locales} 

AEM Forms prend actuellement en charge la localisation du contenu des formulaires adaptatifs en anglais (en), espagnol (es), français (fr), italien (it), allemand (de), japonais (ja), portugais-brésilien (pt-BR), chinois (zh-CN), chinois-taïwanais (zh-TW) et coréen (ko-KR).

Pour ajouter un nouveau paramètre régional lors de l’exécution des formulaires adaptatifs :

1. [Ajouter un paramètre régional au service GuideLocalizationService](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Ajouter la bibliothèque XFA client pour un paramètre régional](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Ajouter la bibliothèque cliente de formulaires adaptatifs pour un paramètre régional](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Ajouter un support pour la langue du dictionnaire](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Redémarrez le serveur](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Ajouter un paramètre régional au service Guide Localisation {#add-a-locale-to-the-guide-localization-service-br}

1. Accédez à `https://'[server]:[port]'/system/console/configMgr`.
1. Cliquer pour modifier le composant **Guide Localization Service**.
1. Ajouter le paramètre régional que vous souhaitez à la liste des paramètres régionaux de supports

![GuideLocalizationSevice](assets/configservice.png)

### Ajouter la bibliothèque XFA client pour un paramètre régional {#add-xfa-client-library-for-a-locale-br}

Créez un noeud de type `cq:ClientLibraryFolder` sous `etc/<folderHierarchy>`, avec la catégorie `xfaforms.I18N.<locale>`, et ajoutez les fichiers suivants à la bibliothèque cliente :

* **I18N.** jsdéfinition  `xfalib.locale.Strings` pour la  `<locale>` fonction définie dans  `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`la.

* **js.txt** contenant les éléments suivants :

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Ajouter la bibliothèque cliente de formulaires adaptatifs pour un paramètre régional {#add-adaptive-form-client-library-for-a-locale-br}

Créez un noeud de type `cq:ClientLibraryFolder` sous `etc/<folderHierarchy>`, avec la catégorie `guides.I18N.<locale>` et les dépendances `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` et `guide.common`. &quot;

Ajouter les fichiers suivants à la bibliothèque client :

* **i18n.** jsdefinition  `guidelib.i18n`, ayant des modèles de &quot;calendarSymbols&quot;,  `datePatterns`,  `timePatterns`,  `dateTimeSymbols`,  `numberPatterns`,  `numberSymbols`, , , pour les selon les spécifications XFA décrites dans le  de spécification des ensembles de paramètres régionaux de l’.`currencySymbols``typefaces``<locale>`[](https://helpx.adobe.com/fr/content/dam/Adobe/specs/xfa_spec_3_3.pdf) Vous pouvez également voir comment il est défini pour les autres paramètres régionaux pris en charge dans `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.** jsdefinition  `guidelib.i18n.strings` et  `guidelib.i18n.LogMessages` pour la  `<locale>` fonction définie dans  `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`la.
* **js.txt** contenant les éléments suivants :

```text
i18n.js
LogMessages.js
```

### Ajouter un support pour la langue du dictionnaire {#add-locale-support-for-the-dictionary-br}

Effectuez cette étape uniquement si le `<locale>` que vous ajoutez n&#39;est pas compris dans `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Créez un `nt:unstructured` noeud `languages` sous `etc`, s’il n’est pas déjà présent.

1. Ajoutez une propriété de chaîne à plusieurs valeurs `languages` au noeud, si elle n’est pas déjà présente.
1. Ajoutez les valeurs de paramètres régionaux par défaut `<locale>` `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, si elles ne sont pas déjà présentes.

1. Ajoutez `<locale>` sur les valeurs de la propriété `languages` de `/etc/languages`.

Le `<locale>` apparaît à `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### Redémarrez le serveur {#restart-the-server}

Redémarrez le serveur AEM pour que le paramètre régional ajouté entre en vigueur.

## Exemples de bibliothèques pour ajouter la prise en charge de l&#39;espagnol{#sample-libraries-for-adding-support-for-spanish} 

Exemples de bibliothèques clientes pour ajouter la prise en charge de l’espagnol

[Obtenir le fichier](assets/sample.zip)
