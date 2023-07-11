---
title: Personnalisation du framework Adobe Analytics
description: Personnalisation du framework Adobe Analytics
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 51%

---

# Personnalisation du framework Adobe Analytics{#customizing-the-adobe-analytics-framework}

Le framework Adobe Analytics détermine les informations suivies avec Adobe Analytics. Pour personnaliser la structure par défaut, vous utilisez JavaScript pour ajouter un suivi personnalisé, intégrer des modules externes Adobe Analytics et modifier les paramètres généraux de la structure utilisée pour le suivi.

## À propos du code JavaScript généré pour les structures {#about-the-generated-javascript-for-frameworks}

Lorsqu’une page est associée à une structure Adobe Analytics et que la page inclut [références au module Analytics](/help/sites-administering/adobeanalytics.md), un fichier analytics.sitecatalyst.js est automatiquement généré pour la page.

Le code JavaScript de la page crée une `s_gi`(que la bibliothèque Adobe Analytics s_code.js définit) et attribue des valeurs à ses propriétés. Le nom de l’instance d’objet est `s`. Les exemples de code présentés dans cette section font référence à cette variable `s` à plusieurs reprises.

L’exemple de code suivant est similaire au code d’un fichier analytics.sitecatalyst.js :

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

Lorsque vous utilisez du code JavaScript personnalisé pour personnaliser la structure, vous modifiez le contenu de ce fichier.

## Configuration des propriétés Adobe Analytics {#configuring-adobe-analytics-properties}

Il existe plusieurs variables prédéfinies dans Adobe Analytics qui peuvent être configurées sur une structure. Les variables **charset**, **cookieLifetime**, **currencyCode** et **trackInlineStats** font, par défaut, partie de la liste des **Paramètres généraux d’Analytics**.

![aa-22](assets/aa-22.png)

Vous pouvez ajouter des valeurs et des noms de variables à la liste. Ces variables prédéfinies et les variables que vous ajoutez sont utilisées pour configurer les propriétés de l’objet `s` dans le fichier analytics.sitecatalyst.js. L’exemple suivant illustre la manière dont l’ajout de `prop10` propriété de valeur `CONSTANT` est représenté dans le code JavaScript :

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

1. Pour supprimer une variable, cliquez sur le bouton (-) en regard de la variable.

>[!NOTE]
>
>Lorsque vous entrez des variables et des valeurs, assurez-vous qu’elles sont correctement mises en forme et orthographiées, sinon les **appels ne seront pas envoyés** avec la paire valeur/variable correcte. Les variables et valeurs mal orthographiées peuvent même empêcher les appels de se produire.
>
>Consultez votre représentant Adobe Analytics pour vous assurer que ces variables sont correctement définies.

>[!CAUTION]
>
>Certaines des variables de cette liste sont **mandatory** pour que les appels Adobe Analytics fonctionnent correctement (par exemple, **currencyCode**, **charSet**)
>
>Ainsi, même si elles sont supprimées du framework lui-même, elles restent associées à une valeur par défaut lors de l’appel Adobe Analytics.

### Ajout de code JavaScript personnalisé à une structure Adobe Analytics {#adding-custom-javascript-to-an-adobe-analytics-framework}

La zone JavaScript gratuite dans la variable **Paramètres généraux d’Analytics** permet d’ajouter du code personnalisé à une structure Adobe Analytics.

![aa-21](assets/aa-21.png)

Le code que vous ajoutez est ajouté au fichier analytics.sitecatalyst.js. Par conséquent, vous pouvez accéder au `s` qui est une instance de la variable `s_gi` Objet JavaScript défini dans `s_code.js`. Par exemple, l’ajout du code suivant équivaut à ajouter une variable nommée `prop10` de valeur `CONSTANT`, qui est l’exemple de la section précédente :

`s.prop10= 'CONSTANT';`

Le code du fichier [analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) (qui inclut le contenu du fichier Adobe Analytics `s-code.js`) contient le code suivant :

`if (s.usePlugins) s.doPlugins(s)`

