---
title: Modification des propriétés de page
description: Définissez les propriétés requises pour une page dans Adobe Experience Manager.
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
mini-toc-levels: 2
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '2477'
ht-degree: 100%

---


# Modification des propriétés de page{#editing-page-properties}

Vous pouvez définir les propriétés requises pour une page. Celles-ci peuvent varier selon la nature de la page. Par exemple, certaines pages peuvent être ou non connectées à une Live Copy. Le cas échéant, les informations de Live Copy deviennent disponibles.

## Propriétés de page {#page-properties}

Les propriétés sont réparties sur plusieurs onglets.

### Réglages de base {#basic}

#### Titre et balises {#tile}

* **Titre** : le titre de la page s’affiche à divers endroits.
   * Par exemple, la liste d’onlget **Sites web** et les vues liste/carte **Sites**.
   * Ce champ est obligatoire.
* **Balises** : vous pouvez ajouter des balises sur la page, ou en supprimer, en mettant à jour la liste dans la zone de sélection.
   * Après avoir sélectionné une balise, celle-ci est répertoriée sous la zone de sélection. Vous pouvez supprimer une balise de cette liste à l’aide du x.
   * Vous pouvez saisir une nouvelle balise en saisissant son nom dans une zone de sélection vide.
      * La nouvelle balise est créée lorsque vous appuyez sur Entrée.
      * Elle est marquée d’une petite étoile sur la droite indiquant qu’il s’agit d’une nouvelle balise.
   * La liste déroulante vous permet de choisir parmi des balises existantes.
   * Un x s’affiche lorsque vous placez le pointeur de la souris sur une entrée de balise dans la zone de sélection, qui peut être utilisé pour supprimer cette balise pour cette page.
   * Pour plus d’informations sur les balises, consultez la section [Utilisation des balises.](/help/sites-authoring/tags.md)
* **Masquer dans la navigation** : indique si la page est affichée ou masquée dans la navigation entre les pages du site qui en résulte.

#### Branding {#branding}

Appliquez une identité de marque cohérente sur plusieurs pages en ajoutant un rappel à chaque titre de page. Cette fonctionnalité nécessite l’utilisation du composant de page de la version 2.14.0, ou ultérieure, des [composants principaux.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr)

* **Remplacer** : cochez la case pour définir le slug de marque sur cette page.
   * La valeur est héritée par toutes les pages enfants, à moins que leurs valeurs de **remplacement** ne soient également définies.
* **Remplacer la valeur** : texte de rappel à ajouter au titre de la page.
   * La valeur est ajoutée au titre de la page après une barre verticale telle que `Cycling Tuscany | Always ready for the WKND`

#### Autres titres et descriptions {#more}

* **Titre de la page** : titre à utiliser sur la page.
   * Généralement utilisé par les composants de titre.
   * Si rien n’est indiqué, le **titre** est utilisé.
* **Titre de navigation** : vous pouvez spécifier un titre distinct à utiliser dans la navigation (par exemple, si vous souhaitez qu’il soit plus concis).
   * Si rien n’est indiqué, le **titre** est utilisé.
* **Sous-titre** : sous-titre à utiliser sur la page.
* **Description** : votre description de la page, son objectif ou tout autre détail que vous souhaiteriez ajouter.

#### Heure d’activation/de désactivation {#on-time}

L’heure d’activation/désactivation d’une page est un moyen pratique de masquer temporairement le contenu déjà publié. Le contenu reste sur l’instance de publication lorsque la page est désactivée. La désactivation d’une page ne dépublie pas le contenu.

* **Heure d’activation** – Date et heure auxquelles la page publiée sera rendue visible (rendue) dans l’environnement de publication. La page doit être publiée, soit manuellement, soit par réplication automatique préconfigurée.

   * Si la page est déjà [publiée,](/help/sites-authoring/publishing-pages.md) elle est disponible sur l’instance de publication, mais à l’état inactif (masquée) jusqu’au rendu à l’heure spécifiée. 
   * Si elle n’est pas publiée et [configurée pour la réplication automatique,](/help/sites-deploying/replication.md) la page est automatiquement publiée, puis rendue au moment spécifié.
   * Si elle n’est pas publiée et n’est pas configurée pour la réplication automatique, la page n’est pas publiée automatiquement. Un message 404 s’affiche lors d’une tentative d’accès à la page.

* **Heure de désactivation** : similaire à l’**heure d’activation**, souvent utilisée en combinaison avec cette dernière, définit l’heure à laquelle la page publiée est masquée dans l’environnement de publication.

Laissez ces champs (**Heure d’activation** et **Heure de désactivation**) vides pour les pages que vous souhaitez publier et qui sont disponibles immédiatement dans l’environnement de publication jusqu’à ce qu’elles soient désactivées (scénario normal).

