---
title: Configuration de Connector for IBM&reg ; Content Manager
description: Configurez Connector for IBM&reg ; Content Manager pour activer la communication entre AEM forms et IBM&reg ; Content Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 2%

---

# Configuration de Connector for IBM® Content Manager{#configuring-connector-for-ibm-content-manager}

Connector for IBM® Content Manager permet la communication entre AEM forms et IBM® Content Manager. Pour plus d’informations, voir &quot;Connecteurs pour ECM&quot; dans [Référence des services](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Configuration de la connexion IBM® Content Manager {#configure-the-ibm-content-manager-connection}

1. Dans Administration Console, cliquez sur Services > Connecteur pour IBM® Content Manager.
1. Dans la zone Datastore Name , saisissez le nom de la banque de données IBM® Content Manager à laquelle vous souhaitez vous connecter. Si la base de données est locale, saisissez son nom. Si la base est distante, indiquez son nom d&#39;alias.
1. Dans la zone Nom d’utilisateur , saisissez l’ID d’un utilisateur qui va se connecter à la banque de données IBM® Content Manager.
1. Dans la zone Mot de passe, saisissez le mot de passe de l’utilisateur.
1. (Facultatif) Dans la zone Chaîne de connexion de l’alias, saisissez des arguments de connexion supplémentaires. En règle générale, cette boîte doit être vide. Pour plus d’informations, consultez votre documentation IBM® .
1. Cliquez sur Enregistrer.

## Validation des paramètres du service {#validation-of-service-settings}

Si vous saisissez un alias de banque de données, un nom d’utilisateur ou un mot de passe incorrects, les résultats sont les suivants, selon que le service Content Repository Connector for IBM® Content Manager est en cours d’exécution ou non :

* Si le service est arrêté, aucune erreur n’apparaît lorsque vous enregistrez les informations de configuration du service. Cependant, lors du prochain démarrage du service, une exception est générée et le service ne démarre pas.
* Si le service est démarré, lorsque vous enregistrez les informations de configuration du service, celui-ci tente de valider immédiatement les informations d’identification. Dans ce cas, une erreur se produit et les informations de configuration ne sont pas enregistrées.
