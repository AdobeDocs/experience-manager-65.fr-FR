---
title: Minimiser les fichiers JavaScript
description: Instructions de génération du code minimisé après les personnalisations de l’espace de travail AEM Forms afin d’optimiser les fichiers JS pour le web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 35%

---

# Minimiser les fichiers JavaScript {#minification-of-the-javascript-files}

La minimisation supprime du code source les caractères redondants, tels que les espaces blancs, les nouvelles lignes et les commentaires. Cela améliore les performances en réduisant la taille du code. Bien que la minimisation n’ait aucune incidence sur les fonctionnalités, elle réduit la lisibilité du code.

Pour générer du code minimisé pour les modifications sémantiques, procédez comme suit.

1. Copiez `client-html/src/main/webapp/js` de src-package dans filesystem.

   >[!NOTE]
   >
   >Voir [Introduction à la personnalisation de l’espace de travail AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) pour plus d’informations sur les packages.

1. Mettez à jour les chemins dans `main.js` sous client-html/src/main/webapp/js, pour added/updated models/views.

   Par exemple, l’ajout d’un nouveau modèle Sharequeue, par exemple mySharequeue, modifiez :

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   To

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Mettez à jour `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` en cas de changement/ajout d’alias dans `main.js`.

   Par exemple, l’ajout d’un nouveau modèle Sharequeue, par exemple mySharequeue, modifiez :

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   To

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. Sur client-html/src/main/webapp/js/minifier, exécutez la commande :

   ```shell
   mvn clean install
   ```

   Il génère un dossier minified-files, sous client-html/src/main/webapp/js avec main.js minifié et registry.js.

>[!NOTE]
>
>La minimisation fonctionne uniquement sur une JVM 64 bits.

>[!NOTE]
>
>Si vous réduisez, votre mise à niveau est affectée.
