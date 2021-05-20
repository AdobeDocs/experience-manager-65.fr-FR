---
title: Configuration de Connector for IBM Content Manager
seo-title: Configuration de Connector for IBM Content Manager
description: Configurez le connecteur pour IBM Content Manager pour permettre la communication entre AEM Forms et IBM Content Manager.
seo-description: Configurez le connecteur pour IBM Content Manager pour permettre la communication entre AEM Forms et IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 96%

---

# Configuration de Connector for IBM Content Manager{#configuring-connector-for-ibm-content-manager}

Le connecteur pour IBM Content Manager permet la communication entre AEM forms et IBM Content Manager. Pour plus d’informations, voir Connectors for ECM, dans le [Guide de référence des services](https://www.adobe.com/go/learn_aemforms_services_63).

## Configuration de la connexion IBM Content Manager {#configure-the-ibm-content-manager-connection}

1. Dans Administration Console, cliquez sur Services > Connector for IBM Content Manager.
1. Dans le champ Nom de la banque de données, saisissez le nom de la banque de données IBM Content Manager à laquelle vous voulez vous connecter. S’il s’agit d’une base de données locale, entrez son nom. S’il s’agit d’une base de données distante, indiquez son nom d’alias.
1. Dans la zone Nom d’utilisateur, saisissez l’ID de l’utilisateur qui se connectera à la banque de données IBM Content Manager.
1. Dans le champ Mot de passe, saisissez le mot de passe de l’utilisateur.
1. (Facultatif) Dans le champ Chaîne de connexion de l’alias, saisissez des arguments de connexion supplémentaires. Ce champ n’est généralement pas complété. Pour plus d’informations, consultez votre documentation IBM.
1. Cliquez sur Enregistrer.

## Validation des paramètres d’un service  {#validation-of-service-settings}

Si vous saisissez un nom d’utilisateur ou un alias de banque de données incorrect, vous obtiendrez les résultats suivants selon que le service Content Repository Connector for IBM Content Manager est en cours d’exécution ou non :

* Si le service est arrêté, aucune erreur n’apparaît lorsque vous enregistrez les informations de configuration du service. Toutefois, lors du prochain démarrage du service, une exception sera générée et le service ne démarrera pas.
* Si le service est démarré, ce dernier tente de valider immédiatement les informations d’identification lorsque vous enregistrez les informations de configuration du service. Dans ce cas, une erreur se produit et les informations de configuration ne sont pas enregistrées.