La procédure suivante explique comment utiliser la boîte JavaScript pour personnaliser le suivi Adobe Analytics. Si votre JavaScript doit utiliser des modules externes Adobe Analytics, [intégrer](/help/sites-administering/adobeanalytics.md) dans AEM.

1. Ajoutez le code JavaScript suivant à la zone afin que `s.doPlugins` est exécuté :

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >Ce code est nécessaire si vous souhaitez envoyer des variables dans un appel Adobe Analytics qui ont été personnalisées d’une manière ou d’une autre par le biais de l’interface de glisser-déposer de base OU par le biais de JavaScript intégré dans la vue Adobe Analytics.
   >
   >Si les variables personnalisées sont en dehors de la fonction s_doPlugins, elles sont envoyées comme *undefined* dans l’appel Adobe Analytics

1. Ajoutez votre code JavaScript dans la variable **s_doPlugins** fonction .

L’exemple suivant concatène les données capturées sur une page dans l’ordre hiérarchique, en utilisant un séparateur commun « | ».

Une structure Adobe Analytics comporte les configurations suivantes :

* La variable Adobe Analytics `prop2` est mappée à la propriété `pagedata.sitesection` du site.

* La variable Adobe Analytics `prop3` est mappée à la propriété `pagedata.subsection` du site.

* Le code suivant est ajouté à la zone de code JavaScript gratuit :

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

Fournissez du code JavaScript personnalisé intégré à toutes les structures Adobe Analytics. Lorsque la structure Adobe Analytics d’une page ne contient pas de structure personnalisée [JavaScript de forme libre](/help/sites-administering/adobeanalytics.md), le code JavaScript généré par le script /libs/cq/analytics/components/sitecatalyst/config.js.jsp est ajouté à la variable [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md) fichier . Par défaut, le script n’a aucun effet car il est commenté. Le code définit également `s.usePlugins` sur `false` :

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

Par conséquent, votre JavaScript doit être défini sur `s.usePlugins` to `true` de sorte que tout code de la variable `s_doPlugins` est exécutée. Pour personnaliser le code, recouvrez le fichier config.js.jsp avec un fichier qui utilise votre propre code JavaScript. Si votre JavaScript doit utiliser des modules externes Adobe Analytics, [intégrer](/help/sites-administering/adobeanalytics.md) dans AEM.

>[!NOTE]
>
>Ne modifiez pas le fichier /libs/cq/analytics/components/sitecatalyst/config.js.jsp. Certaines tâches de mise à niveau ou de maintenance d’AEM peuvent réinstaller le fichier d’origine, en supprimant vos modifications.

1. Dans CRXDE Lite, créez la structure de dossiers /apps/cq/analytics/components :

   1. Cliquez avec le bouton droit sur le dossier /apps et cliquez sur Créer > Créer un dossier.
   1. Indiquez `cq` comme nom de dossier, puis cliquez sur OK.
   1. De même, créez les dossiers `analytics` et `components`.

1. Cliquez avec le bouton droit sur le dossier `components` que vous venez de créer et cliquez sur Créer > Créer un composant. Spécifiez les valeurs de propriété suivantes :

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

   Le code JavaScript généré par le script /apps/cq/analytics/components/sitecatalyst/config.js.jsp est désormais inséré dans le fichier analytics.sitecatalyst.js pour toutes les pages qui utilisent une structure Adobe Analytics.

1. Ajoutez le code JavaScript que vous souhaitez exécuter dans la variable `s_doPlugins` puis cliquez sur Enregistrer tout.

>[!CAUTION]
>
>Si du texte est présent dans le code JavaScript de forme libre de la structure d’une page (même uniquement des espaces blancs), config.js.jsp est ignoré.

### Utilisation des modules externes Adobe Analytics dans AEM {#using-adobe-analytics-plugins-in-aem}

Procurez-vous le code JavaScript des modules externes Adobe Analytics et intégrez-les à votre structure Adobe Analytics dans AEM. Ajoutez le code à un dossier de bibliothèque cliente de la catégorie. `sitecatalyst.plugins` afin qu’ils soient disponibles pour votre code JavaScript personnalisé.

