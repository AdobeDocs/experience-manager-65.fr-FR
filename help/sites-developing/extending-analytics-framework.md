---
title: Personnalisation du framework Adobe Analytics
description: Découvrez comment personnaliser le framework Adobe Analytics pour Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '1610'
ht-degree: 99%

---

# Personnalisation du framework Adobe Analytics{#customizing-the-adobe-analytics-framework}

Le framework Adobe Analytics détermine les informations suivies avec Adobe Analytics. Afin de personnaliser le framework par défaut, utilisez JavasSript pour ajouter un suivi personnalisé, intégrer les modules externes Adobe Analytics et modifier les paramètres généraux dans le framework utilisé pour le suivi.

## À propos du code JavasSript généré pour les frameworks {#about-the-generated-javascript-for-frameworks}

Lorsqu’une page est associée à un cadre Adobe Analytics et qu’elle contient des [références au module Analytics](/help/sites-administering/adobeanalytics.md), un fichier analytics.sitecatalyst.js est automatiquement généré pour la page.

Le code JavaScript dans la page crée un objet `s_gi` (que la bibliothèque Adobe Analytics s_code.js définit) et affecte des valeurs à ses propriétés. Le nom de l’instance d’objet est `s`. Les exemples de code présentés dans cette section font référence à cette variable `s` à plusieurs reprises.

L’exemple de code suivant est similaire au code d’un fichier analytics.sitecatalyst.js :

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

Lorsque vous utilisez du code JavaScript personnalisé pour personnaliser le framework, vous modifiez le contenu de ce fichier.

## Configuration des propriétés Adobe Analytics {#configuring-adobe-analytics-properties}

Un certain nombre de variables prédéfinies dans Adobe Analytics sont configurables sur un framework. Les variables **charset**, **cookieLifetime**, **currencyCode** et **trackInlineStats** font, par défaut, partie de la liste des **Paramètres généraux d’Analytics**.

![aa-22](assets/aa-22.png)

Vous pouvez ajouter des valeurs et des noms de variables à la liste. Ces variables prédéfinies et les variables que vous ajoutez sont utilisées pour configurer les propriétés de l’objet `s` dans le fichier analytics.sitecatalyst.js. L’exemple suivant montre la façon dont la propriété `prop10` ajoutée de la valeur `CONSTANT` est représentée dans le code Javascript :

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

Utilisez la procédure suivante pour ajouter des variables à la liste :

1. Sur votre page de framework Adobe Analytics, développez la zone **Paramètres généraux d’Analytics**.
1. Sous la liste des variables, cliquez sur Ajouter un élément pour ajouter une nouvelle variable à la liste.
1. Dans la cellule de gauche, entrez le nom de la variable, par exemple `prop10`.

1. Dans la colonne de droite, entrez une valeur pour la variable, par exemple `CONSTANT`.

1. Pour supprimer une variable, cliquez sur le bouton - situé en regard de la variable.

>[!NOTE]
>
>Lorsque vous entrez des variables et des valeurs, assurez-vous qu’elles sont correctement mises en forme et orthographiées, sinon les **appels ne seront pas envoyés** avec la paire valeur/variable correcte. Des variables et des valeurs mal orthographiées peuvent même empêcher les appels de se produire.
>
>Adressez-vous à un représentant ou une représentante Adobe Analytics pour vous assurer que ces variables sont correctement définies.

>[!CAUTION]
>
>Certaines des variables de cette liste sont **obligatoires** pour que les appels Adobe Analytics fonctionnent correctement (par exemple, **currencyCode** et **charSet**).
>
>Ainsi, même si elles sont supprimées du framework lui-même, elles restent associées à une valeur par défaut lors de l’appel Adobe Analytics.

### Ajout de code JavaScript personnalisé à un framework Adobe Analytics {#adding-custom-javascript-to-an-adobe-analytics-framework}

La zone Javascript au format libre de la zone **Paramètres généraux d’Analytics** vous permet d’ajouter du code personnalisé à un framework Adobe Analytics.

![aa-21](assets/aa-21.png)

Le code que vous ajoutez est ajouté au fichier analytics.sitecatalyst.js. Par conséquent, vous pouvez accéder à la variable `s` qui est une instance de l’objet Javascript `s_gi` défini dans `s_code.js`. Par exemple, l’ajout du code suivant équivaut à ajouter une variable nommée `prop10` de valeur `CONSTANT`, qui est l’exemple de la section précédente :

`s.prop10= 'CONSTANT';`

Le code du fichier [analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) (qui inclut le contenu du fichier Adobe Analytics `s-code.js`) contient le code suivant :

`if (s.usePlugins) s.doPlugins(s)`

La procédure suivante montre comment utiliser la zone JavaScript pour personnaliser le suivi Adobe Analytics. Si votre code Javascript doit utiliser les modules externes d’Adobe Analytics, [intégrez-les](/help/sites-administering/adobeanalytics.md) à AEM.

