---
title: Modifier les propriétés d’une page de contenu
description: Définissez les propriétés requises pour une page dans Adobe Experience Manager.
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1871'
ht-degree: 61%

---

# Modification des propriétés de page{#editing-page-properties}

Vous pouvez définir les propriétés requises pour une page. Celles-ci peuvent varier selon la nature de la page. Par exemple, certaines pages peuvent être connectées à une Live Copy, tandis que d’autres ne le sont pas, et les informations de la Live Copy deviennent disponibles, le cas échéant.

## Propriétés de page {#page-properties}

Les propriétés sont réparties sur plusieurs onglets.

### De base {#basic}

* **Titre**

  Le titre de la page s’affiche à divers endroits. Par exemple, la liste d’onlget **Sites web** et les vues liste/carte **Sites**.

  Ce champ est obligatoire.

* **Balises**

  Vous pouvez y ajouter ou supprimer des balises de la page en mettant à jour la liste dans la zone de sélection :

   * Après avoir sélectionné une balise, elle est répertoriée sous la zone de sélection. Vous pouvez supprimer une balise de cette liste à l’aide du x.
   * Vous pouvez saisir une nouvelle balise en saisissant son nom dans une zone de sélection vide.

      * La nouvelle balise est créée lorsque vous appuyez sur Entrée.
      * La nouvelle balise s’affiche avec une petite étoile à droite, indiquant qu’il s’agit d’une nouvelle balise.

   * La fonctionnalité de liste déroulante vous permet de sélectionner une balise existante.
   * Un x s’affiche lorsque vous placez le pointeur de la souris sur une entrée de balise dans la zone de sélection, qui peut être utilisé pour supprimer cette balise pour cette page.

  Pour plus d’informations sur les balises, consultez la section [Utilisation des balises](/help/sites-authoring/tags.md).

* **Masquer dans la navigation**

  Indique si la page doit être affichée ou masquée dans la navigation entre les pages du site qui en résulte.

* **Valorisation de marque**

  Appliquez une identité de marque cohérente sur plusieurs pages en ajoutant un rappel à chaque titre de page. Cette fonctionnalité nécessite l’utilisation du composant de page de la version 2.14.0, ou ultérieure, des [composants principaux.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr)

   * **Remplacer** : cochez la case pour définir le slug de marque sur cette page.
      * La valeur est héritée par toutes les pages enfants, à moins que leurs valeurs de **remplacement** ne soient également définies.
   * **Remplacer la valeur** : texte de rappel à ajouter au titre de la page.
      * La valeur est ajoutée au titre de la page après un caractère de barre verticale, par exemple « La Toscane en vélo | Toujours prêt pour le WKND »
* **Titre de la page**

  Titre à utiliser sur la page. Généralement utilisé par les composants de titre. Si rien n’est indiqué, le **titre** est utilisé.

* **Titre de navigation**

  Vous pouvez spécifier un titre distinct à utiliser dans la navigation (par exemple, si vous souhaitez qu’il soit plus concis). Si rien n’est indiqué, le **titre** est utilisé.

* **Sous-titre**

  Sous-titre à utiliser sur la page.

* **Description**

  Votre description de la page, son objectif ou tout autre détail que vous souhaiteriez ajouter.

* **Heure d’activation**

  Date et heure auxquelles la page publiée est activée. Une fois publiée, cette page reste inactive jusqu’à l’heure indiquée.

  Laissez ces champs vides pour les pages que vous souhaitez publier immédiatement (scénario normal).

* **Heure de désactivation**

  Heure à laquelle la page publiée est désactivée.

  Ne renseignez pas ces champs pour une action immédiate.

