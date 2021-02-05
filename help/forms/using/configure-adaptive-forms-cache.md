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
source-git-commit: 2d54d115529126162c92e9943a188d05159535f9
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 23%

---


# Configurer le cache de formulaires adaptatifs {#configure-adaptive-forms-cache}

Un cache est un mécanisme qui permet de raccourcir les temps d’accès aux données, réduire le temps de réponse et améliorer les vitesses d’entrée/sortie (E/S). Le cache de formulaires adaptatifs stocke uniquement le contenu HTML et la structure JSON d’un formulaire adaptatif sans enregistrer les données pré-renseignées. Cela permet de réduire le temps nécessaire pour générer un formulaire adaptatif sur le client. Il est spécialement conçu pour les formulaires adaptatifs.

## Configurer le cache de formulaires adaptatifs aux instances d’auteur et de publication {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Accédez à AEM gestionnaire de configuration de la console Web à l’adresse `https://[server]:[port]/system/console/configMgr`.
1. Cliquez sur la **[!UICONTROL configuration de canal web de communication interactive de formulaire adaptatif]** pour éditer ses valeurs de configuration.
1. Dans la boîte de dialogue [!UICONTROL modifier les valeurs de configuration], spécifiez le nombre maximal de formulaires ou de documents qu&#39;une instance du serveur [!DNL Forms] peut mettre en cache dans le champ **[!UICONTROL Nombre de Forms adaptatif]**. La valeur par défaut est 100.

   >[!NOTE]
   >
   >Pour désactiver le cache, définissez la valeur du champ Nombre de formulaires adaptatifs sur **0**. Le cache est réinitialisé, et tous les formulaires et documents sont supprimés du cache lorsque vous désactivez ou modifiez la configuration du cache.

   ![Boîte de dialogue de configuration du cache HTML de formulaires adaptatifs](assets/cache-configuration-edit.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer la configuration 

Votre environnement est configuré pour utiliser le cache des formulaires adaptatifs et des ressources connexes.


## (Facultatif) Configurez le cache de formulaire adaptatif à l’adresse dispatcher {#configure-the-cache}

Vous pouvez également configurer la mise en cache des formulaires adaptatifs sur le répartiteur pour améliorer les performances.

### Conditions préalables {#pre-requisites}

* Activez l&#39;option [fusion ou préremplissage des données au niveau du client](prepopulate-adaptive-form-fields.md#prefill-at-client). Il permet de fusionner des données uniques pour chaque instance d’un formulaire prérempli.

### Considérations relatives à la mise en cache de formulaires adaptatifs sur un répartiteur {#considerations}

* Lors de l’utilisation du cache de formulaires adaptatifs, utilisez l’AEM [!DNL Dispatcher] pour mettre en cache les bibliothèques client (CSS et JavaScript) d’un formulaire adaptatif.
* Lors du développement des composants personnalisés, sur le serveur utilisé pour le développement, gardez le cache de formulaires adaptatifs désactivé.
* Les URL sans extension ne sont pas mises en cache. Par exemple, les URL avec modèle`/content/forms/[folder-structure]/[form-name].html` sont mises en cache et la mise en cache ignore les URL avec modèle `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Par conséquent, utilisez des URL avec des extensions pour tirer parti des avantages de la mise en cache.
* Considérations relatives aux formulaires adaptatifs localisés :
   * Utilisez le format d’URL `http://host:port/content/forms/af/<afName>.<locale>.html` pour demander une version localisée d’un formulaire adaptatif au lieu de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Désactivez l’utilisation de ](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) localepour les URL au format  `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Lorsque vous utilisez le format d’URL `http://host:port/content/forms/af/<adaptivefName>.html` et **[!UICONTROL Utiliser la langue du navigateur]** dans le gestionnaire de configuration est désactivé, la version non localisée du formulaire adaptatif est diffusée. La langue non localisée est la langue utilisée lors du développement du formulaire adaptatif. Les paramètres régionaux configurés pour votre navigateur (paramètres régionaux du navigateur) ne sont pas pris en compte et une version non localisée du formulaire adaptatif est diffusée.
   * Lorsque vous utilisez le format d’URL `http://host:port/content/forms/af/<adaptivefName>.html` et **[!UICONTROL Utiliser les paramètres régionaux du navigateur]** dans le gestionnaire de configuration est activé, une version localisée du formulaire adaptatif est diffusée, le cas échéant. La langue du formulaire adaptatif localisé est basée sur les paramètres régionaux configurés pour votre navigateur (paramètres régionaux du navigateur). Il peut conduire à [la mise en cache de la première instance d’un formulaire adaptatif]. Pour éviter que le problème ne se produise sur votre instance, voir [dépannage](#only-first-insatnce-of-adptive-forms-is-cached).

### Activation de la mise en cache sur le répartiteur

Suivez les étapes ci-dessous pour activer et configurer la mise en cache des formulaires adaptatifs sur le répartiteur :

1. Ouvrez l’URL suivante pour chaque instance de publication de votre environnement et [activez l’agent de vidage pour les instances de publication de votre environnement](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) :
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Ajoutez les éléments suivants à votre fichier](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files) dispatcher.any :

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

   * Lorsqu’une nouvelle version de la ressource référencée dans un formulaire adaptatif est publiée, les formulaires adaptatifs concernés sont automatiquement invalidés. Il existe certaines exceptions à l’invalidation automatique des ressources référencées. Pour contourner les exceptions, voir la section [dépannage](#troubleshooting).
1. [Ajoutez le fichier dispatcher.any des règles ci-dessous ou le fichier](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache) de règles personnalisées. Elle exclut les URL qui ne prennent pas en charge la mise en cache. Par exemple, Communication interactive.

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

1. [Ajoutez les paramètres suivants à la liste](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters) des paramètres d’URL ignorés :

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Votre environnement AEM est configuré pour mettre en cache les formulaires adaptatifs. Il met en cache tous les types de formulaires adaptatifs. Si vous devez vérifier les autorisations d’accès utilisateur pour une page avant de diffuser la page mise en cache, voir [mise en cache du contenu sécurisé](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Résolution des incidents {#troubleshooting}

### Certains formulaires adaptatifs contenant des images ou des vidéos ne sont pas automatiquement invalidés à partir du cache de répartiteur {#videos-or-images-not-auto-invalidated}

#### Problème {#issue1}

Lorsque vous sélectionnez et ajoutez des images ou des vidéos via l’explorateur de ressources à un formulaire adaptatif et que ces images et vidéos sont modifiées dans l’éditeur Ressources, les formulaires adaptatifs contenant de telles images ne sont pas automatiquement invalidés à partir du cache du répartiteur.

#### Solution {#Solution1}

Après avoir publié les images et la vidéo, annulez et publiez explicitement les formulaires adaptatifs qui référencent ces ressources.

### Seule la première instance d’un formulaire adaptatif est mise en cache {#only-first-instance-of-adaptive-forms-is-cached}

#### Problème {#issue3}

Lorsque l’URL du formulaire adaptatif ne contient aucune information de localisation et **[!UICONTROL Utiliser la langue du navigateur]** dans le gestionnaire de configuration est activée, une version localisée du formulaire adaptatif est diffusée et seule la première instance du formulaire adaptatif est mise en cache et remise à chaque utilisateur suivant.

#### Solution {#Solution3}

Exécutez les étapes suivantes afin de résoudre ce problème :

1. Ouvrez le fichier conf.d/httpd-dispatcher.conf ou tout autre fichier de configuration configuré pour se charger au moment de l’exécution.

1. Ajoutez le code suivant dans votre fichier et enregistrez-le. Il s’agit d’un exemple de code que vous pouvez modifier en fonction de votre environnement.

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
