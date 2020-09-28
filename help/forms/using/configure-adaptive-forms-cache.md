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
source-git-commit: d5a649337acdc01c58ecc473e7c919e06cbd0188
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Configurer le cache de formulaires adaptatifs {#configure-adaptive-forms-cache}

Un cache est un mécanisme qui permet de raccourcir les temps d’accès aux données, réduire le temps de réponse et améliorer les vitesses d’entrée/sortie (E/S). Le cache de formulaires adaptatifs stocke uniquement le contenu HTML et la structure JSON d’un formulaire adaptatif sans enregistrer les données pré-renseignées. Cela permet de réduire le temps nécessaire pour générer un formulaire adaptatif sur le client. Il est spécialement conçu pour les formulaires adaptatifs.

## Configuration du cache de formulaires adaptatifs aux instances d’auteur et de publication {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Go to AEM web console configuration manager at `https://[server]:[port]/system/console/configMgr`.
1. Cliquez sur la **[!UICONTROL configuration de canal web de communication interactive de formulaire adaptatif]** pour éditer ses valeurs de configuration.
1. In the [!UICONTROL edit configuration values] dialog, specify the maximum number of forms or documents an instance of the AEM [!DNL Forms] server can cache in the **[!UICONTROL Number of Adaptive Forms]** field. La valeur par défaut est 100.   

   >[!NOTE]
   >
   >Pour désactiver le cache, définissez la valeur du champ Nombre de formulaires adaptatifs sur **0**. Le cache est réinitialisé, et tous les formulaires et documents sont supprimés du cache lorsque vous désactivez ou modifiez la configuration du cache.

   ![Boîte de dialogue de configuration du cache HTML de formulaires adaptatifs](assets/cache-configuration-edit.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer la configuration 

Votre environnement est configuré pour utiliser le cache des formulaires adaptatifs et des ressources connexes.


## (Facultatif) Configuration du cache de formulaires adaptatifs au répartiteur {#configure-the-cache}

Vous pouvez également configurer la mise en cache des formulaires adaptatifs sur le répartiteur pour améliorer les performances.

### Conditions préalables {#pre-requisites}

* Activez l’option de [fusion ou de préremplissage des données au niveau du client](prepopulate-adaptive-form-fields.md#prefill-at-client) . Il permet de fusionner des données uniques pour chaque instance d’un formulaire prérempli.
* [Activez l’agent de vidage pour chaque instance](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance)de publication. Il permet de mieux mettre en cache les performances des formulaires adaptatifs. L’URL par défaut des agents de vidage est `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Considérations relatives à la mise en cache de formulaires adaptatifs sur un répartiteur {#considerations}

* When using the adaptive forms cache, use the AEM [!DNL Dispatcher] to cache client libraries (CSS and JavaScript) of an adaptive form.
* Lors du développement des composants personnalisés, sur le serveur utilisé pour le développement, gardez le cache de formulaires adaptatifs désactivé.
* Les URL sans extension ne sont pas mises en cache. Par exemple, les URL avec modèle`/content/forms/[folder-structure]/[form-name].html` sont mises en cache et la mise en cache ignore les URL avec modèle `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Par conséquent, utilisez des URL avec des extensions pour tirer parti des avantages de la mise en cache.
* Considérations relatives aux formulaires adaptatifs localisés :
   * Utilisez le format URL `http://host:port/content/forms/af/<afName>.<locale>.html` pour demander une version localisée d’un formulaire adaptatif au lieu de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Désactivez l’utilisation des paramètres régionaux](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) du navigateur pour les URL au format `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Lorsque vous utilisez le format d’URL `http://host:port/content/forms/af/<adaptivefName>.html`et que l’option **** Utiliser les paramètres régionaux du navigateur dans le gestionnaire de configuration est désactivée, la version non localisée du formulaire adaptatif est diffusée. La langue non localisée est la langue utilisée lors du développement du formulaire adaptatif. Les paramètres régionaux configurés pour votre navigateur (paramètres régionaux du navigateur) ne sont pas pris en compte et une version non localisée du formulaire adaptatif est diffusée.
   * Lorsque vous utilisez le format d’URL `http://host:port/content/forms/af/<adaptivefName>.html`et que l’option **[!UICONTROL Utiliser la langue du navigateur]** dans le gestionnaire de configuration est activée, une version localisée du formulaire adaptatif est diffusée, le cas échéant. La langue du formulaire adaptatif localisé est basée sur les paramètres régionaux configurés pour votre navigateur (paramètres régionaux du navigateur). Elle peut entraîner la mise en [cache de la première instance d’un formulaire]adaptatif uniquement. Pour éviter que le problème ne se produise sur votre instance, voir [Dépannage](#only-first-insatnce-of-adptive-forms-is-cached).

### Activation de la mise en cache sur le répartiteur

Suivez les étapes ci-dessous pour activer et configurer la mise en cache des formulaires adaptatifs sur le répartiteur :

1. Ouvrez l’URL suivante pour chaque instance de publication de votre environnement et configurez l’agent de réplication :
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [ajoutez les éléments suivants à votre fichier](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files)dispatcher.any :

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   Lorsque vous ajoutez ce qui suit :

   * Un formulaire adaptatif reste en cache jusqu’à ce qu’une version mise à jour du formulaire ne soit pas publiée.

   * Lorsqu’une nouvelle version de la ressource référencée dans un formulaire adaptatif est publiée, les formulaires adaptatifs concernés sont automatiquement invalidés. Il existe certaines exceptions à l’invalidation automatique des ressources référencées. Pour contourner les exceptions, reportez-vous à la section [Dépannage](#troubleshooting) .
1. [ajoutez le fichier dispatcher.any des règles ci-dessous ou le fichier](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache)de règles personnalisées. Elle exclut les URL qui ne prennent pas en charge la mise en cache. Par exemple, Communication interactive.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [ajoutez les paramètres suivants à la liste](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters)des paramètres d’URL ignorés :

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Votre environnement AEM est configuré pour mettre en cache les formulaires adaptatifs. Il met en cache tous les types de formulaires adaptatifs. Si vous devez vérifier les autorisations d’accès utilisateur pour une page avant de diffuser la page mise en cache, reportez-vous à la section [Mise en cache du contenu](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html)sécurisé.

## Résolution des incidents {#troubleshooting}

### Certains formulaires adaptatifs contenant des images ou des vidéos ne sont pas automatiquement invalidés à partir du cache du répartiteur {#videos-or-images-not-auto-invalidated}

#### Problème {#issue1}

Lorsque vous sélectionnez et ajoutez des images ou des vidéos via l’explorateur de ressources à un formulaire adaptatif et que ces images et vidéos sont modifiées dans l’éditeur Ressources, les formulaires adaptatifs contenant de telles images ne sont pas automatiquement invalidés à partir du cache du répartiteur.

#### Solution {#Solution1}

Après avoir publié les images et la vidéo, annulez et publiez explicitement les formulaires adaptatifs qui référencent ces ressources.

### Certains formulaires adaptatifs contenant des fragments de contenu ou d’expérience ne sont pas automatiquement invalidés à partir du cache du répartiteur {#content-or-experience-fragment-not-auto-invalidated}

#### Problème {#issue2}

Lorsque vous ajoutez un fragment de contenu ou un fragment d’expérience à un formulaire adaptatif et que ces ressources sont modifiées et publiées de manière indépendante, les formulaires adaptatifs contenant ces ressources ne sont pas automatiquement invalidés à partir du cache du répartiteur.

#### Solution {#Solution2}

Après avoir publié un fragment de contenu ou un fragment d’expérience mis à jour, annulez explicitement la publication et publiez les formulaires adaptatifs qui utilisent ces ressources.

### Seule la première instance d’un formulaire adaptatif est mise en cache{#only-first-insatnce-of-adptive-forms-is-cached}

#### Problème {#issue3}

Lorsque l’URL du formulaire adaptatif ne contient aucune information de localisation et que l’option **[!UICONTROL Utiliser la langue du navigateur]** dans le gestionnaire de configuration est activée, une version localisée du formulaire adaptatif est diffusée et seule la première instance du formulaire adaptatif est mise en cache et remise à chaque utilisateur suivant.

#### Solution {#Solution3}

Exécutez les étapes suivantes afin de résoudre ce problème :

1. Ouvrez le fichier conf.d/httpd-dispatcher.conf ou tout autre fichier de configuration configuré pour se charger au moment de l’exécution.

1. ajoutez le code suivant dans votre fichier et enregistrez-le. Il s’agit d’un exemple de code que vous pouvez modifier en fonction de votre environnement.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
