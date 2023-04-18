---
title: Modification des propriétés de page
description: Les propriétés d’une page peuvent varier en fonction de la nature de la page. Par exemple, certaines pages peuvent être connectées à une Live Copy, tandis que d’autres ne le sont pas, et les informations de Live Copy seront disponibles, le cas échéant.
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
exl-id: 1a77e4cd-bbf8-4d05-bb35-fd43c02eaf30
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 45%

---

# Modification des propriétés de page{#editing-page-properties}

Vous pouvez définir les propriétés requises pour une page. Celles-ci peuvent varier selon la nature de la page. Par exemple, certaines pages peuvent être connectées à une Live Copy alors que d’autres ne le sont pas et les informations de Live Copy seront disponibles, le cas échéant.

## Propriétés de page {#page-properties}

Les propriétés sont réparties sur plusieurs onglets :

### De base {#basic}

* **Titre**

   Le titre de la page s’affiche à divers endroits. Par exemple, la variable **Sites web** et la liste des onglets **Sites** modes Carte/Liste.

   Ce champ est obligatoire.

* **Balises**

   Vous pouvez ajouter des balises sur la page, ou en supprimer, en mettant à jour la liste dans la zone de sélection :

   * La balise sélectionnée est alors répertoriée sous la zone de sélection. Vous pouvez supprimer une balise de cette liste à l’aide du symbole x.
   * Vous pouvez saisir une nouvelle balise en saisissant son nom dans une zone de sélection vide.

      La nouvelle balise est en réalité créée lorsque vous appuyez sur Entrée. Elle s’affiche alors dans un cadre et est marquée à droite d’une petite étoile indiquant qu’il s’agit d’une nouvelle balise.

   * Avec la fonctionnalité de liste déroulante, vous pouvez effectuer un choix parmi des balises existantes.
   * Un x s’affiche lorsque vous placez le pointeur de la souris sur une entrée de balise dans la zone de sélection. vous pouvez l’utiliser pour supprimer cette balise pour cette page.

* **Masquer dans la navigation**

   Bascule pour indiquer si la page est affichée ou masquée dans la navigation.

* **Titre de la page**

   Titre à utiliser sur la page.

* **Titre de navigation**

   Vous pouvez spécifier un titre distinct à utiliser dans la navigation (par exemple, si vous souhaitez qu’il soit plus concis). Si elle est vide, la variable **Titre** sera utilisé.

* **Sous-titre**

   Sous-titre à utiliser sur la page.

* **Description**

   Votre description de la page, son objectif ou tout autre détail que vous souhaitez ajouter.

* **Heure d’activation**

   Date et heure auxquelles la page publiée sera activée. Une fois publiée, cette page restera dormante jusqu’à l’heure indiquée.

   Laissez ces champs vides pour les pages que vous souhaitez publier immédiatement (scénario normal).

* **Heure de désactivation**

   Heure à laquelle la page publiée sera désactivée.

   Laissez à nouveau ces champs vides pour les pages que vous souhaitez publier immédiatement.

* **URL de redirection**

   Permet de saisir une URL Vanity pour cette page. Cela vous permet d’avoir une URL plus courte et plus expressive.

   Par exemple, si l’URL de redirection est définie sur w`elcome` sur la page identifiée par le chemin / `v1.0/startpage` pour le site Web h`ttp://example.com,`, `ttp://example.com/welcome` devient alors l’URL de redirection de `ttp://example.com/content/v1.0/startpage`.

   >[!CAUTION]
   >
   >URL de redirection :
   >
   >* doit être unique. Vous devez donc veiller à ce que la valeur ne soit pas déjà utilisée par une autre page.
   >* ne prennent pas en charge les modèles regex.


* **Rediriger l’URL Vanity**

   Indique si vous souhaitez que la page utilise l’URL Vanity.

### Avancé {#advanced}

* **Langue**

   Langue de la page.

* **Rediriger**

   Indiquez la page vers laquelle cette page doit automatiquement être redirigée.

* **Conception**

   Indiquez les [design](/help/sites-developing/designer.md) à utiliser pour cette page.

* **Alias**

   Indiquez un alias à utiliser avec cette page.

* **Activer le groupe d’utilisateurs fermé**

   Active (ou désactive) l’utilisation de [groupes d’utilisateurs fermés](/help/sites-administering/cug.md) (CUG).

* **Page de connexion**

   Page à utiliser pour la connexion.

* **Groupes admis**

   Groupes pouvant se connecter au groupe d’utilisateurs fermé.

* **Domaine**

   Nom de domaine du CUG.

* **Exporter la configuration**

   Spécifiez une configuration d’exportation.

### Miniature  {#thumbnail}

* **Miniature de page**

   Affiche la miniature de la page. Vous pouvez :

   * **Générer l’aperçu**

      Générez un aperçu de la page à utiliser comme miniature.

   * **Charger l’image**

      Téléchargez une image à utiliser comme miniature.

### Services cloud {#cloud-services}

* **Services cloud**

   Définition des propriétés pour [services cloud](/help/sites-developing/extending-cloud-config.md).

### Personnalisation {#personalization}

* **Personnalisation**

   Sélectionnez une [marque pour spécifier la portée du ciblage](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Autorisations {#permissions}

* **Autorisations** (IU optimisée pour les écrans tactiles)

   Permet d’afficher les [autorisations en vigueur et d’en ajouter de nouvelles](/help/sites-administering/user-group-ac-admin.md).

### Plan directeur {#blueprint}

* **Plan directeur**

   Définition des propriétés d’une page de plan directeur dans [gestion multisite](/help/sites-administering/msm.md). Détermine les circonstances dans lesquelles les modifications seront diffusées à la Live Copy.

### Live Copy  {#live-copy}

* **Live Copy**

   Définition des propriétés d’une page Live Copy dans [gestion multisite](/help/sites-administering/msm.md). Détermine les circonstances dans lesquelles les modifications seront propagées à partir du plan directeur.

### Structure du site  {#site-structure}

* Diffusez des liens d’accès aux pages qui fournissent les fonctionnalités à l’échelle du site, comme la **page d’inscription** et la page **en mode hors ligne**, entre autres.

## Modification des propriétés de page {#editing-page-properties-2}

### Modification des propriétés de page d’une page spécifique {#editing-page-properties-for-a-specific-page}

Les propriétés de page définissent les différentes propriétés de la page, telles que les titres, lorsqu’elles apparaissent sur le site web, etc.

1. Ouvrez la page à modifier.

1. Dans le sidekick, ouvrez l’onglet **Page**, puis sélectionnez **Propriétés de la page…**

   Une boîte de dialogue comprenant plusieurs onglets s’ouvre.

1. Apportez les modifications requises, puis cliquez sur **OK** pour les enregistrer.
