---
title: Cet article comprend l’instruction de désinstallation du module complémentaire Forms à l’aide du gestionnaire de modules CRX.
description: Découvrez les étapes de désinstallation du module complémentaire Forms à l’aide du gestionnaire de modules CRX.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 2755e414ea23ebc1472e9c08d832eca93f28311b
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# Désinstallation du module complémentaire AEM Forms à partir de l’instance AEM

Cet article décrit les étapes nécessaires à la désinstallation correcte du module complémentaire AEM Forms à partir d’une instance du SDK AEM Forms. Suivez ces étapes pour garantir la suppression du module complémentaire Forms, afin d’éviter tout problème potentiel avec votre environnement AEM.

## Condition préalable

Veillez à effectuer une sauvegarde pour éviter toute perte de données.

## Pour désinstaller le module complémentaire AEM Forms

Pour désinstaller le module complémentaire AEM Forms, procédez comme suit :

1. **Désinstallez le module complémentaire AEM Forms :**
   1. Accédez au `http://[host]:[port]/crx/de/index.jsp`.
   1. Recherchez et désinstallez le `AEM Forms add-on package`.

   ![Désinstaller le package](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **Supprimez le dossier natif de CRXDE :**
   1. Accédez au `http://[host]:[port]/crx/de/index.jsp`.
   1. Accédez à `/libs/fd/native/install` et supprimer `native` dans CRXDE.

      ![Supprimer le noeud natif de CRX/de](/help/forms/using/assets/native-install-folder-crxde.png)
   1. Enregistrez les modifications.

1. **Arrêtez le SDK AEM Forms :**
   1. Arrêtez l’instance du SDK AEM Forms à l’aide de la commande &quot;Ctrl + C&quot;.

1. **Recherchez le fichier de base et installez les dossiers dans le dossier crx-quickstart .**
   1. Accédez à `..author\crx-quickstart` dans l’instance SDK AEM Forms.
   1. Recherche des dossiers nommés `bedrock` et `install`.
Si elles sont trouvées, assurez-vous qu’elles sont supprimées de la variable `crx-quickstart` dans l’instance SDK AEM Forms.

   >[!NOTE]
   >
   > La variable `bedrock` est à nouveau créé automatiquement lorsque vous redémarrez l’instance du SDK AEM Forms.

1. **Redémarrez l’instance AEM :**
   1. Une fois toutes les étapes précédentes terminées, [redémarrez l’instance du SDK AEM Forms.](/help/forms/using/restart-aem-sdk.md).




