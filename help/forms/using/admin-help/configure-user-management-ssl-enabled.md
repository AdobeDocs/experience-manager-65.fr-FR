---
title: Configuration de User Management pour un serveur LDAP compatible SSL
seo-title: Configuration de User Management pour un serveur LDAP compatible SSL
description: Découvrez comment configurer User Management pour un serveur LDAP SSL afin de permettre le fonctionnement correct de la synchronisation sur LDAPS.
seo-description: Découvrez comment configurer User Management pour un serveur LDAP SSL afin de permettre le fonctionnement correct de la synchronisation sur LDAPS.
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuration de User Management pour un serveur LDAP compatible SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Pour un bon fonctionnement de la synchronisation sur LDAPS, les certificats LDAP délivrés par l’autorité de certification doivent être présents dans l’environnement JRE (Java Runtime Environment) du serveur d’applications. Import the certificate into the application server’s JRE cacerts file, which is usually in the *[JAVA_HOME]*/jre/lib/security/cacerts directory.

1. Activez SSL sur le serveur d’annuaire. Pour plus d’informations, consultez la documentation fournie avec l’annuaire.
1. Exportez un certificat client depuis le serveur d’annuaire.
1. Utilisez le programme Keytool pour importer le fichier du certificat client dans le magasin de certificats de la JVM™ (Java Virtual Machine) par défaut du serveur d’applications AEM Forms. La procédure peut varier selon la version de la JVM installée et les chemins d’installation du client. Ainsi, si vous utilisez BEA WebLogic Server avec le JDK 1.5, ouvrez une invite de commande et saisissez ce texte :

   `keytool -import -alias`*alias *`-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. A l’invite, spécifiez votre mot de passe (pour Java, le mot de passe par défaut est `changeit`). Une fois le certificat importé, un message vous confirme la réussite de l’opération.
1. When prompted, type `Yes` to trust the certificate.
1. Activez SSL dans User Management et, lors de la configuration des paramètres d’annuaire, sélectionnez Oui pour l’option SSL puis modifiez la définition du port en conséquence. Le numéro de port par défaut est 636.

>[!NOTE]
>
>si vous rencontrez un problème lors de l’utilisation du protocole SSL, utilisez un navigateur LDAP pour vérifier si le système LDAP est accessible lorsque vous utilisez le protocole SSL. Si le navigateur LDAP n’a pas accès au système, le certificat ou le serveur d’applications n’est pas configuré correctement. Si le navigateur LDAP fonctionne correctement et que les problèmes persistent, User Management n’est pas configuré correctement.