1. Ajoutez le code Javascript suivant à la zone afin que `s.doPlugins` soit exécuté :

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >Ce code est nécessaire si vous souhaitez envoyer des variables dans un appel Adobe Analytics, variables qui ont été personnalisées d’une façon impossible à réaliser via l’interface basique de glisser-déposer OU via le code JavaScript intégré en mode Adobe Analytics.
   >
   >Si les variables personnalisées sont en dehors de la fonction s_doPlugins, elles sont envoyées comme *undefined* dans l’appel Adobe Analytics

1. Ajoutez votre code Javascript dans la fonction **s_doPlugins**.

L’exemple suivant concatène les données capturées sur une page dans l’ordre hiérarchique, en utilisant un séparateur commun « | ».

Un framework Adobe Analytics possède les configurations suivantes :

* La variable Adobe Analytics `prop2` est mappée à la propriété `pagedata.sitesection` du site.

* La variable Adobe Analytics `prop3` est mappée à la propriété `pagedata.subsection` du site.

* Le code suivant est ajouté à la zone JavaScript au format libre :

  ```
  s.usePlugins=true;
   function s_doPlugins(s) {
   s.prop1 = s.prop2+'|'+s.prop3;
   }
   s.doPlugins=s_doPlugins;
  ```

* Si la page Web qui utilise le framework est consultée (ou, en mode d’édition, la page est rechargée ou prévisualisée), les appels à Adobe Analytics sont effectués.

Par exemple, les valeurs suivantes sont générées dans Adobe Analytics :

![aa-20](assets/aa-20.png)

### Ajout de code personnalisé global pour tous les frameworks Adobe Analytics {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

Entrez du code JavaScript personnalisé intégré à tous les frameworks Adobe Analytics. Lorsque le framework Adobe Analytics d’une page ne contient pas de code [JavaScript au format libre](/help/sites-administering/adobeanalytics.md) personnalisé, le code JavaScript généré par le script /libs/cq/analytics/components/sitecatalyst/config.js.jsp est ajouté au fichier [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md). Par défaut, le script n’a aucun effet car il est commenté. Le code définit également `s.usePlugins` sur `false` :

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

Le code du fichier analytics.sitecatalyst.js (qui inclut le contenu du Adobe Analytics s_code.js) contient le code suivant :

if (s.usePlugins) s.doPlugins(s)

Par conséquent, votre code JavaScript doit définir `s.usePlugins` sur `true` pour que le code de la fonction `s_doPlugins` soit exécuté. Pour personnaliser le code, superposez le fichier config.js.jsp avec celui qui utilise votre propre code JavaScript. Si votre code JavaScript doit utiliser les modules externes d’Adobe Analytics, [intégrez-les](/help/sites-administering/adobeanalytics.md) à AEM.

>[!NOTE]
>
>Ne modifiez pas le fichier /libs/cq/analytics/components/sitecatalyst/config.js.jsp. Certaines tâches de mise à niveau ou de maintenance d’AEM peuvent réinstaller le fichier d’origine, supprimant ainsi vos modifications.

1. Dans CRXDE Lite, créez la structure de dossiers /apps/cq/analytics/components :

   1. Cliquez avec le bouton droit sur le dossier /apps puis sur Créer > Créer un dossier.
   1. Indiquez `cq` comme nom de dossier, puis cliquez sur OK.
   1. De même, créez les dossiers `analytics` et `components`.

1. Cliquez avec le bouton droit sur le dossier `components` que vous avez créé et cliquez sur Créer > Créer un composant. Spécifiez les valeurs de propriété suivantes :

   * Libellé : `sitecatalyst`
   * Titre : `sitecatalyst`
   * Super Type : `/libs/cq/analytics/components/sitecatalyst`
   * Groupe : `hidden`

1. Cliquez plusieurs fois sur Suivant jusqu’à ce que le bouton OK soit activé, puis cliquez sur OK.

   Le composant sitecatalyst contient le fichier sitecatalyst.jsp automatiquement créé.

1. Cliquez avec le bouton droit sur le fichier sitecatalyst.jsp et cliquez sur Supprimer.

1. Cliquez avec le bouton droit sur le composant sitecatalyst et cliquez sur Créer > Créer un fichier. Indiquez le nom `config.js.jsp`, puis cliquez sur OK.

   Le fichier config.js.jsp s’ouvre automatiquement pour se faire modifier.

1. Ajoutez le texte suivant au fichier, puis cliquez sur Enregistrer tout :

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   Le code JavaScript généré par le script /apps/cq/analytics/components/sitecatalyst/config.js.jsp est désormais inséré dans le fichier analytics.sitecatalyst.js pour toutes les pages utilisant un framework Adobe Analytics.

1. Ajoutez le code JavaScript que vous voulez exécuter dans la fonction `s_doPlugins`, puis cliquez sur Enregistrer tout.

