---
title: Utiliser le traducteur pour gérer les dictionnaires
description: AEM fournit une console pour gérer les différentes traductions des textes utilisés dans l'interface utilisateur des composants.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: a8d50c09-72d0-406e-874e-50a985227a56
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 98%

---

# Utiliser le traducteur pour gérer les dictionnaires{#using-translator-to-manage-dictionaries}

AEM fournit une console pour gérer les différentes traductions des textes utilisés dans l&#39;interface utilisateur des composants. Cette console est disponible à l’adresse

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

Utilisez l’outil Traducteur pour gérer les chaînes de caractères anglaises, ainsi que leurs traductions. Les dictionnaires sont créés dans le référentiel ; par exemple /apps/myproject/i18n.

L&#39;outil Traducteur et les dictionnaires que vous gérez servent à présenter l&#39;interface utilisateur des composants dans différentes langues. Si vous souhaitez traduire une page ou du contenu généré par des utilisateurs ou des utilisatrices, consultez [Traduction de contenu pour des sites multilingues](/help/sites-administering/translation.md) et [Traduction de contenu généré par les utilisateurs et les utilisatrices](/help/communities/translate-ugc.md).

>[!CAUTION]
>
>Ne modifiez que les dictionnaires qui sont créés pour votre projet et qui résident sous `/apps`.
>
>Les dictionnaires système d’AEM sont également disponibles dans cet outil. Ne modifiez pas les dictionnaires système d’AEM, car cela pourrait entraîner des problèmes avec l’interface utilisateur d’AEM. De plus, les modifications peuvent être perdues lors d’une mise à niveau. Les dictionnaires système AEM sont situés sous `/libs`.

>[!NOTE]
>
>Bien que l’outil Traducteur possède une interface utilisateur classique, il est utilisé pour traduire des expressions, quelle que soit l’interface où se trouvent celles-ci.

Le traducteur répertorie les textes utilisés dans AEM avec les diverses traductions correspondantes :

![chlimage_1-205](assets/chlimage_1-205.png)

Vous pouvez rechercher, filtrer et modifier les textes en anglais et les textes traduits. Vous pouvez également exporter des dictionnaires au format XLIFF pour les traduire, puis importer les traductions dans ces mêmes dictionnaires.

Il est également possible d&#39;ajouter les dictionnaires i18n à un projet de traduction depuis cette console. Vous pouvez soit en créer un, soit l&#39;ajouter à un projet existant.

1. Cliquez sur **Traduire le dictionnaire**.

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. Sélectionnez l’option Créer ou Ajouter selon vos besoins. Une boîte de dialogue s’ouvre.

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. Renseignez les champs suivant les besoins et cliquez ensuite sur OK. ![chlimage_1-208](assets/chlimage_1-208.png)

1. Vous pouvez à présent cliquer sur **OK** ou consulter le dictionnaire cible.

   >[!NOTE]
   >
   >Pour plus d&#39;informations sur les projets de traduction, consultez [Gestion des projets de traduction](/help/sites-administering/tc-manage.md).

## Création d’un dictionnaire {#creating-a-dictionary}

Créez un dictionnaire pour gérer vos chaînes d’interface utilisateur localisées. Après avoir créé un dictionnaire, vous pouvez utiliser l’outil de traduction pour le gérer.

1. À l’aide de CRXDE Lite, ajoutez le nœud racine (`sling:Folder`) de votre nouveau dictionnaire comme structure de stockage des définitions de langue :

   ` /apps/<projectName>/i18n`

   Par exemple, `/apps/myProject/i18n`

