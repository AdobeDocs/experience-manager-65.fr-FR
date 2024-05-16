---
title: Configurer le mot de passe de liaison LDAP
description: Découvrez comment configurer le champ de mot de passe de liaison avant d’importer le fichier de configuration dans un autre système.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '183'
ht-degree: 100%

---

# Configurer le mot de passe de liaison LDAP{#configure-the-ldap-bind-password}

Pour éviter tout risque de sécurité, le champ du mot de passe de liaison dans le fichier de configuration exporté (config.xml) n’est pas configuré. Avant d’importer le fichier de configuration dans un autre système, assurez-vous de configurer ce mot de passe. Ce mot de passe remplace un mot de passe existant qui est stocké dans la base de données. Un mot de passe nul ne remplace pas une valeur de mot de passe non nulle existante.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Importer et exporter des fichiers de configuration.
1. Pour exporter le paramètre de configuration en cours dans un fichier, cliquez sur Exporter, puis enregistrez le fichier de configuration dans un autre emplacement.
1. Dans le fichier, recherchez le nœud `Domains` > *[Votre nom de domaine]* > `DirectoryConfigs` > `LDAPGroupConfig`. Par exemple :

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   Saisissez une valeur pour `bindpassword` et enregistrez vos modifications.

1. Dans le fichier, recherchez le nœud `Domains` > *[Votre nom de domaine]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`. Par exemple :

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   Saisissez une valeur pour `bindpassword` et enregistrez vos modifications.

1. Pour importer le fichier mis à jour, dans Gestion des utilisateurs, cliquez sur Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Parcourir pour trouver le fichier, puis sur Importer et enfin sur OK.
