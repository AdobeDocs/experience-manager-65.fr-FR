---
title: Configurer le mot de passe d’administrateur sur l’installation
description: Découvrez comment modifier le mot de passe administrateur lors de l’installation d’Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 9%

---

# Configurer le mot de passe d’administrateur sur l’installation{#configure-the-admin-password-on-installation}

## Présentation {#overview}

Depuis la version 6.3, Adobe Experience Manager (AEM) permet de définir le mot de passe administrateur à l’aide de la ligne de commande lors de l’installation d’une nouvelle instance.

Avec les versions précédentes d’AEM, le mot de passe du compte administrateur, ainsi que le mot de passe de diverses autres consoles, devaient être modifiés après l’installation.

Cette fonctionnalité ajoute la possibilité de définir un nouveau mot de passe administrateur pour le référentiel et le moteur de servlet lors de l’installation d’une instance AEM, éliminant ainsi la nécessité de le faire manuellement par la suite.

>[!CAUTION]
>
>La fonctionnalité ne couvre pas la console Felix, pour laquelle le mot de passe doit être modifié manuellement. Pour plus d’informations, voir [Section Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## Comment Puis-Je L’Utiliser ? {#how-do-i-use-it}

Cette fonctionnalité se déclenche automatiquement si vous choisissez d’installer AEM par le biais de la ligne de commande, au lieu de double-cliquer sur le fichier JAR dans un explorateur de système de fichiers.

La syntaxe générale pour exécuter une instance AEM à partir de la ligne de commande est la suivante :

```shell
java -jar aem6.3.jar
```

Une fois l’instance exécutée à partir de la ligne de commande, vous avez la possibilité de modifier le mot de passe administrateur lors du processus d’installation :

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>L’invite de modification du mot de passe administrateur s’affiche uniquement lors de l’installation d’une nouvelle instance AEM.

## Utilisation de l’indicateur -nointeractive {#using-the-nointeractive-flag}

Vous pouvez également choisir de spécifier le mot de passe dans un fichier de propriétés. Pour ce faire, utilisez la méthode `-nointeractive` l’indicateur associé au `-Dadmin.password.file` propriété système.

Voici un exemple :

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

Le mot de passe à l’intérieur du `passwordfile.properties` doit avoir le format suivant :

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Si vous utilisez simplement la variable `-nointeractive` sans le paramètre `-Dadmin.password.file` système, AEM utilise le mot de passe administrateur par défaut sans vous demander de le modifier, répliquant essentiellement le comportement des versions antérieures. Ce mode non interactif peut être utilisé pour les installations automatisées à l’aide de la ligne de commande dans un script d’installation.
