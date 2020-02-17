---
title: Configurer le cache de formulaires adaptatifs
seo-title: Configurer le cache de formulaires adaptatifs
description: 'Le cache de formulaires adaptatifs est spécialement conçu pour les formulaires et documents adaptatifs. Il met en cache des formulaires et documents adaptatifs en vue de réduire le temps nécessaire pour effectuer le rendu d’un formulaire ou d’un document adaptatif sur le client. '
seo-description: 'Le cache de formulaires adaptatifs est spécialement conçu pour les formulaires et documents adaptatifs. Il met en cache des formulaires et documents adaptatifs en vue de réduire le temps nécessaire pour effectuer le rendu d’un formulaire ou d’un document adaptatif sur le client. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# Configurer le cache de formulaires adaptatifs{#configure-adaptive-forms-cache}

Un cache est un mécanisme qui permet de raccourcir les temps d’accès aux données, réduire le temps de réponse et améliorer les vitesses d’entrée/sortie (E/S). Le cache de formulaires adaptatifs stocke uniquement le contenu HTML et la structure JSON d’un formulaire adaptatif sans enregistrer les données pré-renseignées. Cela permet de réduire le temps nécessaire pour effectuer le rendu d’un formulaire ou d’un document adaptatif sur le client. Il est spécialement conçu pour les formulaires adaptatifs et prend également en charge les documents adaptatifs.

>[!NOTE]
>
>Lorsque vous utilisez le cache de formulaires adaptatifs, utilisez le répartiteur AEM pour masquer les bibliothèques client (CSS et Javascript) d’un formulaire ou d’un document adaptatif.

>[!NOTE]
>
>Lors du développement des composants personnalisés, sur le serveur utilisé pour le développement, gardez le cache de formulaires adaptatifs désactivé.

## Configurer le cache {#configure-the-cache}

Effectuez les étapes suivantes pour configurer le cache des formulaires adaptatifs :

1. Go to AEM web console configuration manager at https://[server]:[port]/system/console/configMgr.
1. Cliquez sur la **configuration de canal web de communication interactive de formulaire adaptatif** pour éditer ses valeurs de configuration.
1. In the edit configuration values dialog, specify the maximum number of forms or documents an instance of the AEM Forms server can cache in the **Number of Adaptive Forms** field. La valeur par défaut est 100.

   >[!NOTE]
   >
   >Pour désactiver le cache, définissez la valeur du champ Nombre de formulaires adaptatifs sur **0**. Le cache est réinitialisé, et tous les formulaires et documents sont supprimés du cache lorsque vous désactivez ou modifiez la configuration du cache.

   ![Boîte de dialogue de configuration du cache HTML de formulaires adaptatifs](assets/cache-configuration-edit.png)

1. Cliquez sur **Enregistrer** pour enregistrer la configuration 

