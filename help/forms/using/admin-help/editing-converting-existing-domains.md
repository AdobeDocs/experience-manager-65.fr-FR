---
title: Modification et conversion de domaines existants
seo-title: Editing and converting existing domains
description: Découvrez comment modifier les paramètres des domaines existants à partir de la page Gestion des domaines. Convertissez un domaine d’entreprise existant en domaine hybride ou inversement.
seo-description: Learn how to change the settings for existing domains from the Domain Management page. Convert an existing enterprise domain to a hybrid domain or conversely.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 16%

---

# Modification et conversion de domaines existants{#editing-and-converting-existing-domains}

Vous pouvez modifier les paramètres des domaines existants à partir de la page Gestion des domaines . Vous pouvez également convertir un domaine d’entreprise existant en domaine hybride.

## Modification d’un domaine existant {#edit-an-existing-domain}

1. Dans la console dʼadministration, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le nom du domaine à modifier.
1. Pour modifier le nom du domaine, modifiez le texte dans la zone Nom .
1. Pour modifier les informations d’authentification d’un domaine d’entreprise ou hybride, cliquez sur le nom d’authentification approprié en bas de la page. Sur la page Modifier l’authentification , modifiez les paramètres selon les besoins. (Voir [Paramètres d’authentification](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Pour modifier les informations d’annuaire d’un domaine d’entreprise, cliquez sur le nom d’annuaire approprié en bas de la page. Sur la page Modifier l’annuaire, modifiez les paramètres selon les besoins. (Voir [Ajout d’annuaires ou d’interfaces SPI personnalisées](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Lorsque vous avez terminé vos modifications, cliquez sur OK.

## Convertir un domaine d’entreprise en domaine hybride {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. Dans la console dʼadministration, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le nom du domaine d’entreprise à convertir.
1. Cliquez sur Convertir en domaine hybride.
1. Vérifiez les informations qui s’affichent concernant les données utilisateur et de groupe, ainsi que l’authentification des utilisateurs, puis cliquez sur OK.
1. Modifiez les paramètres du domaine hybride et cliquez sur OK.

>[!NOTE]
>
>Si le domaine d’entreprise que vous convertissez ne contient pas de paramètres d’annuaire, tout paramètre d’authentification LDAP est perdu.

## Conversion d’un domaine hybride en domaine d’entreprise {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. Dans la console dʼadministration, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le nom du domaine hybride à convertir.
1. Cliquez sur Convertir en domaine d’entreprise.
1. Vérifiez les informations qui s’affichent concernant les données utilisateur et de groupe, ainsi que l’authentification des utilisateurs, puis cliquez sur OK.
1. Cliquez sur Ajouter un annuaire et configurez les informations d’annuaire requises. (Voir [Ajout d’annuaires ou d’interfaces SPI personnalisées](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
