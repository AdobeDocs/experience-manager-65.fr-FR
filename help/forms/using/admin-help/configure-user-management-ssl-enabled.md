---
title: Configuration de User Management pour un serveur LDAP compatible SSL
description: Découvrez comment configurer User Management pour un serveur LDAP SSL afin de permettre le fonctionnement correct de la synchronisation sur LDAPS.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 100%

---

# Configurer User Management pour un serveur LDAP compatible SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Pour que la synchronisation fonctionne correctement sur LDAPS, les certificats LDAP émis par l’autorité de certification doivent être présents dans l’environnement d’exécution Java (JRE) du serveur d’applications. Importez le certificat dans le fichier cacerts de l’environnement JRE du serveur d’applications, fichier se trouvant généralement dans le répertoire *[JAVA_HOME]*/jre/lib/security/cacerts.

1. Activez SSL sur le serveur d’annuaire. Pour plus d’informations, consultez la documentation fournie avec l’annuaire.
1. Exportez un certificat client depuis le serveur d’annuaire.
1. Utilisez le programme Keytool pour importer le fichier du certificat client dans le magasin de certificats JVM™ (Java Virtual Machine) par défaut du serveur d’applications AEM Forms. La procédure pour cette tâche varie en fonction de la JVM et des chemins d’installation du client. Par exemple, si vous utilisez BEA WebLogic Server avec JDK 1.5, saisissez ce texte à partir d’une invite de commande :

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Lorsque le système vous y invite, saisissez le mot de passe. (Pour Java, le mot de passe par défaut est : `changeit`.) Une fois le certificat importé, un message vous confirme la réussite de l’opération.
1. Lorsque vous y êtes invité, saisissez`Yes` pour approuver le certificat.
1. Activez SSL dans User Management et, lors de la configuration des paramètres d’annuaire, sélectionnez Oui pour l’option SSL puis modifiez la définition du port en conséquence. Le numéro de port par défaut est 636.

>[!NOTE]
>
>si vous rencontrez un problème lors de l’utilisation du protocole SSL, utilisez un navigateur LDAP pour vérifier si le système LDAP est accessible lorsque vous utilisez le protocole SSL. Si le navigateur LDAP n’a pas accès au système, le certificat ou le serveur d’applications n’est pas configuré correctement. Si le navigateur LDAP fonctionne correctement et que vous rencontrez toujours des problèmes, User Management n’est pas configuré correctement.
