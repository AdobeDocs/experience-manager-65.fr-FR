---
title: Configuration du mot de passe d’administrateur sur l’installation
seo-title: Configuration du mot de passe d’administrateur sur l’installation
description: Découvrez comment modifier le mot de passe d’administrateur sur l’installation AEM.
seo-description: Découvrez comment modifier le mot de passe d’administrateur sur l’installation AEM.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 87%

---


# Configuration du mot de passe d’administrateur sur l’installation{#configure-the-admin-password-on-installation}

## Présentation {#overview}

Depuis la version 6.3, AEM permet de définir le mot de passe d’administrateur à l’aide de la ligne de commande lors de l’installation d’une nouvelle instance.

Avec les versions antérieures d’AEM, le mot de passe du compte administrateur, ainsi que le mot de passe pour d’autres consoles, devaient être modifiés après l’installation.

Cette fonction ajoute la capacité à définir un nouveau mot de passe d’administrateur pour le référentiel et le moteur de servlets pendant l’installation d’une instance AEM, éliminant ainsi la nécessité de le créer manuellement par la suite.

>[!CAUTION]
>
>Notez que la fonction ne couvre pas la console Felix, dont le mot de passe doit être modifié manuellement. Pour plus d’informations, voir la section [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## Comment puis-je l’utiliser ? {#how-do-i-use-it}

Cette fonction se déclenche automatiquement si vous choisissez d’installer AEM via la ligne de commande, au lieu de double-cliquer sur le fichier JAR à partir d’un explorateur de système de fichiers.

La syntaxe générale pour exécuter une instance AEM à partir de la ligne de commande est la suivante :

```shell
java -jar aem6.3.jar
```

Lors de l’exécution de l’instance à partir de la ligne de commande, vous avez la possibilité de modifier le mot de passe administrateur au cours du processus d’installation :

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>L’invite pour modifier le mot de passe administrateur s’affiche uniquement lors de l’installation d’une nouvelle instance AEM.

## À l’aide de l’indicateur -nointeractive  {#using-the-nointeractive-flag}

Vous pouvez également choisir de spécifier le mot de passe dans un fichier de propriétés. Pour ce faire, utilisez l&#39;indicateur `-nointeractive` associé à la propriété système `-Dadmin.password.file`.

Voici un exemple :

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

Le mot de passe dans le fichier `passwordfile.properties` doit avoir le format suivant :

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Si vous utilisez simplement le paramètre `-nointeractive` sans la propriété système `-Dadmin.password.file`, AEM utilisera le mot de passe d&#39;administrateur par défaut sans vous demander de le modifier, répliquant essentiellement le comportement des versions antérieures. Ce mode non interactif peut être utilisé pour les installations automatisées via l’option de ligne de commande dans un script d’installation.

