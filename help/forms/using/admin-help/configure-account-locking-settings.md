---
title: Configurer les paramètres de verrouillage des comptes
description: Utilisez l’option Activer le verrouillage de compte pour verrouiller les comptes utilisateur après un nombre spécifié d’échecs d’authentification consécutifs.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 13%

---

# Configurer les paramètres de verrouillage des comptes {#configure-account-locking-settings}

Lorsque vous ajoutez un domaine, indiquez s’il faut activer le verrouillage des comptes. Lorsque l’option Activer le verrouillage de compte est sélectionnée, les comptes utilisateur sont verrouillés après un nombre spécifié d’échecs d’authentification consécutifs. Après une durée spécifiée, l’utilisateur peut à nouveau tenter de s’authentifier. Cette fonctionnalité empêche les utilisateurs d’essayer différentes combinaisons d’informations d’identification pour accéder au système.

Utilisez les paramètres de la page Gestion des domaines pour spécifier le nombre maximal d’échecs d’authentification et la durée de verrouillage des comptes. Ces paramètres s’appliquent à tous les domaines pour lesquels le verrouillage de compte est activé.

1. Dans la console dʼadministration, cliquez sur **[!UICONTROL Paramètres > Gestion des utilisateurs > Gestion des domaines]**.
1. Dans la zone Echecs d’authentification consécutifs maximum, saisissez le nombre de tentatives consécutives d’ouverture de session d’un utilisateur avant que son compte ne soit verrouillé. La valeur par défaut est 20.
1. Dans la zone Déverrouiller le compte après (minutes) , saisissez le nombre de minutes pendant lesquelles le compte utilisateur est verrouillé. Après le nombre de minutes spécifié, l’utilisateur peut tenter de se reconnecter. La valeur par défaut est 30.
1. Cliquez sur **[!UICONTROL Enregistrer]**.
