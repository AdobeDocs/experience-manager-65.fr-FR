---
title: Configurer les paramètres de verrouillage des comptes
description: Utilisez l’option Activer le verrouillage de compte pour verrouiller des comptes utilisateur après un nombre spécifié d’échecs d’authentification consécutifs.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 100%
---
# Configurer les paramètres de verrouillage des comptes {#configure-account-locking-settings}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Lorsque vous ajoutez un domaine, spécifiez s’il convient d’activer le verrouillage des comptes. Si l’option Activer le verrouillage de compte est activée, les comptes d’utilisateurs sont verrouillés après un certain nombre d’échecs d’authentification consécutifs. Après une durée définie, l’utilisateur ou l’utilisatrice peut à nouveau tenter de s’authentifier. Cette fonctionnalité évite que les utilisateurs et les utilisatrices ne tentent plusieurs combinaisons d’informations d’identification pour accéder au système.

Utilisez les paramètres de la page Gestion des domaines pour spécifier le nombre maximum d’échecs d’authentification et la durée de verrouillage des comptes. Ces paramètres s’appliquent à tous les domaines dans lesquels le verrouillage des comptes est activé.

1. Dans la console dʼadministration, cliquez sur **[!UICONTROL Paramètres > Gestion des utilisateurs > Gestion des domaines]**.
1. Dans la zone Échecs d’authentification consécutifs maximum, saisissez le nombre de tentatives consécutives de connexion infructueuses d’un utilisateur ou d’une utilisatrice avant que son compte ne soit verrouillé. La valeur par défaut est 20.
1. Dans la zone Déverrouiller le compte après (minutes), indiquez la durée de verrouillage du compte utilisateur en minutes. À l’issue de ce délai, l’utilisateur ou l’utilisatrice peut tenter de se reconnecter. La valeur par défaut est 30.
1. Cliquez sur **[!UICONTROL Enregistrer]**.
