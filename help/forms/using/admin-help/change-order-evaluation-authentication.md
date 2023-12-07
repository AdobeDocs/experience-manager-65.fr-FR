---
title: Modifier l’ordre d’évaluation pour l’authentification
description: Vous pouvez modifier l’ordre dans lequel AEM forms évalue plusieurs fournisseurs d’authentification.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 59%

---

# Modifier l’ordre d’évaluation pour l’authentification {#change-the-order-of-evaluation-for-authentication}

Si vous avez configuré plusieurs fournisseurs d’authentification, vous pouvez modifier l’ordre dans lequel AEM forms les évalue pour authentification. L’ordre des fournisseurs d’authentification répertoriés dans le fichier config.xml détermine l’ordre d’évaluation pour l’authentification.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Importer et exporter des fichiers de configuration.
1. Pour exporter le paramètre de configuration en cours dans un fichier, cliquez sur Exporter, puis enregistrez le fichier de configuration dans un autre emplacement.
1. Recherchez le noeud suivant dans le fichier :

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

   Dans `<entry key="order" value="3" />`, modifiez la valeur de chaque nœud pour définir l’ordre de l’évaluation de l’authentification.

1. Pour importer le fichier mis à jour, dans Gestion des utilisateurs, cliquez sur Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Parcourir pour trouver le fichier, puis sur Importer et enfin sur OK.
