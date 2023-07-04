---
title: Modifier les propriétés d’une page de contenu
description: Vous pouvez définir les propriétés requises d’une page.
uuid: d3a2183b-8082-4cfc-aeed-26facbf3f3e6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1e9dd0d7-209a-4989-b66b-bca0d04b437a
docset: aem65
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: ht
source-wordcount: '1885'
ht-degree: 100%

---

# Modification des propriétés de page{#editing-page-properties}

Vous pouvez définir les propriétés requises pour une page. Celles-ci peuvent varier selon la nature de la page. Par exemple, certaines pages peuvent être connectées à une Live Copy alors que d’autres ne le sont pas, et les informations de Live Copy seront disponibles, le cas échéant.

## Propriétés de page {#page-properties}

Les propriétés sont réparties sur plusieurs onglets.

### De base {#basic}

* **Titre**

   Le titre de la page s’affiche à divers endroits. Par exemple, la liste d’onlget **Sites web** et les vues liste/carte **Sites**.

   Ce champ est obligatoire.

* **Balises**

   Vous pouvez ajouter des balises sur la page, ou en supprimer, en mettant à jour la liste dans la zone de sélection :

   * La balise sélectionnée est alors répertoriée sous la zone de sélection. Vous pouvez supprimer une balise de cette liste à l’aide du symbole x.
   * Vous pouvez saisir une nouvelle balise en saisissant son nom dans une zone de sélection vide.

      * La nouvelle balise est créée lorsque vous appuyez sur Entrée.
      * Elle est marquée d’une petite étoile sur la droite indiquant qu’il s’agit d’une nouvelle balise.
   * Avec la fonctionnalité de liste déroulante, vous pouvez effectuer un choix parmi des balises existantes.
   * Un x s’affiche lorsque vous placez le pointeur de la souris sur une entrée de balise dans la zone de sélection, qui peut être utilisé pour supprimer cette balise pour cette page.

   Pour plus d’informations sur les balises, consultez la section [Utilisation des balises](/help/sites-authoring/tags.md).

* **Masquer dans la navigation**

   Indique si la page doit être affichée ou masquée dans la navigation entre les pages du site qui en résulte.

* **Valorisation de marque**

   Appliquez une identité de marque cohérente sur plusieurs pages en ajoutant un rappel à chaque titre de page. Cette fonctionnalité nécessite l’utilisation du composant de page de la version 2.14.0, ou ultérieure, des [composants principaux.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr)

   * **Remplacer** : cochez la case pour définir le titre de rappel sur cette page.
      * La valeur sera héritée par toutes les pages enfants à moins que leurs valeurs de **remplacement** ne soient également définies.
   * **Remplacer la valeur** : texte de rappel à ajouter au titre de la page.
      * La valeur est ajoutée au titre de la page après un caractère de barre verticale, par exemple « La Toscane en vélo | Toujours prêt pour le WKND »
* **Titre de la page**

   Titre à utiliser sur la page. Généralement utilisé par les composants de titre. Si le champ est vide, le **Titre** sera utilisé.

* **Titre de navigation**

   Vous pouvez spécifier un titre distinct à utiliser dans la navigation (par exemple, si vous souhaitez qu’il soit plus concis). Si le champ est vide, le **Titre** sera utilisé.

* **Sous-titre**

   Sous-titre à utiliser sur la page.

* **Description**

   Votre description de la page, son objectif ou tout autre détail que vous souhaiteriez ajouter.

* **Heure d’activation**

   Date et heure auxquelles la page publiée sera activée. Une fois publiée, cette page restera dormante jusqu’à l’heure indiquée.

   Laissez ces champs vides pour les pages que vous souhaitez publier immédiatement (scénario normal).

* **Heure de désactivation**

   Heure à laquelle la page publiée sera désactivée.

   Ne renseignez pas ces champs pour une action immédiate.

