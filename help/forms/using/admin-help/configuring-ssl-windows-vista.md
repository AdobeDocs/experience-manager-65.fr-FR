---
title: Configurer SSL sous Windows Vista
description: Découvrez comment configurer SSL sous Windows Vista. Utilisez Java Keytool pour générer le certificat SSL avec les clés RSA pour l’authentification.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 100%
---
# Configurer SSL sous Windows Vista {#configuring-ssl-on-windows-vista}

Pour configurer SSL sous Windows Vista™, vous avez besoin d’un certificat SSL avec des clés RSA pour l’authentification. Vous pouvez utiliser l’outil Java Keytool pour créer ce certificat.

>[!NOTE]
>
>Windows Vista ne fonctionnera pas avec les clés DSA.

Vous pouvez exécuter Keytool à l’aide d’une seule commande qui inclut toutes les informations requises pour créer le certificat et le fichier de stockage de clés.

**Créer un certificat SSL**

1. Dans une invite de commande, naviguez jusqu’à *`[JAVA HOME]`*/bin et tapez la commande ci-dessous pour créer le certificat et le fichier de stockage des clés :

   `keytool -genkey -keyalg RSA -dname "CN=`*Nom d’hôte* `, OU=`*Nom du groupe* `, O=`*Nom de la société* `,L=`*Nom de la ville* `, S=`*État* `, C=`*Code pays* `" -alias`*« LC Cert »* `-keypass` `key`*_* *mot de passe* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Remplacez *`[JAVA_HOME]`par le répertoire dans lequel le JDK est installé, puis remplacez le texte en italiques par les valeurs correspondant à l’environnement.*

1. Saisissez `changeit` comme mot de passe. Il s’agit du mot de passe par défaut d’une installation Java, mais l’administrateur système peut l’avoir modifié.
