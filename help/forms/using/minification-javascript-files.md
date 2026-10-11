---
title: Minimiser les fichiers JavaScript
description: Instructions permettant de générer du code minimisé après des personnalisations de l’espace de travail AEM Forms pour optimiser les fichiers JS pour le web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
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
source-wordcount: '194'
ht-degree: 100%
---
# Minimiser les fichiers JavaScript {#minification-of-the-javascript-files}

La minimisation supprime du code source les caractères redondants, comme les espaces blancs, les nouvelles lignes et les commentaires. Cela améliore les performances en réduisant la taille du code. La minimisation n’a aucun impact sur la fonctionnalité et réduit la lisibilité du code.

Pour générer un code minimisé pour les modifications sémantiques, effectuez les étapes suivantes.

1. Copiez `client-html/src/main/webapp/js` de src-package dans filesystem.

   >[!NOTE]
   >
   >Voir [Introduction à la personnalisation de l’espace de travail AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) pour plus d’informations sur les packages.

1. Mettez à jour les chemins dans `main.js` sous client-html/src/main/webapp/js, pour added/updated models/views.

   Par exemple, pour ajouter un nouveau modèle Sharequeue, par exemple mySharequeue, modifiez :

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   To

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Mettez à jour `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` en cas de changement/ajout d’alias dans `main.js`.

   Par exemple, pour ajouter un nouveau modèle Sharequeue, par exemple mySharequeue, modifiez :

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

1. Dans client-html/src/main/webapp/js/minifier, exécutez la commande :

   ```shell
   mvn clean install
   ```

   Elle génère un dossier minified-files, sous client-html/src/main/webapp/js avec main.js et registre.js minifiés.

>[!NOTE]
>
>La minimisation fonctionne uniquement sur les JVM 64 bits.

>[!NOTE]
>
>Elle a des effets sur la mise à niveau.
