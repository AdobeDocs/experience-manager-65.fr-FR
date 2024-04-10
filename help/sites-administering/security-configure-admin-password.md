---
title: Configurer le mot de passe d’administrateur sur l’installation
description: Découvrez comment modifier le mot de passe administrateur sur l’installation de Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 10%

---

# Configurer le mot de passe d’administrateur sur l’installation{#configure-the-admin-password-on-installation}

## Présentation {#overview}

Depuis la version 6.3, Adobe Experience Manager (AEM) permet de définir le mot de passe administrateur à l’aide de la ligne de commande lors de l’installation d’une nouvelle instance.

Avec les versions antérieures d’AEM, le mot de passe du compte administrateur, ainsi que le mot de passe de diverses autres consoles, devaient être modifiés après l’installation.

Cette fonctionnalité permet de définir un nouveau mot de passe administrateur pour le référentiel et le moteur de servlet lors de l’installation d’une instance AEM, ce qui élimine la nécessité de le faire manuellement par la suite.

>[!CAUTION]
>
>La fonction ne couvre pas la console Felix, pour laquelle le mot de passe doit être modifié manuellement. Pour plus d’informations, voir la [Section Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## Comment L&#39;Utiliser ? {#how-do-i-use-it}

Cette fonction se déclenche automatiquement si vous choisissez d’installer AEM par le biais de la ligne de commande, au lieu de double-cliquer sur le fichier JAR à partir de l’explorateur de système de fichiers.

La syntaxe générale pour l&#39;exécution d&#39;une instance AEM à partir de la ligne de commande est la suivante :

```shell
java -jar aem6.3.jar
```

Après avoir exécuté l’instance à partir de la ligne de commande, vous avez la possibilité de modifier le mot de passe administrateur pendant le processus d’installation :

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>L’invite de modification du mot de passe administrateur n’apparaît que lors de l’installation d’une nouvelle instance AEM.

## Utilisation de l’indicateur -nointeractive {#using-the-nointeractive-flag}

Vous pouvez également choisir de spécifier le mot de passe dans un fichier de propriétés. Pour ce faire, utilisez le `-nointeractive` indicateur associé à `-Dadmin.password.file` propriété système.

Voici un exemple :

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

Le mot de passe dans le `passwordfile.properties` le fichier doit avoir le format suivant :

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Si vous utilisez simplement le `-nointeractive` paramètre sans `-Dadmin.password.file` propriété système , AEM utilise le mot de passe administrateur par défaut sans vous demander de le modifier, répliquant essentiellement le comportement des versions antérieures. Ce mode non interactif peut être utilisé pour les installations automatisées à l’aide de la ligne de commande d’un script d’installation.
