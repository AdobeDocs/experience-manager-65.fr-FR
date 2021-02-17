---
title: Modification et conversion de domaines
seo-title: Modification et conversion de domaines
description: Découvrez comment modifier les paramètres des domaines existants à partir de la page Gestion des domaines. Convertissez un domaine d’entreprise existant en un domaine hybride ou inversement.
seo-description: Découvrez comment modifier les paramètres des domaines existants à partir de la page Gestion des domaines. Convertissez un domaine d’entreprise existant en un domaine hybride ou inversement.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 100%

---


# Modification et conversion de domaines{#editing-and-converting-existing-domains}

Vous pouvez modifier les paramètres des domaines existants à partir de la page Gestion des domaines. Vous avez également la possibilité de convertir un domaine d’entreprise existant en domaine hybride.

## Modification d’un domaine {#edit-an-existing-domain}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le nom du domaine à modifier.
1. Pour modifier le nom du domaine, entrez les modifications voulues dans le champ Nom.
1. Pour modifier les informations d’authentification d’un domaine d’entreprise ou hybride, cliquez sur le nom de l’authentification approprié situé au bas de la page. Dans la page Modifier l’authentification, modifiez les paramètres selon les besoins. Voir [Paramètres d’authentification](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).
1. Pour modifier les informations d’annuaire d’un domaine d’entreprise, cliquez sur le nom de l’annuaire situé au bas de la page. Dans la page Modifier l’annuaire, modifiez les paramètres selon les besoins. Voir [Ajout d’annuaires ou d’interfaces SPI personnalisées](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).
1. Une fois les modifications effectuées, cliquez sur OK.

## Conversion d’un domaine d’entreprise en domaine hybride  {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le nom du domaine à convertir.
1. Cliquez sur Convertir en domaine hybride.
1. Vérifiez les informations affichées concernant les données des utilisateurs et des groupes ainsi que l’authentification des utilisateurs, puis cliquez sur OK.
1. Modifiez les paramètres du domaine hybride et cliquez sur OK.

>[!NOTE]
>
>si le domaine d’entreprise que vous convertissez ne contient pas de paramètres d’annuaire, les paramètres d’authentification LDAP sont perdus.

## Conversion d’un domaine hybride en domaine d’entreprise  {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le nom du domaine hybride à convertir.
1. Cliquez sur Convertir en domaine d’entreprise.
1. Vérifiez les informations affichées concernant les données des utilisateurs et des groupes ainsi que l’authentification des utilisateurs, puis cliquez sur OK.
1. Cliquez sur Ajouter un annuaire et configurez les informations requises sur l’annuaire. Voir [Ajout d’annuaires ou d’interfaces SPI personnalisées](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).