Par exemple, si vous intégrez la variable `getQueryParams` module externe, vous pouvez appeler le module externe à partir de la fonction `s_doPlugins` de votre code JavaScript personnalisé. L’exemple de code suivant envoie la chaîne de requête dans **&quot;pid&quot;** de l’URL du référent en tant que **eVar1**, lorsqu’un appel Adobe Analytics est déclenché.

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
>Créez un dossier de bibliothèques clientes pour vos modules externes. N’ajoutez pas de modules externes au dossier `/libs/cq/analytics/clientlibs/sitecatalyst/plugins`. Cette pratique garantit que votre contribution à la catégorie `sitecatalyst.plugins` ne se retrouve pas remplacée lors de réinstallations ou de mises à niveau d’AEM.

Suivez la procédure ci-après pour créer le dossier de bibliothèque cliente de vos modules externes. Vous n’avez à réaliser cette opération qu’une seule fois. Pour ajouter un module externe au dossier de bibliothèque cliente, procédez comme suit.

1. Dans un navigateur Web, ouvrez CRXDE Lite. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. Cliquez avec le bouton droit sur le dossier /apps/my-app/clientlibs puis sur Créer > Créer un nœud. Entrez les valeurs de propriété suivantes, puis cliquez sur OK :

   * Nom : nom de votre dossier de bibliothèque cliente, par exemple, mes-modules-externes

   * Type : cq:ClientLibraryFolder

1. Sélectionnez le dossier de bibliothèques clientes que vous avez créé et utilisez la barre de propriétés située en bas à droite pour ajouter la propriété suivante :

   * Nom : categories
   * Type : chaîne
   * Valeur : sitecatalyst.plugins
   * Multi : selected

   Cliquez sur OK dans la fenêtre Modifier pour confirmer la valeur de la propriété.

1. Cliquez avec le bouton droit de la souris sur le dossier de bibliothèques clientes que vous avez créé, puis cliquez sur Créer > Créer un fichier. Pour le nom de fichier, tapez js.txt, puis cliquez sur OK.

1. Cliquez sur Enregistrer tout.

Procédez comme suit pour obtenir le code du module externe, stocker le code dans le référentiel AEM et l’ajouter dans votre dossier de bibliothèque cliente.

1. Connectez-vous à [sc.omniture.com](https://sc.omniture.com/login/) en utilisant votre compte Adobe Analytics.
1. Sur la page d’entrée, accédez à Aide > Page d’accueil de l’aide.
1. Dans la table des matières du côté gauche, cliquez sur Modules externes d’implémentation.
1. Cliquez sur le lien vers le module externe à ajouter. Une fois la page ouverte, recherchez le code source JavaScript du module externe, sélectionnez-le, puis copiez-le.

1. Cliquez avec le bouton droit sur le dossier de votre bibliothèque cliente, puis cliquez sur Créer > Créer un fichier. Pour le nom de fichier, tapez le nom du module externe que vous intégrez, suivi du suffixe .js, puis cliquez sur OK. Par exemple, si vous intégrez le module externe getQueryParam, nommez le fichier getQueryParam.js.

   Lorsque vous créez le fichier, il s’ouvre pour se faire modifier.

1. Collez le code JavaScript du module externe dans le fichier, cliquez sur Enregistrer tout, puis fermez le fichier.

1. Ouvrez le fichier js.txt à partir du dossier de votre bibliothèque cliente.

1. Dans une nouvelle ligne, ajoutez le nom du fichier qui contient le module externe, par exemple getQueryParam.js. Ensuite, cliquez sur Enregistrer tout et fermez le fichier.

>[!NOTE]
>
>Lors de l’utilisation de modules externes, assurez-vous d’intégrer également les modules externes de prise en charge, sinon le module externe JavaScript ne reconnaîtra pas les appels qu’il effectue aux fonctions du module externe de prise en charge. Par exemple, le module externe getPreviousValue() nécessite que le module externe split() fonctionne correctement.
>
>Le nom du module externe de support doit également être ajouté au fichier **js.txt**.