1. Ajoutez la structure de langues requise sous ce nœud : Par exemple :

   ```shell
   /apps/myProject/i18n [sling:Folder]
       - de.json [nt:file] [mix:language]
           + jcr:language = de
       - fr.json [nt:file] [mix:language]
           + jcr:language = fr
   ```

   >[!NOTE]
   >
   >Il s’agit de la structure du [module Sling i18n](https://sling.apache.org/site/internationalization-support.html).

1. Rechargez le traducteur. Le chemin d’accès au dictionnaire (`/apps/myProject/i18n`) devient disponible dans le sélecteur déroulant de la barre d’outils. Sélectionnez-le pour commencer à ajouter des chaînes et leurs traductions.

   >[!NOTE]
   >
   >Le traducteur enregistre uniquement les traductions pour les langues présentes dans le chemin d’accès (`/apps/myProject/i18n`, par exemple).
   >
   >Vérifiez que ces langues correspondent à celles affichées dans la grille.

## Gestion des chaînes de dictionnaire {#managing-dictionary-strings}

Utilisez l’outil de traduction pour gérer les chaînes dans vos dictionnaires. Vous pouvez ajouter, modifier et supprimer des chaînes de caractères anglaises et également fournir des chaînes traduites.

>[!CAUTION]
>
>Ne modifiez que les dictionnaires qui sont créés pour votre projet et qui résident sous `/apps`.
>
>Ne modifiez pas les dictionnaires système d’AEM, car cela pourrait entraîner des problèmes avec l’interface utilisateur d’AEM. De plus, les modifications peuvent être perdues lors d’une mise à niveau. Les dictionnaires système AEM sont situés sous `/libs`.

### Ajout, modification et suppression de chaînes {#adding-changing-and-removing-strings}

Ajoutez des chaînes en anglais à un dictionnaire que votre composant a internationalisées. Ajoutez uniquement des chaînes internationalisées afin de ne pas gaspiller de ressources en traduisant des chaînes qui ne sont pas utilisées.

Les chaînes que vous ajoutez à un dictionnaire doivent correspondre exactement à la chaîne spécifiée dans le code. Si la chaîne en anglais par défaut utilisée dans le code ne correspond pas à la chaîne en anglais d’un dictionnaire, la chaîne traduite n’apparaît pas dans l’interface utilisateur, le cas échéant. Les chaînes respectent la casse.

**Fournir des conseils de traduction**

Utilisez la propriété Commentaire de la chaîne du dictionnaire pour fournir des informations au traducteur ou à la traductrice afin de clarifier la signification de la chaîne. En règle générale, l&#39;interface utilisateur aide les utilisateurs et les utilisatrices à déterminer la signification des mots ambigus. Cependant, le traducteur ou la traductrice ne voit pas la chaîne dans le contexte de l’interface utilisateur. Le conseil de traduction supprime l’ambiguïté. Par exemple, un commentaire aide le traducteur à comprendre que le terme anglais « Request » est utilisé comme substantif et non comme verbe.

Les conseils de traduction distinguent également les chaînes identiques et celles ayant des significations différentes. Par exemple, le mot « Search » peut être un nom ou un verbe, nécessitant deux entrées « Search » dans le dictionnaire avec deux conseils de traduction différents. Le code qui appelle la chaîne inclut également le conseil de traduction afin que la chaîne correcte soit utilisée dans l’interface utilisateur.

**Inclusion de variables indexées**

Incluez des variables dans la chaîne localisée pour créer un contexte de signification dans une phrase. Par exemple, après vous être connecté à une application Web, la page d’accueil affiche le message « Bienvenue, Administrateur ou Administratrice. Vous avez 2 nouveaux messages dans votre boîte de réception ». Le contexte de la page détermine le nom de l’utilisateur ou de l’utilisatrice et le nombre de messages.

Pour inclure des variables dans la chaîne localisée, placez des index entre accolades à l’emplacement des variables dans le premier argument de la méthode get. Utilisez l’indice de localisation pour décrire les valeurs. Le traducteur doit comprendre la signification des variables car les structures de phrase varient en fonction de la langue.

Notez que le [code qui demande la chaîne traduite](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) fournit des valeurs pour les variables indexées en fonction du contexte.

Par exemple, la chaîne suivante s’affiche lorsqu’un utilisateur se connecte à un site web, et est incluse dans le dictionnaire :

`Welcome back {0}. You have {1} messages.`

Le commentaire suivant décrit les variables :

`{0} = the user name, {1} = the number of items in the user's inbox`

**Modification de chaînes**

Modifiez ou supprimez des chaînes en anglais lorsqu’elles sont modifiées ou supprimées dans le code. Lorsque vous modifiez une chaîne, la chaîne d’origine est conservée et une nouvelle chaîne est créée pour refléter la modification. Avant de supprimer une chaîne, assurez-vous qu’aucun code ne l’utilise.

Suivez la procédure ci-après pour ajouter une chaîne.

1. Dans le menu déroulant Dictionnaires, sélectionnez le dictionnaire auquel vous ajoutez une chaîne. Dans le menu déroulant, les dictionnaires sont représentés par leur chemin d’accès dans le référentiel.
1. Au-dessus du tableau Chaînes et traductions, cliquez sur Ajouter.

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. Dans la zone Chaîne de la boîte de dialogue Ajouter une chaîne, saisissez la chaîne en anglais. Dans la zone Commentaire, saisissez un conseil de traduction pour le traducteur ou la traductrice le cas échéant.
1. Cliquez sur OK.
1. Cliquez sur Enregistrer.

   ![chlimage_1-210](assets/chlimage_1-210.png)

Suivez la procédure ci-après pour modifier une chaîne dans un dictionnaire.

1. Dans le menu déroulant Dictionnaires, sélectionnez le dictionnaire contenant la chaîne à modifier.
1. Double-cliquez sur la chaîne à modifier.
1. Dans la boîte de dialogue Modifier la chaîne, sélectionnez Modifier la chaîne ou le commentaire (cela crée une copie).

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. Modifiez la chaîne ou le commentaire et cliquez sur OK.
1. Cliquez sur Enregistrer.

   ![chlimage_1-212](assets/chlimage_1-212.png)

Suivez la procédure ci-après pour supprimer une chaîne d&#39;un dictionnaire.

1. Dans le menu déroulant Dictionnaires, sélectionnez le dictionnaire contenant la chaîne à supprimer.
1. Cliquez sur Supprimer.

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. Cliquez sur Enregistrer.

   ![chlimage_1-214](assets/chlimage_1-214.png)

### Recherche de chaînes {#searching-for-strings}

La barre de recherche en bas de l’outil de traduction fournit des options de sélection de chaînes :

* **Filtre par texte** : motif à faire correspondre à la chaîne, au commentaire ou aux traductions de langue anglaise. Seuls les éléments qui correspondent à l’ensemble ou à une partie du schéma s’affichent dans le tableau.
* **Modifications : Tous, Modifié, Nouveau, Supprimé** : affiche les éléments qui ont été modifiés, mais pas enregistrés.

   * Tous : affiche les éléments qui ont été modifiés, ajoutés ou supprimés.
   * Modifié : affiche les éléments modifiés.
   * Nouveau : affiche les éléments ajoutés.
   * Supprimé : affiche les éléments qui doivent être supprimés.
   * Sélections multiples : affiche les éléments qui possèdent toutes les propriétés sélectionnées.

* **Contient un commentaire** : affiche les éléments contenant des commentaires pour les traducteurs et les traductrices.
* **Traductions manquantes** : affiche les éléments pour lesquels il n’existe pas de traduction pour au moins une langue.

![chlimage_1-215](assets/chlimage_1-215.png)

1. Dans la barre de recherche, sélectionnez les options de filtrage.
1. Pour filtrer à l&#39;aide des options, cliquez sur Filtrer.
1. Pour supprimer les filtres et voir tous les éléments du dictionnaire, cliquez sur Effacer.

### Modification de chaînes traduites {#editing-translated-strings}

Après avoir ajouté la chaîne en anglais à un dictionnaire, vous pouvez ajouter des traductions de cette chaîne. Vous pouvez également [export du dictionnaire](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) pour le faire traduire par un tiers.

1. Sélectionnez le [dictionnaire spécifique à votre projet](#creating-a-dictionary), car il spécifie le chemin dans le référentiel qui contient les traductions. Par exemple, sélectionnez des **Dictionnaires** tels que :

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >Ne modifiez que les dictionnaires qui sont créés pour votre projet et qui résident sous `/apps`.
   >
   >Les dictionnaires système d’AEM sont également disponibles dans cet outil. Ne modifiez pas les dictionnaires système d’AEM, car cela pourrait entraîner des problèmes avec l’interface utilisateur d’AEM. De plus, les modifications peuvent être perdues lors d’une mise à niveau. Les dictionnaires système AEM sont situés sous `/libs`.

1. Pour modifier les textes traduits pour l’une des chaînes, vous pouvez effectuer l’une des opérations suivantes :

   * Double-cliquez sur la langue adéquate de la chaîne requise pour modifier ce texte :

   ![chlimage_1-216](assets/chlimage_1-216.png)

   * Double-cliquez sur le champ **Chaîne** ou le champ **Commentaire** de la chaîne requise pour ouvrir la boîte de dialogue **Modifier la chaîne**. Modifiez les traductions le cas échéant, puis cliquez sur **OK** pour fermer la boîte de dialogue :

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Cliquez sur **Enregistrer** pour valider vos modifications.

   >[!NOTE]
   >
   >Si vous cliquez sur **Réinitialiser et Actualiser** (au lieu d’**Enregistrer**), les textes précédents sont rétablis.

## Utilisation de traducteurs tiers {#using-third-party-translators}

Pour prendre en charge l’utilisation de services de traduction tiers, l’outil de traduction vous permet d’exporter et d’importer des dictionnaires.

### Exportation d’un dictionnaire {#exporting-a-dictionary}

Exportez un dictionnaire vers un fichier XLIFF pour permettre à un service tiers de traduire les chaînes du dictionnaire.

* Exportez un dictionnaire et incluez les termes en anglais et les termes traduits dans une langue donnée.
* Exportez une partie ou la totalité des chaînes en anglais uniquement.

Lorsque vous exportez un fichier XLIFF et incluez une langue, la structure des nœuds du dictionnaire dans le référentiel doit inclure cette langue. Si la langue n’est pas incluse, cela entraîne des erreurs. Par exemple, pour exporter le fichier XLIFF français, le dossier de dictionnaire doit inclure le nœud enfant `mix:language` nommé `fr` (Voir [Création d’un dictionnaire](/help/sites-developing/i18n-translator.md#creating-a-dictionary)).

Procédez comme suit pour exporter un fichier XLIFF pour une langue donnée.

1. Ouvrez l’outil de traduction `http://<host>:<port>/libs/cq/i18n/translator.html`.
1. Utilisez le menu déroulant Dictionnaires pour sélectionner le dictionnaire à exporter.
1. Cliquez sur Exporter > Exporter complètement les options Xliff *XX*, où *XX* est le code de langue à deux lettres tel que DE ou FR.

   Le fichier XLIFF s’ouvre dans un nouvel onglet ou une nouvelle fenêtre.

1. Utilisez les commandes du navigateur web pour enregistrer la page en tant que fichier sur votre système de fichiers, par exemple Fichier > Enregistrer la page sous.

Utilisez la procédure suivante pour exporter tout ou partie uniquement des chaînes anglaises.

1. Ouvrez l’outil de traduction `http://<host>:<port>/libs/cq/i18n/translator.html`. 
1. Utilisez le menu déroulant Dictionnaires pour sélectionner le dictionnaire à exporter.
1. Si vous exportez un sous-ensemble de chaînes, sélectionnez les éléments du dictionnaire à exporter. La sélection d’aucun élément exporte tous les éléments.
1. Cliquez sur Exporter > Exporter la sélection au format Xliff (chaînes uniquement).
1. Dans la boîte de dialogue qui apparaît, copiez le texte et collez-le dans un fichier texte.

### Importer un dictionnaire {#importing-a-dictionary}

Importez un fichier XLIFF dans un dictionnaire pour remplir le dictionnaire. Lorsque le dictionnaire inclut une traduction pour une chaîne anglaise et que le fichier XLIFF contient une traduction différente pour la même chaîne, la traduction du dictionnaire est remplacée.

1. Ouvrez l’outil de traduction `http://<host>:<port>/libs/cq/i18n/translator.html`.
1. Cliquez sur Importer > Traductions XLIFF.
1. Sélectionnez le fichier à importer et cliquez sur OK.

## Gérer les langues prises en charge {#managing-supported-lanuages}

Ajoutez ou supprimez des langues prises en charge par l’outil de traduction et fournies aux utilisateurs et utilisatrices de vos pages web.

### Modifier les langues répertoriées dans le tableau du dictionnaire {#changing-languages-listed-in-the-dictionary-table}

Les langues suivantes sont reprises dans le tableau de dictionnaire de l’outil Traducteur :

* de - Allemand
* fr - Français
* it - Italien
* es - Espagnol
* ja - Japonais
* pt-br - Portugais brésilien
* zh-cn - Chinois simplifié
* zh-tw - Chinois traditionnel (support limité)
* ko-kr - Coréen

Utilisez la procédure suivante pour ajouter ou supprimer des langues.

1. À l’aide de CRXDE Lite, créez un nœud :

   `/etc/languages`

1. Sur ce nœud, créez une propriété :

   * **Nom** : `languages`
   * **Type** : `Multi-String`
   * **Valeur** : la liste des langues que vous souhaitez afficher. Par exemple :

      * fr
      * es

   >[!NOTE]
   >
   >Les codes de langue doivent être en minuscules.

1. Cliquez sur **Enregistrer tout** dans CRXDE Lite, puis rechargez le traducteur. La grille est mise à jour pour afficher les langues définies.

   >[!NOTE]
   >
   >Le traducteur enregistre uniquement les traductions pour les langues qui sont [présentes dans le dictionnaire](#creating-a-dictionary) (c’est-à-dire, dans le chemin d’accès au dictionnaire, comme `/apps/myProject/i18n`).
   >
   >Vérifiez que ces langues correspondent à celles affichées dans la grille.

### Mise à disposition des langues pour les auteurs {#making-languages-available-to-authors}

Une fois que vous avez défini un dictionnaire pour une nouvelle langue de l’instance AEM, vous devez la rendre disponible pour les auteurs (par exemple, dans les **Préférences**) :

1. Pour modifier la liste des langues disponibles dans l’option **Préférences** de la console **Sécurité** :

   1. Créez un recouvrement dans le code de votre application pour :

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. Pour que la langue soit disponible dans les **Préférences** de la console **Sites web**, vous devez apporter les modifications suivantes à votre application :

   1. Créez un recouvrement pour la structure sous :

      `/libs/cq/security/content/tools/userProperties`

   1. Dans le recouvrement, mettez à jour la liste des langues sous :

      `items/common/items /lang/options`

1. Enregistrez tout et rechargez la console appropriée.

### Modifer les noms de langue et les pays par défaut {#changing-language-names-and-default-countries}

Différents pays utilisent la même langue, par exemple les États-Unis, le Royaume-Uni et l’Australie utilisent tous l’anglais. Cette indication est portée par un code qui est composé de la langue et du pays, par exemple `en_GB`, `en_US` et `en_AU`.

Les pays par défaut sont utilisés lors de l’affichage des drapeaux (par exemple, dans la boîte de dialogue de copie de langue), ils sont utilisés pour résoudre le pays pour un code de langue.

>[!NOTE]
>
>Pour les localisations gérées par le traducteur ci-dessus, seule la langue exacte fonctionne. Si la liste déroulante des préférences linguistiques utilise `en_uk`, un dictionnaire `en_uk` doit figurer dans le référentiel.

Pour modifier les définitions par défaut, procédez comme suit :

1. Une liste des langues est stockée sous :

   `/libs/wcm/core/resources/languages`

   Recouvrez-la en la copiant dans :

   `/apps/wcm/core/resources/languages`

   Modifiez ou étendez ensuite la liste. La propriété `defaultCountry` dans un nœud de langue (`ja`, par exemple) doit contenir le code complet (`ja_jp`) qui définit `jp` comme le pays par défaut pour la langue `ja`.

1. Mettez à jour le **gestionnaire de langues WCM CQ**.

   * **Liste des langues** :

     chemin d’accès à la liste des langues dans le référentiel. Définissez-la sur l’emplacement utilisé pour le recouvrement :

     ```
            /apps/wcm/core/resources/languages
     ```

   Vous pouvez effectuer les actions suivantes à l’aide de la console web OSGi :

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## Publier des dictionnaires {#publishing-dictionaries}

Intégrez vos dictionnaires dans le processus de gestion des versions de vos applications AEM. Par exemple, incluez le dictionnaire dans le package de contenu de votre application pour le déploiement sur l’instance de publication. Cette stratégie offre les avantages suivants :

* Des dictionnaires sont disponibles pour les composants dans leur environnement de publication.
* Les modifications apportées aux chaînes de l’interface utilisateur des composants sont déployées avec les traductions mises à jour.

De même, le test des chaînes du dictionnaire doit être effectué dans le cadre du cycle de développement habituel du logiciel.

>[!NOTE]
>
>N’utilisez pas la fonctionnalité de publication ou de réplication standard pour les dictionnaires. Au lieu de cela, les dictionnaires doivent être traités de la même manière que le code et la configuration. Cela inclut l’utilisation du contrôle de code source pour suivre les modifications et l’utilisation de packages de contenu pour appliquer les modifications à l’auteur et à la publication.

>[!NOTE]
>
>Lors de l’utilisation du Dispatcher, vous devez [invalider les pages mises en cache](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/page-invalidate.html) afin d’inclure les nouvelles chaînes de dictionnaire dans les chaînes de composant rendues.
