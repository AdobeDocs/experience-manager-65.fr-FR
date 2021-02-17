---
title: Modification des propriétés de page
seo-title: Modification des propriétés de page
description: Les propriétés d’une page peuvent varier selon la nature de la page. Par exemple, certaines pages peuvent être connectées à une Live Copy, et d’autres pas, et les informations Live Copy seront disponibles suivant le cas.
seo-description: Les propriétés d’une page peuvent varier selon la nature de la page. Par exemple, certaines pages peuvent être connectées à une Live Copy, et d’autres pas, et les informations Live Copy seront disponibles suivant le cas.
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 94%

---


# Modification des propriétés de page{#editing-page-properties}

Vous pouvez définir les propriétés requises pour une page. Celles-ci peuvent varier selon la nature de la page. Par exemple, certaines pages peuvent être connectées à une Live Copy, et d’autres pas, et les informations Live Copy seront disponibles suivant le cas.

## Propriétés de page {#page-properties}

Les propriétés sont réparties sur plusieurs onglets:

### De base {#basic}

* **Titre**

   Le titre de la page s’affiche à divers endroits. Par exemple, la liste de l’onglet **Sites web** et les modes Carte/Liste des **Sites**.

   Ce champ est obligatoire.

* **Balises**

   Vous pouvez ajouter des balises sur la page, ou en supprimer, en mettant à jour la liste dans la zone de sélection:

   * La balise sélectionnée est alors répertoriée sous la zone de sélection. Vous pouvez supprimer une balise de cette liste à l’aide du symbole x.
   * Vous pouvez saisir une nouvelle balise en entrant son nom dans une zone de sélection vide.

      La nouvelle balise sera en fait créée lorsque vous appuyez sur Entrée. Elle s’affiche alors dans un cadre et est marquée à droite d’une petite étoile indiquant qu’il s’agit d’une nouvelle balise.

   * Vous pouvez faire votre choix parmi les balises existantes dans la liste déroulante.
   * Un « x » apparaît lorsque vous passez le pointeur de la souris sur une entrée de balise dans la zone de sélection ; vous pouvez vous en servir pour supprimer cette balise de la page.

* **Masquer dans la navigation**

   Commutateur à bascule pour indiquer si la page doit être affichée ou masquée dans la navigation.

* **Titre de la page**

   Titre à utiliser sur la page.

* **Titre de navigation**

   Vous pouvez spécifier un titre distinct à utiliser dans la navigation (par exemple, si vous souhaitez qu’il soit plus concis). Si ce champ reste vide, le **titre** est utilisé.

* **Sous-titre**

   Sous-titre à utiliser sur la page.

* **Description**

   Votre description de la page, son objectif ou tout autre détail que vous souhaiteriez ajouter.

* **Heure d’activation**

   Date et heure auxquelles la page publiée sera activée. Une fois publiée, cette page restera dormante jusqu’à l’heure indiquée.

   Ne complétez pas ces champs pour les pages que vous souhaitez publier immédiatement (scénario normal).

* **Heure de désactivation**

   Heure à laquelle la page publiée sera désactivée.

   Ici encore, ne complétez pas ces champs pour les pages que vous souhaitez publier immédiatement.

* **URL Vanity**

   Permet de saisir une URL Vanity pour cette page. Vous pouvez ainsi disposer d’une URL plus courte et plus explicite.

   Par exemple, si l’URL de vanité est définie sur w `elcome`pour la page identifiée par le chemin / `v1.0/startpage`pour le site Web h `ttp://example.com,`, h `ttp://example.com/welcome`serait l’URL de vanité de h `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >L’URL Vanity :
   >
   >* doit être unique. Vous devez donc veiller à ce que la valeur ne soit pas déjà utilisée par une autre page.
   >* Ne prend pas en charge les modèles d’expression régulière.


* **Rediriger l’URL Vanity**

   Indique si vous souhaitez que la page utilise l’URL Vanity.

### Avancé {#advanced}

* **Langue**

   Langue de la page.

* **Rediriger**

   Indique la page vers laquelle cette page doit être automatiquement redirigée.

* **Conception**

   Indique la [conception](/help/sites-developing/designer.md) à utiliser pour cette page.

* **Alias**

   Indique un alias à utiliser avec cette page.

* **Activer le groupe d’utilisateurs fermé**

   Active (ou désactive) l’utilisation de [groupes d’utilisateurs fermés](/help/sites-administering/cug.md) (CUG).

* **Page de connexion**

   Page à utiliser pour la connexion.

* **Groupes admis**

   Groupes réunissant les conditions nécessaires pour se connecter au CUG.

* **Domaine**

   Nom de domaine pour le CUG.

* **Exporter la configuration**

   Indiquez une configuration d’exportation.

### Miniature  {#thumbnail}

* **Miniature de page**

   Affiche l’image de la miniature de la page. Vous pouvez :

   * **Générer l’aperçu**

      Génère un aperçu de la page à utiliser comme miniature.

   * **Télécharger l’image**

      Télécharge une image à utiliser comme miniature.

### Cloud Services {#cloud-services}

* **Cloud Services**

   Définissez les propriétés des [services cloud](/help/sites-developing/extending-cloud-config.md).

### Personnalisation  {#personalization}

* **Personnalisation**

   Sélectionnez une [marque pour spécifier la portée du ciblage](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Autorisations {#permissions}

* **Autorisations** (IU optimisée pour les écrans tactiles)

   Permet d’afficher les [autorisations en vigueur et d’en ajouter de nouvelles](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

   Définissez les propriétés d’une page Blueprint dans le cadre de la [gestion multi-site](/help/sites-administering/msm.md). Détermine les circonstances dans lesquelles les modifications seront diffusées à la Live Copy.

### Live Copy   {#live-copy}

* **Live Copy**

   Définissez les propriétés d’une page Live Copy dans le cadre de la [gestion multi-site](/help/sites-administering/msm.md). Détermine les circonstances dans lesquelles les modifications seront propagées à partir du plan directeur.

### Structure du site   {#site-structure}

* Diffusez des liens d’accès aux pages qui fournissent les fonctionnalités à l’échelle du site, comme la **page d’inscription** et la page **en mode hors ligne**, entre autres.

## Modification des propriétés de page {#editing-page-properties-2}

### Modification des propriétés d’une page spécifique {#editing-page-properties-for-a-specific-page}

Les Propriétés de page définissent les différentes propriétés de la page, telles que les titres, lorsqu’elles apparaissent sur le site Web et à d’autres emplacements.

1. Ouvrez la page à modifier.

1. Dans le sidekick, ouvrez l’onglet **Page**, puis sélectionnez **Propriétés de la page…**

   Une boîte de dialogue comprenant plusieurs onglets s’ouvre.

1. Apportez les modifications requises, puis cliquez sur **OK** pour les enregistrer.

