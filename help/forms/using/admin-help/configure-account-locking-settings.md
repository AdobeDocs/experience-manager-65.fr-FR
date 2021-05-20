---
title: Configuration des paramètres de verrouillage des comptes
seo-title: Configuration des paramètres de verrouillage des comptes
description: Utilisez l’option Activer le verrouillage de compte pour verrouiller des comptes utilisateur après un nombre spécifié d’échecs d’authentification consécutifs.
seo-description: Utilisez l’option Activer le verrouillage de compte pour verrouiller des comptes utilisateur après un nombre spécifié d’échecs d’authentification consécutifs.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 95%

---

# Configuration des paramètres de verrouillage des comptes {#configure-account-locking-settings}

Lorsque vous ajoutez un domaine, spécifiez s’il convient d’activer le verrouillage des comptes. Si l’option Activer le verrouillage de compte est activée, les comptes d’utilisateurs sont verrouillés après un certain nombre d’échecs d’authentification consécutifs. Après une durée définie, l’utilisateur peut à nouveau tenter de s’authentifier, ce qui évite que les utilisateurs ne tentent plusieurs combinaisons d’informations d’identification pour accéder au système.

Utilisez les paramètres de la page Gestion des domaines pour spécifier le nombre maximum d’échecs d’authentification et la durée de verrouillage des comptes. Ces paramètres s’appliquent à tous les domaines dans lesquels le verrouillage des comptes est activé.

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > User Management > Gestion des domaines]**.
1. Dans la zone Echecs d’authentification consécutifs max., indiquez le nombre de tentatives consécutives dont dispose un utilisateur pour ouvrir une session avant que son compte ne soit verrouillé. La valeur par défaut est 20.
1. Dans la zone Déverrouiller le compte après (minutes), indiquez la durée de verrouillage du compte utilisateur en minutes. A l’issue de ce délai, l’utilisateur peut tenter d’ouvrir une autre session. La valeur par défaut est 30.
1. Cliquez sur **[!UICONTROL Enregistrer]**.