* **URL Vanity**

  Saisissez une URL Vanity pour cette page, qui peut vous permettre d’avoir une URL plus courte et/ou plus expressive.

  Par exemple, si l’URL de redirection est définie sur `welcome` sur la page identifiée par le chemin `/v1.0/startpage` pour le site Web `http://example.com,`, `http://example.com/welcome` sera l’URL de redirection de `http://example.com/content/v1.0/startpage`.

  >[!CAUTION]
  >
  >URL de redirection :
  >
  >* Doit être unique. Assurez-vous que la valeur n’est pas déjà utilisée par une autre page.
  >* Elles ne prennent pas en charge les modèles d’expression régulière.
  >* ne doit pas être définie sur une page existante.
  >

  Configurez Dispatcher pour activer l’accès aux URL de redirection vers un microsite. Consultez [Activation de l’accès aux URL de redirection](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr#enabling-access-to-vanity-urls-vanity-urls) pour plus d’informations.

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
   * Pour plus d’informations, voir [Noms de page localisés sous Bonnes pratiques de gestion des URL et de l’optimisation pour les moteurs de recherche](/help/managing/seo-and-url-management.md#localized-page-names).

* **Hérité de &lt;*chemin*>**

  Indique si la page est héritée. Indique aussi d’où elle est héritée.

* **Configuration du cloud**

  Chemin d’accès à la configuration.

* **Modèles autorisés**

  [Définir la liste des modèles disponibles](/help/sites-authoring/templates.md#allowingatemplate) dans cette sous-branche.

* **Activer** (exigence d’authentification)

  Activez (ou désactivez) l’utilisation de l’authentification afin d’accéder à la page.

  >[!NOTE]
  >
  >Les groupes d’utilisateurs fermés pour la page sont définis dans l’onglet **[Autorisations](/help/sites-authoring/editing-page-properties.md#permissions)**.

  >[!CAUTION]
  >
  >La variable **[Autorisations](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** permet de modifier les configurations des groupes d’utilisateurs fermés en fonction de la présence de la variable `granite:AuthenticationRequired` mixin. Si les autorisations de page sont configurées à l’aide de configurations de CUG obsolètes, en fonction de la présence de `cq:cugEnabled` , un message d’avertissement s’affiche sous **Exigence d’authentification** et l’option n’est pas modifiable, pas plus que le [Autorisations](/help/sites-authoring/editing-page-properties.md#permissions) modifiable.
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

  Générez un aperçu de la page que vous souhaitez utiliser comme miniature.

* **Charger l’image**

  Téléchargez une image que vous souhaitez utiliser comme miniature.

* **Sélectionner une image**

  Sélectionnez une ressource existante que vous souhaitez utiliser comme miniature.

* **Rétablir**

  Cette option devient disponible une fois que vous avez modifié la miniature. Si vous ne souhaitez pas conserver votre modification, vous pouvez l’annuler avant d’enregistrer.

### Réseaux sociaux {#social-media}

* **Partage sur les réseaux sociaux**

  Définit les options de partage disponibles sur la page. Expose les options disponibles pour la variable [Partage du composant principal](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/sharing.html?lang=en).

   * **Activer le partage utilisateur/utilisatrice pour Facebook**
   * **Activer le partage utilisateur/utilisatrice pour Pinterest**
   * **Variation de fragment d’expérience préférée**
Définition de la variation de fragment d’expérience utilisée pour générer des métadonnées pour une page

### Services cloud {#cloud-services}

* **Services cloud**

  Définissez des propriétés pour les [services cloud](/help/sites-developing/extending-cloud-config.md).

### Personnalisation {#personalization}

* **Configurations ContextHub**

  Sélectionnez la [configuration ContextHub](/help/sites-developing/ch-configuring.md) et le [chemin d’accès des segments](/help/sites-administering/segmentation.md).

* **Configuration du ciblage**

  Sélectionnez une [marque pour spécifier la portée du ciblage](/help/sites-authoring/target-adobe-campaign.md).

  >[!NOTE]
  >Cette option nécessite que le compte d’utilisateur figure dans le groupe `Target Adminstrators`.

### Autorisations {#permissions}

* **Autorisations**

  Dans cet onglet, vous pouvez :

   * [Ajouter des autorisations](/help/sites-administering/user-group-ac-admin.md)
   * [Modifier le groupe d’utilisateurs fermé](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * Afficher les [autorisations effectives](/help/sites-administering/user-group-ac-admin.md)

  >[!CAUTION]
  >
  >L’onglet **Autorisations** permet de modifier les configurations des groupes d’utilisateurs fermés basées sur la présence du mixin `granite:AuthenticationRequired`. Si les autorisations de page sont configurées à l’aide de configurations de CUG obsolètes, en fonction de la présence de `cq:cugEnabled` , un message d’avertissement s’affiche et les autorisations de CUG ne sont pas modifiables, de même que l’ exigence d’authentification sur la propriété [Avancé](/help/sites-authoring/editing-page-properties.md#advanced) onglet modifiable.
  >
  >
  >Le cas échéant, les autorisations des groupes d’utilisateurs fermés doivent être modifiées dans l’[IU classique](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

  >[!NOTE]
  >
  >L’onglet Autorisations n’autorise pas la création de groupes d’utilisateurs et d’utilisatrices vides, ce qui peut se révéler utile comme un moyen simple de refuser l’accès à chaque utilisateur et utilisatrice. Pour ce faire, l’Explorateur CRX doit être utilisé. Voir le document [Administration des droits d’utilisateur, de groupe et d’accès](/help/sites-administering/user-group-ac-admin.md) pour plus d’informations.

### Plan directeur {#blueprint}

* **Plan directeur**

  Définissez des propriétés pour une page de plan directeur dans la [gestion multi-sites](/help/sites-administering/msm.md). Contrôle les circonstances dans lesquelles les modifications sont propagées à la Live Copy.

### Live Copy {#live-copy}

* **Live Copy**

  Définissez des propriétés pour une page Live Copy dans la [gestion multi-sites](/help/sites-administering/msm.md). Contrôle les circonstances dans lesquelles les modifications sont propagées à partir du plan directeur.

### Structure du site {#site-structure}

* Fournir des liens vers des pages qui fournissent des fonctionnalités à l’échelle du site, telles que **Page d’inscription**, **Page hors ligne**, entre autres.

## Modification des propriétés de page {#editing-page-properties-1}

Vous pouvez définir les propriétés de page :

* Dans la console **Sites** :

   * [Créer une page](/help/sites-authoring/managing-pages.md#creating-a-new-page) (un sous-ensemble des propriétés)

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

   Les propriétés de la page sont affichées dans les onglets appropriés.

1. Affichez ou modifiez les propriétés selon les besoins.

1. Ensuite, utilisez **Enregistrer** pour enregistrer vos mises à jour, puis **Fermer** pour pouvoir revenir à la console.

### Lors de la modification d’une page {#when-editing-a-page}

Lorsque vous modifiez une page, vous pouvez utiliser **Informations sur la page** pour définir les propriétés de la page :

1. Ouvrez la page dont vous souhaitez modifier les propriétés.

1. Sélectionnez l’icône **Informations sur la page** pour ouvrir le menu de sélection :

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Sélectionner **Ouvrir les propriétés** et une boîte de dialogue s’ouvre pour vous permettre de modifier les propriétés, triées selon l’onglet approprié. Les boutons suivants sont également disponibles à droite de la barre d’outils :

   * **Annuler**
   * **Enregistrez et fermez**

1. Utilisez le bouton **Enregistrer et fermer** pour enregistrer les modifications.

### À partir de la console Sites – Plusieurs pages {#from-the-sites-console-multiple-pages}

Dans la **Sites** console, vous pouvez sélectionner plusieurs pages, puis utiliser **Afficher les propriétés** pour afficher et/ou modifier les propriétés de la page. On parle alors de modification en masse des propriétés de la page.

>[!NOTE]
>
>La modification en masse des propriétés est également disponible pour les ressources. Elle est similaire, mais diffère en quelques points. Pour plus d’informations, voir [Modification des propriétés de plusieurs ressources](/help/assets/metadata.md).
>
>Il y a également la [Éditeur en bloc](/help/sites-administering/bulk-editor.md). Cet éditeur vous permet de rechercher du contenu à partir de plusieurs pages à l’aide du langage de requête Google (GQL), puis de le modifier directement à l’aide de l’éditeur en bloc avant d’enregistrer les modifications dans les pages d’origine.

Vous pouvez sélectionner plusieurs pages à des fins de modification en bloc de différentes manières, notamment :

* lorsque vous parcourez la console **Sites** ;
* après avoir utilisé **Rechercher** pour localiser un ensemble de pages.

![epp-01](assets/epp-01.png)

Après avoir sélectionné les pages, puis cliqué ou appuyé sur l’option **Propriétés**, les propriétés en bloc s’affichent :

![epp-02](assets/epp-02.png)

Vous ne pouvez modifier en masse que des pages qui :

* Partagent le même type de ressource.
* Ne font pas partie d’une Live Copy.

   * Si l’une de ces pages fait partie d’une Live Copy, un message s’affiche lorsque les propriétés sont ouvertes.

Une fois que vous avez saisi l’option Modification en bloc, vous pouvez effectuer les opérations suivantes :

* **Mode**

  Lors de l’affichage des propriétés de page pour plusieurs pages, vous pouvez voir les éléments suivants :

   * Liste des pages affectées

      * Vous pouvez, au besoin, sélectionner/désélectionner

   * Onglets

      * Comme pour l’affichage des propriétés d’une seule page, les propriétés sont classées sous les onglets.

   * Un sous-ensemble de propriétés

      * Les propriétés qui sont disponibles sur toutes les pages sélectionnées, et qui ont été définies explicitement comme étant disponibles pour la modification en masse, sont visibles.
      * Si vous réduisez la sélection à une seule page, toutes les propriétés sont alors visibles.

   * Propriétés communes partageant une valeur commune

      * Seules les propriétés qui partagent une valeur commune sont visibles en mode Affichage.
      * Lorsque le champ comporte plusieurs valeurs (Balises, par exemple), les valeurs ne sont visibles que lorsque *all* sont courantes. Si seulement certains d’entre eux sont communs, ils s’affichent uniquement lors de la modification.

  En l’absence de propriétés avec une valeur commune, un message s’affiche.

* **Modifier**

  Lors de la modification des propriétés de page pour plusieurs pages :

   * Vous pouvez mettre à jour les valeurs dans les champs disponibles.

      * Les nouvelles valeurs sont appliquées à toutes les pages sélectionnées lorsque vous appuyez sur **Terminé**.
      * Lorsque le champ comporte plusieurs valeurs (Balises, par exemple), vous pouvez ajouter une nouvelle valeur ou supprimer une valeur commune.

   * Les champs communs, mais ayant des valeurs différentes sur les différentes pages, sont indiqués par une valeur spéciale, telle que le texte. `<Mixed Entries>`.

>[!NOTE]
>
>Le composant de page peut être configuré pour spécifier les champs disponibles en vue de la modification en bloc. Reportez-vous à la section [Configuration de votre page en vue de la modification en bloc des propriétés](/help/sites-developing/bulk-editing.md).
