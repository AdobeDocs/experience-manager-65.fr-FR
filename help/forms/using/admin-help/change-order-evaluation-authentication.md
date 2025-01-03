---
title: Modifier l’ordre d’évaluation pour l’authentification
description: Vous pouvez modifier l’ordre dans lequel AEM Forms évalue plusieurs fournisseurs d’authentification.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 100%

---

# Modifier l’ordre d’évaluation pour l’authentification {#change-the-order-of-evaluation-for-authentication}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Si vous avez configuré plusieurs fournisseurs d’authentification, vous pouvez modifier l’ordre dans lequel AEM Forms les évalue pour authentification. L’ordre des fournisseurs d’authentification répertoriés dans le fichier config.xml détermine l’ordre d’évaluation pour l’authentification.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Importer et exporter des fichiers de configuration.
1. Pour exporter le paramètre de configuration en cours dans un fichier, cliquez sur Exporter, puis enregistrez le fichier de configuration dans un autre emplacement.
1. Recherchez le nœud suivant dans le fichier :

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
