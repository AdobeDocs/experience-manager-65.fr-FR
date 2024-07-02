---
title: Modification et conversion de domaines existants
description: Découvrez comment modifier les paramètres des domaines existants à partir de la page Gestion des domaines. Convertissez un domaine d’entreprise existant en un domaine hybride ou inversement.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '309'
ht-degree: 100%

---

# Modification et conversion de domaines existants{#editing-and-converting-existing-domains}

Vous pouvez modifier les paramètres des domaines existants à partir de la page Gestion des domaines. Vous avez également la possibilité de convertir un domaine d’entreprise existant en domaine hybride.

## Modifier un domaine {#edit-an-existing-domain}

1. Dans la console dʼadministration, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le nom du domaine à modifier.
1. Pour modifier le nom du domaine, saisissez les modifications voulues dans le champ Nom.
1. Pour modifier les informations d’authentification d’un domaine d’entreprise ou hybride, cliquez sur le nom de l’authentification approprié situé au bas de la page. Sur la page Modifier l’authentification, modifiez les paramètres selon les besoins. (Voir [Paramètres d’authentification](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)).
1. Pour modifier les informations d’annuaire d’un domaine d’entreprise, cliquez sur le nom de l’annuaire situé au bas de la page. Sur la page Modifier l’annuaire, modifiez les paramètres selon les besoins. (Voir [Ajout d’annuaires ou d’interfaces SPI personnalisées](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Une fois les modifications effectuées, cliquez sur OK.

## Convertir un domaine d’entreprise en domaine hybride {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. Dans la console dʼadministration, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le nom du domaine d’entreprise à convertir.
1. Cliquez sur Convertir en domaine hybride.
1. Vérifiez les informations affichées concernant les données des personnes et des groupes, ainsi que l’authentification des personnes, puis cliquez sur OK.
1. Modifiez les paramètres du domaine hybride et cliquez sur OK.

>[!NOTE]
>
>Si le domaine d’entreprise que vous convertissez ne contient pas de paramètres d’annuaire, les paramètres d’authentification LDAP sont perdus.

## Convertir un domaine hybride en domaine d’entreprise {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. Dans la console dʼadministration, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le nom du domaine hybride à convertir.
1. Cliquez sur Convertir en domaine d’entreprise.
1. Vérifiez les informations affichées concernant les données des personnes et des groupes, ainsi que l’authentification des personnes, puis cliquez sur OK.
1. Cliquez sur Ajouter un annuaire et configurez les informations requises sur l’annuaire. (Voir [Ajout d’annuaires ou d’interfaces SPI personnalisées](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