>[!CAUTION]
>
>Si du texte est présent dans le code JavaScript de forme libre du framework d’une page (même uniquement les espaces), config.js.jsp est ignoré.

### Utilisation des modules externes Adobe Analytics dans AEM {#using-adobe-analytics-plugins-in-aem}

Obtenez le code JavaScript pour les modules externes d’Adobe Analytics et intégrez-les à votre framework Adobe Analytics dans AEM. Ajoutez le code dans un dossier de bibliothèque cliente de la catégorie `sitecatalyst.plugins` afin qu’il soit disponible pour votre code JavaScript personnalisé.

Par exemple, si vous intégrez le module externe `getQueryParams`, vous pouvez appeler le module externe depuis la fonction `s_doPlugins` de votre code JavaScript personnalisé. L’exemple de code suivant envoie la chaîne de requête dans le **« pid »** de l’URL du référent sous la forme **eVar1**, lorsqu’un appel Adobe Analytics est déclenché.

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM installe les modules externes Adobe Analytics suivants qui sont donc disponibles par défaut :

* getQueryParam()
* getPreviousValue()
* split()

Le dossier de bibliothèque cliente /libs/cq/analytics/clientlibs/sitecatalyst/plugins contient ces modules externes dans la catégorie sitecatalyst.plugins.

>[!NOTE]
>
>Créez un dossier de bibliothèque cliente pour vos plug-ins. N’ajoutez pas de modules externes au dossier `/libs/cq/analytics/clientlibs/sitecatalyst/plugins`. Cette pratique garantit que votre contribution à la catégorie `sitecatalyst.plugins` ne se retrouve pas remplacée lors de réinstallations ou de mises à niveau d’AEM.

Suivez la procédure ci-après pour créer le dossier de bibliothèque cliente de vos modules externes. Vous n’avez à réaliser cette opération qu’une seule fois. Pour ajouter un module externe au dossier de bibliothèque cliente, procédez comme suit.

1. Dans un navigateur Web, ouvrez CRXDE Lite. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. Cliquez avec le bouton droit sur le dossier /apps/my-app/clientlibs puis sur Créer > Créer un nœud. Entrez les valeurs de propriété suivantes, puis cliquez sur OK :

   * Nom : nom de votre dossier de bibliothèque cliente, par exemple, mes-modules-externes

   * Type : cq:ClientLibraryFolder

1. Sélectionnez le dossier de bibliothèque cliente que vous avez créé et utilisez la barre de propriétés en bas à droite pour ajouter la propriété suivante :

   * Nom : categories
   * Type : chaîne
   * Valeur : sitecatalyst.plugins
   * Multi : sélectionné

   Cliquez sur OK dans la fenêtre Modifier pour confirmer la valeur de la propriété.

1. Cliquez avec le bouton droit sur le dossier de votre bibliothèque cliente, puis cliquez sur Créer > Créer un fichier. Pour le nom de fichier, tapez js.txt, puis cliquez sur OK.

1. Cliquez sur Enregistrer tout.

Procédez comme suit pour obtenir le code du module externe, stocker le code dans le référentiel AEM et l’ajouter dans votre dossier de bibliothèque cliente.

1. Connectez-vous à [sc.omniture.com](https://sc.omniture.com/login/) en utilisant votre compte Adobe Analytics.
1. Sur la page de destination, accédez à Aide > Accueil de l’aide.
1. Dans la table des matières sur le côté gauche, cliquez sur Plug-ins d’implémentation.
1. Cliquez sur le lien vers le plug-in que vous souhaitez ajouter. Quand la page s’ouvre, recherchez le code source Javascript pour le plug-in externe, puis sélectionnez-le et copiez-le.

1. Cliquez avec le bouton droit sur le dossier de votre bibliothèque cliente, puis cliquez sur Créer > Créer un fichier. Pour le nom de fichier, tapez le nom du module externe que vous intégrez, suivi du suffixe .js, puis cliquez sur OK. Par exemple, si vous intégrez le module externe getQueryParam, nommez le fichier getQueryParam.js.

   Lorsque vous créez le fichier, il s’ouvre pour se faire modifier.

1. Collez le code Javascript du plug-in dans le fichier, cliquez sur Enregistrer tout, puis fermez le fichier.

1. Ouvrez le fichier js.txt à partir du dossier de votre bibliothèque cliente.

1. Dans une nouvelle ligne, ajoutez le nom du fichier qui contient le plug-in, par exemple getQueryParam.js. Ensuite, cliquez sur Enregistrer tout et fermez le fichier.

>[!NOTE]
>
>Lors de l’utilisation de plug-ins, assurez-vous d’intégrer des plug-ins de support. À défaut, le plug-in Javascript ne reconnaîtra pas les appels qu’il passe aux fonctions du plug-in de support. Par exemple, le plug-in getPreviousValue() nécessite le plug-in split() pour fonctionner correctement.
>
>Le nom du module externe de support doit également être ajouté au fichier **js.txt**.
