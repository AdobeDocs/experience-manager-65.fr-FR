---
title: Configuration de User Management pour un serveur LDAP compatible SSL
description: Découvrez comment configurer User Management pour un serveur LDAP SSL afin de permettre le fonctionnement correct de la synchronisation sur LDAPS.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
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
source-wordcount: '282'
ht-degree: 94%
---
# Configurer User Management pour un serveur LDAP avec SSL activé {#configure-user-management-for-an-ssl-enabled-ldap-server}

Pour que la synchronisation fonctionne correctement sur LDAPS, les certificats LDAP émis par l’autorité de certification (CA) doivent être présents dans l’environnement d’exécution Java (JRE) du serveur d’applications. Importez le certificat dans le fichier cacerts de l’environnement JRE du serveur d’applications, fichier se trouvant généralement dans le répertoire *[JAVA_HOME]*/jre/lib/security/cacerts.

1. Activez SSL sur le serveur d’annuaire. Pour plus d’informations, consultez la documentation fournie par le fournisseur du répertoire.
1. Exportez un certificat client depuis le serveur d’annuaire.
1. Utilisez le programme keytool pour importer le fichier du certificat client dans le magasin de certificats JVM™ (Java Virtual Machine) par défaut du serveur d’applications AEM Forms. La procédure pour cette tâche varie en fonction de la JVM et des chemins d’installation du client. Par exemple, si vous utilisez BEA WebLogic Server avec JDK 1.5, saisissez ce texte à partir d’une invite de commande :

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Lorsque le système vous y invite, saisissez le mot de passe. (Pour Java, le mot de passe par défaut est `changeit`.) Un message s’affiche indiquant que l’importation du certificat a réussi.
1. Lorsque vous y êtes invité, saisissez`Yes` pour approuver le certificat.
1. Activez SSL dans User Management et, lors de la configuration des paramètres d’annuaire, sélectionnez Oui pour l’option SSL puis modifiez le paramètre de port en conséquence. Le numéro de port par défaut est 636.

>[!NOTE]
>
>Si vous rencontrez un problème lors de l’utilisation du protocole SSL, utilisez un navigateur LDAP pour vérifier si le système LDAP est accessible lorsque vous utilisez le protocole SSL. Si le navigateur LDAP n’a pas accès au système, le certificat ou le serveur d’applications n’est pas configuré correctement. Si le navigateur LDAP fonctionne correctement et que vous rencontrez toujours des problèmes, User Management n’est pas configuré correctement.
