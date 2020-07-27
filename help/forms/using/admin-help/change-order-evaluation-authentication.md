---
title: Modification de l’ordre d’évaluation pour l’authentification
seo-title: Modification de l’ordre d’évaluation pour l’authentification
description: Vous pouvez modifier l’ordre dans lequel AEM Forms évalue plusieurs fournisseurs d’authentification.
seo-description: Vous pouvez modifier l’ordre dans lequel AEM Forms évalue plusieurs fournisseurs d’authentification.
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 91%

---


# Modification de l’ordre d’évaluation pour l’authentification {#change-the-order-of-evaluation-for-authentication}

Si vous avez configuré plusieurs fournisseurs d’authentification, vous pouvez modifier l’ordre dans lequel AEM forms les évalue pour authentification. L’ordre des fournisseurs d’authentification répertoriés dans le fichier config.xml détermine l’ordre d’évaluation de l’authentification.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Importer et exporter des fichiers de configuration.
1. Pour exporter la configuration en cours dans un fichier, cliquez sur Exporter, puis enregistrez le fichier de configuration à un autre emplacement.
1. Recherchez le nœud ci-après dans le fichier :

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   In `<entry key="order" value="3" />`, edit the value for each node to set the order of the authentication evaluation.

1. Pour importer le fichier mis à jour, dans User Management, cliquez sur Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Parcourir pour rechercher le fichier, sur Importer, puis sur OK.

