---
title: Minimisation des fichiers JavaScript
seo-title: Minimisation des fichiers JavaScript
description: Instructions permettant de générer du code minimisé après des personnalisations de l’espace de travail AEM Forms pour optimiser les fichiers JS pour le Web.
seo-description: Instructions permettant de générer du code minimisé après des personnalisations de l’espace de travail AEM Forms pour optimiser les fichiers JS pour le Web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 85%

---


# Minimisation des fichiers JavaScript {#minification-of-the-javascript-files}

La minimisation supprime du code source les caractères redondants, comme les espaces blancs, les nouvelles lignes et les commentaires. Cela améliore les performances en réduisant la taille du code. La minimisation n’a aucun impact sur la fonctionnalité et réduit la lisibilité du code.

Pour générer un code minimisé pour les modifications sémantiques, effectuez les étapes suivantes.

1. Copiez `client-html/src/main/webapp/js` du paquet src sur le système de fichiers.

   >[!NOTE]
   >
   >Voir [Introduction à la personnalisation de l’espace de travail AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) pour plus d’informations sur les paquets.

1. Mettez à jour les chemins dans `main.js` situé sous client-html/src/main/webapp/js, pour les modèles/vues ajoutés/mis à jour.

   Par exemple, pour ajouter un nouveau modèle Sharequeue, par exemple mySharequeue, modifiez :

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   To

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Mettez à jour `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` en cas de modification/ajout d&#39;alias dans `main.js`.

   Par exemple, pour ajouter un nouveau modèle Sharequeue, par exemple mySharequeue, modifiez :

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   À

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. Dans client-html/src/main/webapp/js/minifier, exécutez la commande :

   ```shell
   mvn clean install
   ```

   Elle génère un dossier minified-files, sous client-html/src/main/webapp/js avec main.js et registre.js minifiés.

>[!NOTE]
>
>la minimisation fonctionne uniquement sur les JVM 64 bits.

>[!NOTE]
>
>la minimisation a des effets sur la mise à niveau.