>[!NOTE]
>Si l’**heure d’activation** ou l’**heure de désactivation** est dans le passé et que la réplication automatique est configurée, l’action appropriée est déclenchée immédiatement.

>[!TIP]
>
>Les heures d’activation/de désactivation portent uniquement sur le contenu déjà publié (par voie manuelle ou la réplication automatique). Pour cette raison, les workflows de publication tels que ceux d’approbation de contenu ne sont pas déclenchés par les heures d’activation/de désactivation, et ces dernières n’affectent pas le statut de publication de la page. Pour cette raison, les heures d’activation/de désactivation sont les plus appropriées pour afficher/masquer temporairement du contenu déjà approuvé et publié.
>
>Si vous souhaitez publier du nouveau contenu avec tous les workflows associés ou supprimer entièrement (dépublier) le contenu de votre site, envisagez de procéder à la [gestion de votre instance de publication.](/help/sites-authoring/publishing-pages.md#manage-publication)

#### URL de redirection {#vanity-url}

Saisissez une URL de redirection pour cette page afin d’avoir une URL plus courte ou plus expressive.

Par exemple, si l’URL de redirection est définie sur `welcome` sur la page identifiée par le chemin `/v1.0/startpage` pour le site Web `http://example.com,`, `http://example.com/welcome` sera l’URL de redirection de `http://example.com/content/v1.0/startpage`.

>[!CAUTION]
>
>URL de redirection :
>
>* Doit être unique.
>* Elles ne prennent pas en charge les modèles d’expression régulière.
>* ne doit pas être définie sur une page existante.

Configurez Dispatcher pour activer l’accès aux URL de redirection. Consultez [Activation de l’accès aux URL de redirection](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr#enabling-access-to-vanity-urls-vanity-urls) pour plus d’informations.

* **Ajouter** : appuyez ou cliquez pour ajouter une URL de redirection.
* **Supprimer** : appuyez ou cliquez pour supprimer une URL de redirection.
  **Rediriger l’URL de redirection** : indique si vous souhaitez que la page utilise l’URL de redirection ou redirige vers l’URL réelle de la page.

### Avancé {#advanced}

#### Paramètres {#settings}

* **Langue** – Langue de la page.
* **Racine de la langue** : cette option doit être activée si la page est la racine d’une copie linguistique.
* **Rediriger** – Indique la page vers laquelle cette page doit être automatiquement redirigée.
* **Conception** : indique la [conception](/help/sites-developing/designer.md) à utiliser sur cette page.
* **Alias** : indique un alias à utiliser avec cette page.
   * Par exemple, si vous définissez l’alias de `private` pour la page `/content/wknd/us/en/magazine/members-only`, alors cette page est également accessible via `/content/wknd/us/en/magazine/private`.
   * La création d’un alias permet de définir la propriété `sling:alias` sur le nœud de page, ce qui affecte uniquement la ressource, et non le chemin d’accès au référentiel.
   * Les pages accessibles par alias dans l’éditeur ne peuvent pas être publiées. Les [options de publication](/help/sites-authoring/publishing-pages.md) dans l’éditeur ne sont disponibles que pour les pages auxquelles vous pouvez accéder à partir de leur chemin d’accès.
   * Pour plus d’informations, consultez [Noms de page localisés dans les Bonnes pratiques de SEO et de gestion des URL](/help/managing/seo-and-url-management.md#localized-page-names).

#### Configuration {#configuration}

* **Hérité du &lt;*chemin*>** - Activer/désactiver l’héritage de la **configuration cloud** pour la page
* **Configuration du cloud** : chemin d’accès à la configuration

#### Paramètres de modèles {#templates}

* **Modèles autorisés** : [définit la liste des modèles qui seront disponibles](/help/sites-authoring/templates.md#allowingatemplate) dans cette sous-branche.

#### Exigence d’authentification {#authentication}

* **Activer** : active/désactive l’utilisation de l’authentification afin que vous puissiez accéder à la page.
* **Page de connexion** : page à utiliser pour la connexion

>[!NOTE]
>
>Les groupes d’utilisateurs et d’utilisatrices fermés pour la page sont définis dans l’onglet **[Autorisations](/help/sites-authoring/editing-page-properties.md#permissions)**.

>[!CAUTION]
>
>L’onglet **[Autorisations](#permissions)** permet de modifier les configurations des groupes d’utilisateurs et d’utilisatrices fermés basées sur la présence du mixin `granite:AuthenticationRequired`. Si les autorisations de page sont configurées à l’aide de configurations des groupes d’utilisateurs et d’utilisatrices fermés obsolètes, selon la présence de la propriété `cq:cugEnabled`, un message d’avertissement s’affiche sous **Exigence d’authentification** et l’option n’est pas modifiable, tout comme les [autorisations](/help/sites-authoring/editing-page-properties.md#permissions).
>
>
>Le cas échéant, les autorisations des groupes d’utilisateurs et utilisatrices fermés doivent être modifiées dans l’[UI classique](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

#### Export {#export}

* **Configuration de l’export** : spécifie une configuration d’export.

#### SEO {#seo}

* **URL canonique** : permet de remplacer l’URL canonique de la page.
   * Si le champ est vide, l’URL de la page est son URL canonique.
* **Balises robots** : utilisez la liste déroulante pour sélectionner les balises robots permettant de gérer le comportement des robots des moteurs de recherche.
   * Certaines options entrent en conflit avec d&#39;autres. Dans ce cas, l’option la plus permissive prévaut.
* **Générer un plan de site** : lorsque cette option est sélectionnée, un fichier `sitemap.xml` est généré pour cette page et ses descendants.

### Images {#images}

#### Image en vedette {#featured-image}

Cette section permet de sélectionner et de configurer l’image à afficher. Cette option est utilisée dans les composants qui référencent la page, par exemple, les teasers, les listes de pages, etc.

* **Image** : vous pouvez **sélectionner** un fichier ou rechercher un fichier à télécharger, puis **modifier** ou **effacer** l’image sélectionnée.
* **Texte secondaire** : texte utilisé pour décrire la signification et/ou la fonction de l’image. Couramment utilisé par les lecteurs d’écran.
* **Hériter - Valeur issue de la ressource DAM** : lorsque cette option est cochée, le texte secondaire est renseigné avec la valeur des métadonnées `dc:description`dans DAM.

#### Miniature {#thumbnail}

Cette section permet de sélectionner et de configurer la miniature d&#39;image de la page. Cette option est utilisée dans les composants qui référencent la page, par exemple, les teasers, les listes de pages, etc.

* **Générer l’aperçu** : générez un aperçu de la page que vous souhaitez utiliser comme miniature.
* **Charger une image** : chargez une image que vous souhaitez utiliser comme miniature.
* **Sélectionner une image** : sélectionnez une ressource existante à utiliser comme miniature.
* **Rétablir** : cette option est disponible une fois que vous avez modifié la miniature. Si vous ne souhaitez pas conserver votre modification, vous pouvez l’annuler avant d’enregistrer.

### Services cloud {#cloud-services}

* **Configurations du service cloud** : définit la configuration utilisée pour les services cloud de la page.
* **Hérité de** : pour les Live Copies et les copies de langue, les configurations cloud sont par défaut héritées du plan directeur.
   * Désélectionner pour remplacer l’héritage

### Personnalisation {#personalization}

#### Configurations ContextHub {#contexthub}

* **Hérité de** : les configurations ContextHub sont héritées par défaut de la page parent.
   * Décochez pour remplacer l’héritage.
* **Chemin ContextHub** : définit la [configuration ContextHub.](/help/sites-developing/ch-configuring.md)
* **Chemin d’accès aux segments** : permet de sélectionner le [chemin d’accès aux segments](/help/sites-administering/segmentation.md).

#### Configuration du ciblage {#targeting}

Sélectionnez une [marque pour spécifier la portée du ciblage.](/help/sites-authoring/target-adobe-campaign.md)

>[!NOTE]
>Cette option nécessite que le compte d’utilisateur figure dans le groupe `Target Adminstrators`.

### Autorisations {#permissions}

Utilisez l’onglet **Autorisations** pour définir les utilisateurs et utilisatrices, groupes ou [groupes fermés d’utilisateurs et d’utilisatrices (CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=fr) autorisés à accéder à la page et/ou à la modifier.

* [Ajouter des autorisations](/help/sites-administering/user-group-ac-admin.md)
* [Modifier le groupe d’utilisateurs fermé](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)
* Afficher les [autorisations effectives](/help/sites-administering/user-group-ac-admin.md)

>[!CAUTION]
>
>L’onglet **Autorisations** permet de modifier les configurations des groupes d’utilisateurs fermés basées sur la présence du mixin `granite:AuthenticationRequired`. Si les autorisations de page sont configurées à l’aide de configurations de groupes d’utilisateurs et d’utilisatrices fermés obsolètes, basées sur la présence de la propriété `cq:cugEnabled`, un message d’avertissement s’affiche et les autorisations des groupes d’utilisateurs et d’utilisatrices fermés ne sont pas modifiables, tout comme l’option Exigence d’authentification de l’onglet modifiable [Avancé](/help/sites-authoring/editing-page-properties.md#advanced).
>
>
>Le cas échéant, les autorisations des groupes d’utilisateurs fermés doivent être modifiées dans l’[IU classique](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

>[!NOTE]
>
>L’onglet Autorisations n’autorise pas la création de groupes d’utilisateurs et d’utilisatrices vides, ce qui peut se révéler utile comme un moyen simple de refuser l’accès à chaque utilisateur et utilisatrice. Pour ce faire, utilisez l’explorateur CRX. Pour plus d’informations, consultez le document [Administration des utilisateurs, des utilisatrices, des groupes et des droits d’accès](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

Cet onglet n’est visible que pour les pages qui servent de plan directeur. Les plans directeurs servent de base aux Live Copies, et font partie de la [gestion multisite.](/help/sites-administering/msm.md)

* **Déploiement** : lance le déploiement du contenu du plan directeur vers les Live Copies.
* **Aperçu de la Live Copy** : ouvre une fenêtre permettant de parcourir la structure de la page de la Live Copy.
* **Live Copies actuelles** : listes de pages basées sur (c’est-à-dire qu’il s’agit de Live Copies de) la page de plan directeur sélectionnée.
* **Configuration du déploiement** : définit la configuration du déploiement de la page.

### Live Copy {#live-copy}

Cet onglet n’est visible que pour les pages configurées en tant que Live Copies. Comme pour les [plans directeurs](#blueprint), les Live Copies font partie de la [gestion multisite.](/help/sites-administering/msm.md)

* **Synchroniser** : synchronise la Live Copy avec le plan directeur, en conservant les modifications locales.
* **Réinitialiser** : réinitialise la Live Copy à l’état de plan directeur, en supprimant les modifications locales.
* **Suspendre** : empêche la Live Copy de recevoir des modifications de déploiement supplémentaires.
* **Désolidariser** : désolidarise la Live Copy du plan directeur.

#### Source {#source}

* Affiche le chemin du plan directeur pour cette Live Copy.

#### Statut {#status}

* Liste l’état actuel de la Live Copy de la page.

#### Configuration {#live-copy-config}

* **Héritage de Live Copy** : si cette option est cochée, la configuration de la Live Copy est effective sur tous les enfants.
* **Hériter des configurations de déploiement du parent** : si cette option est cochée, la configuration de déploiement est héritée du parent de la page.
* **Choisir la configuration de déploiement** : définit les circonstances dans lesquelles les modifications sont propagées à partir du plan directeur et disponibles uniquement lorsque l’option **Hériter des configurations de déploiement du parent** n’est pas sélectionnée.
* **Liste des chemins exclus**

## Modification des propriétés de page {#editing-page-properties-1}

Vous pouvez définir les propriétés de page :

* Dans la console **Sites** :

   * [Créer une page](/help/sites-authoring/managing-pages.md#creating-a-new-page) (sous-ensemble des propriétés)

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

1. Cliquez ensuite sur **Enregistrer** pour enregistrer vos modifications et sur **Fermer** pour revenir à la console.

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

Dans la console **Sites**, vous pouvez sélectionner plusieurs pages, puis utiliser **Afficher les propriétés** pour afficher et/ou modifier les propriétés de la page. On parle alors de modification en bloc des propriétés de la page.

>[!NOTE]
>
>La modification en bloc des propriétés est également disponible pour les ressources. Elle est similaire, mais diffère en quelques points. Pour plus d’informations, voir [Modification des propriétés de plusieurs ressources](/help/assets/metadata.md).
>
>Il existe également un [Éditeur en bloc](/help/sites-administering/bulk-editor.md). Celui-ci vous permet de rechercher du contenu provenant de plusieurs pages à l’aide du langage GQL (Google Query Language), puis de le modifier directement avant d’enregistrer les modifications dans les pages d’origine.

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

Une fois en mode de modification en bloc, vous pouvez effectuer les opérations suivantes :

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
      * Lorsque le champ comporte plusieurs valeurs (Balises, par exemple), les valeurs ne sont visibles que si elles sont *toutes* communes. Si seulement certaines d’entre elles sont communes, elles s’affichent uniquement lors de la modification.

  En l’absence de propriétés avec une valeur commune, un message s’affiche.

* **Modifier**

  Lors de la modification des propriétés de page pour plusieurs pages :

   * Vous pouvez mettre à jour les valeurs dans les champs disponibles.

      * Les nouvelles valeurs sont appliquées à toutes les pages sélectionnées lorsque vous sélectionnez **Terminé**.
      * Lorsque le champ comporte plusieurs valeurs (Balises, par exemple), vous pouvez ajouter une nouvelle valeur ou supprimer une valeur commune.

   * Les champs qui sont communs, mais pour lesquels des valeurs différentes sont renseignées dans les différentes pages, sont signalés par une valeur spéciale, par exemple par le texte `<Mixed Entries>`.

>[!NOTE]
>
>Le composant de page peut être configuré pour spécifier les champs disponibles pour une modification en masse. Voir [Configurer votre page pour une modification en masse des propriétés de page](/help/sites-developing/bulk-editing.md).