* **URL Vanity**

   Elle vous permet de saisir une URL Vanity pour cette page, ce qui peut vous permettre d’avoir une URL plus courte ou plus expressive.

   Par exemple, si l’URL de redirection est définie sur `welcome` sur la page identifiée par le chemin `/v1.0/startpage` pour le site Web `http://example.com,`, `http://example.com/welcome` sera l’URL de redirection de `http://example.com/content/v1.0/startpage`.

   >[!CAUTION]
   >
   >L’URL Vanity :
   >
   >* doit être unique. Vous devez donc veiller à ce que la valeur ne soit pas déjà utilisée par une autre page.
   >* Elles ne prennent pas en charge les modèles d’expression régulière.
   >* ne doit pas être définie sur une page existante.


   Vous devez également configurer le Dispatcher pour activer l’accès aux URL de redirection. Consultez [Activation de l’accès aux URL de redirection](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr#enabling-access-to-vanity-urls-vanity-urls) pour plus d’informations.

* **Rediriger l’URL Vanity**

   Indique si vous souhaitez que la page utilise l’URL Vanity.

### Avancé {#advanced}

* **Langue**

   Langue de la page.

* **Racine de la langue**

   Cette option doit être cochée si la page est la racine d’une copie de langue.

* **Rediriger**

   Indiquez la page vers laquelle cette page doit rediriger automatiquement.

* **Conception**

   Indiquez la [conception](/help/sites-developing/designer.md) à utiliser pour cette page.

* **Alias**

   Indiquez un alias à utiliser pour cette page.

   * Par exemple, si vous définissez l’alias de `private` pour la page `/content/wknd/us/en/magazine/members-only`, alors cette page est également accessible via `/content/wknd/us/en/magazine/private`.
   * La création d’un alias permet de définir la propriété `sling:alias` sur le nœud de page, ce qui affecte uniquement la ressource, et non le chemin d’accès au référentiel.
   * Les pages accessibles par alias dans l’éditeur ne peuvent pas être publiées. Les [options de publication](/help/sites-authoring/publishing-pages.md) dans l’éditeur ne sont disponibles que pour les pages auxquelles vous pouvez accéder à partir de leur chemin d’accès réel.
   * Pour plus d’informations, consultez [Noms de page localisés dans les Bonnes pratiques de SEO et de gestion des URL](/help/managing/seo-and-url-management.md#localized-page-names).

* **Hérité de &lt;*chemin*>**

   Indique si la page est héritée. Indique aussi d’où elle est héritée.

* **Configuration du cloud**

   Chemin d’accès à la configuration.

* **Modèles autorisés**

   [Définit la liste des modèles qui seront disponibles](/help/sites-authoring/templates.md#allowingatemplate) dans cette sous-branche.

* **Activer** (exigence d’authentification)

   Active/désactive l’utilisation de l’authentification pour accéder à la page.

   >[!NOTE]
   >
   >Les groupes d’utilisateurs fermés pour la page sont définis dans l’onglet **[Autorisations](/help/sites-authoring/editing-page-properties.md#permissions)**.

   >[!CAUTION]
   >
   >L’onglet **[Autorisations](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** permet de modifier les configurations des groupes d’utilisateurs fermés basées sur la présence du mixin `granite:AuthenticationRequired`. Si les autorisations de page sont configurées à l’aide de configurations des groupes d’utilisateurs fermés obsolètes, selon la présence de la propriété `cq:cugEnabled`, un message d’avertissement s’affiche sous **Exigence d’authentification** et l’option n’est pas modifiable, tout comme les [autorisations](/help/sites-authoring/editing-page-properties.md#permissions).
   >
   >
   >Le cas échéant, les autorisations des groupes d’utilisateurs fermés doivent être modifiées dans l’[IU classique](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **Page de connexion**

   La page à utiliser pour se connecter.

* **Exporter la configuration**

   Indiquez une configuration d’exportation.

### Miniature  {#thumbnail}

Affiche l’image miniature de la page. Vous pouvez :

* **Générer l’aperçu**

   Générez un aperçu de la page à utiliser comme miniature.

* **Charger l’image**

   Chargez une image à utiliser comme miniature.

* **Sélectionner une image**

   Sélectionnez une ressource existante à utiliser comme miniature.

* **Rétablir**

   Cette option n’est disponible qu’après avoir effectué une modification de la vignette. Si vous ne souhaitez pas conserver votre modification, vous pouvez l’annuler avant d’enregistrer.

### Réseaux sociaux {#social-media}

* **Partage sur les réseaux sociaux**

   Définit les options de partage disponibles sur la page. Expose les options disponibles pour le [composant principal de partage](https://helpx.adobe.com/fr/experience-manager/core-components/using/sharing.html).

   * **Activer le partage utilisateur/utilisatrice pour Facebook**
   * **Activer le partage utilisateur/utilisatrice pour Pinterest**
   * **Variation de fragment d’expérience préférée**
Définit la variation de fragment d’expérience utilisée pour générer les métadonnées de la page.

### Services cloud {#cloud-services}

* **Services cloud**

   Définissez des propriétés pour les [services cloud](/help/sites-developing/extending-cloud-config.md).

### Personnalisation {#personalization}

* **Configurations ContextHub**

   Sélectionnez la [configuration ContextHub](/help/sites-developing/ch-configuring.md) et le [chemin d’accès des segments](/help/sites-administering/segmentation.md).

* **Configuration du ciblage**

   Sélectionnez une [marque pour spécifier la portée du ciblage](/help/sites-authoring/target-adobe-campaign.md).

   >[!NOTE]
   >Cette option nécessite que le compte utilisateur figure dans le groupe `Target Adminstrators`.

### Autorisations {#permissions}

* **Autorisations**

   Dans cet onglet, vous pouvez :

   * [Ajouter des autorisations](/help/sites-administering/user-group-ac-admin.md)
   * [Modifier le groupe d’utilisateurs fermé](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * Afficher les [autorisations effectives](/help/sites-administering/user-group-ac-admin.md)
   >[!CAUTION]
   >
   >L’onglet **Autorisations** permet de modifier les configurations des groupes d’utilisateurs fermés basées sur la présence du mixin `granite:AuthenticationRequired`. Si les autorisations de page sont configurées à l’aide de configurations de groupes d’utilisateurs fermés obsolètes, basées sur la présence de la propriété `cq:cugEnabled`, un message d’avertissement s’affiche et les autorisations des groupes d’utilisateurs fermés ne sont pas modifiables, tout comme l’option Exigence d’authentification de l’onglet [Avancé](/help/sites-authoring/editing-page-properties.md#advanced).
   >
   >
   >Le cas échéant, les autorisations des groupes d’utilisateurs fermés doivent être modifiées dans l’[IU classique](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

   >[!NOTE]
   >
   >L’onglet Autorisations n’autorise pas la création de groupes d’utilisateurs et d’utilisatrices vides, ce qui peut se révéler utile comme un moyen simple de refuser l’accès à chaque utilisateur et utilisatrice. Pour ce faire, utilisez l’Explorateur CRX. Pour plus d’informations, consultez le document [Administration des utilisateurs, des groupes et des droits d’accès](/help/sites-administering/user-group-ac-admin.md).

### Plan directeur {#blueprint}

* **Plan directeur**

   Définissez des propriétés pour une page de plan directeur dans la [gestion multi-sites](/help/sites-administering/msm.md). Détermine les circonstances dans lesquelles les modifications seront diffusées à la Live Copy.

### Live Copy  {#live-copy}

* **Live Copy**

   Définissez des propriétés pour une page Live Copy dans la [gestion multi-sites](/help/sites-administering/msm.md). Détermine les circonstances dans lesquelles les modifications seront propagées à partir du plan directeur.

### Structure du site  {#site-structure}

* Diffusez des liens d’accès aux pages qui fournissent les fonctionnalités à l’échelle du site, comme la **page d’inscription** et la page **en mode hors ligne**, entre autres.

## Modification des propriétés de page {#editing-page-properties-1}

Vous pouvez définir les propriétés de page :

* Dans la console **Sites** :

   * [En créant une page](/help/sites-authoring/managing-pages.md#creating-a-new-page) (sous-ensemble des propriétés)

   * En cliquant ou en appuyant sur **Propriétés**

      * Pour une seule page
      * Pour plusieurs pages (seul un sous-ensemble des propriétés peut être modifié en masse)

* À partir de l’éditeur de page :

   * En sélectionnant **Informations sur la page** (puis **Ouvrir les propriétés**)

### À partir de la console Sites – Une seule page {#from-the-sites-console-single-page}

Cliquez ou appuyez sur **Propriétés** pour définir les propriétés de la page :

1. Dans la console **Sites**, accédez à l’emplacement de la page pour laquelle afficher et modifier les propriétés.

1. Sélectionnez l’option **Propriétés** pour la page requise, en utilisant :

   * [Actions rapides](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Mode de sélection](/help/sites-authoring/basic-handling.md#selectionmode)

   Les propriétés de la page affichées dans les onglets appropriés.

1. Affichez ou modifiez les propriétés selon les besoins.

1. Puis cliquez sur **Enregistrer** pour enregistrer vos modifications et sur **Fermer** pour revenir à la console.

### Lors de la modification d’une page {#when-editing-a-page}

Lorsque vous modifiez une page, utilisez les **Informations sur la page** pour définir ses propriétés :

1. Ouvrez la page dont vous souhaitez modifier les propriétés.

1. Sélectionnez l’icône **Informations sur la page** pour ouvrir le menu de sélection :

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Sélectionnez **Ouvrir les propriétés**. Une boîte de dialogue s’ouvre alors pour vous permettre de modifier les propriétés, triées selon l’onglet approprié. Les boutons suivants sont également disponibles à droite de la barre d’outils :

   * **Annuler**
   * **Enregistrez et fermez**

1. Utilisez le bouton **Enregistrer et fermer** pour enregistrer les modifications.

### À partir de la console Sites – Plusieurs pages {#from-the-sites-console-multiple-pages}

Dans la console **Sites**, vous pouvez sélectionner plusieurs pages, puis utiliser **Afficher les propriétés** pour afficher et/ou modifier les propriétés de la page. On parle alors de modification en masse des propriétés de la page.

>[!NOTE]
>
>La modification en masse des propriétés est également disponible pour les ressources. La procédure est très semblable. Seuls quelques points sont différents. Pour plus d’informations, voir [Modification des propriétés de plusieurs ressources](/help/assets/metadata.md).
>
>Il existe également un [Éditeur en bloc](/help/sites-administering/bulk-editor.md) qui vous permet de rechercher du contenu provenant de plusieurs pages à l’aide du langage GQL (Google Query Language), puis de le modifier directement avant d’enregistrer les modifications dans les pages d’origine.

Vous pouvez sélectionner plusieurs pages à des fins de modification en bloc de différentes manières, notamment :

* lorsque vous parcourez la console **Sites** ;
* après avoir utilisé **Rechercher** pour localiser un ensemble de pages.

![epp-01](assets/epp-01.png)

Sélectionnez les pages et cliquez ou appuyez ensuite sur l’option **Propriétés** pour afficher les propriétés en bloc :

![epp-02](assets/epp-02.png)

Vous ne pouvez modifier en masse que des pages qui :

* Partagent le même type de ressource.
* Ne font pas partie d’une Live Copy.

   * Si l’une de ces pages fait partie d’une Live Copy, un message s’affiche lorsque les propriétés sont ouvertes.

Une fois le mode de modification en bloc activé, vous pouvez effectuer les opérations suivantes :

* **Mode**

   Lorsque vous affichez les propriétés de page pour plusieurs pages, vous pouvez voir les éléments suivants :

   * Liste des pages affectées

      * Vous pouvez sélectionner/désélectionner si nécessaire.
   * Onglets

      * Comme pour l’affichage des propriétés d’une seule page, les propriétés sont classées sous les onglets.
   * Un sous-ensemble de propriétés

      * Les propriétés qui sont disponibles sur toutes les pages sélectionnées, et qui ont été définies explicitement comme étant disponibles pour la modification en masse, sont visibles.
      * Si vous réduisez la sélection à une seule page, toutes les propriétés sont alors visibles.
   * Propriétés communes partageant une valeur commune

      * Seules les propriétés qui partagent une valeur commune sont visibles en mode Affichage.
      * Si le champ comporte plusieurs valeurs (Balises, par exemple), les valeurs ne sont visibles que lorsque *toutes* sont communes. Si seulement quelques-unes sont communes, elles sont visibles lors de la phase de modification.

   En l’absence de propriétés avec une valeur commune, un message s’affiche.

* **Modifier**

   Lors de la modification des propriétés de page pour plusieurs pages :

   * Vous pouvez mettre à jour les valeurs dans les champs disponibles.

      * Les nouvelles valeurs sont appliquées à toutes les pages sélectionnées lorsque vous appuyez sur **Terminé**.
      * Lorsque le champ comporte plusieurs valeurs (des balises, par exemple), vous pouvez ajouter une nouvelle valeur ou supprimer une valeur commune.
   * Les champs qui sont communs, mais pour lesquels des valeurs différentes sont renseignées dans les différentes pages, sont signalés par une valeur spéciale, par exemple par le texte `<Mixed Entries>`.


>[!NOTE]
>
>Le composant de page peut être configuré pour spécifier les champs disponibles en vue de la modification en bloc. Reportez-vous à la section [Configuration de votre page en vue de la modification en bloc des propriétés](/help/sites-developing/bulk-editing.md).
