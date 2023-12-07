---
title: Configuration de User Management pour un serveur LDAP compatible SSL
description: Découvrez comment configurer User Management pour un serveur LDAP SSL afin de permettre le fonctionnement correct de la synchronisation sur LDAPS.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 26%

---

# Configurer User Management pour un serveur LDAP compatible SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Pour que la synchronisation fonctionne correctement sur LDAPS, les certificats LDAP émis par l’autorité de certification doivent être présents dans l’environnement d’exécution Java (JRE) du serveur d’applications. Importez le certificat dans le fichier cacerts de l’environnement JRE du serveur d’applications, fichier se trouvant généralement dans le répertoire *[JAVA_HOME]*/jre/lib/security/cacerts.

1. Activez SSL sur le serveur d’annuaire. Pour plus d’informations, consultez la documentation fournie par le fournisseur de votre répertoire.
1. Exportez un certificat client à partir du serveur d’annuaire.
1. Utilisez le programme keytool pour importer le fichier du certificat client dans la boutique de certificats de la machine virtuelle Java (JVM™) par défaut du serveur d’applications d’AEM forms. La procédure pour cette tâche varie en fonction de la JVM et des chemins d’installation du client. Par exemple, si vous utilisez BEA WebLogic Server avec JDK 1.5, saisissez ce texte à partir d’une invite de commande :

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Lorsque vous y êtes invité, saisissez le mot de passe. (Pour Java, le mot de passe par défaut est : `changeit`.) Une fois le certificat importé, un message vous confirme la réussite de l’opération.
1. Lorsque vous y êtes invité, saisissez`Yes` pour approuver le certificat.
1. Activez SSL dans User Management et, lors de la configuration des paramètres d’annuaire, sélectionnez Oui pour l’option SSL et modifiez le paramètre de port en conséquence. Le numéro de port par défaut est 636.

>[!NOTE]
>
>Si vous rencontrez des problèmes lors de l’utilisation de SSL, utilisez un navigateur LDAP pour vérifier s’il peut accéder au système LDAP lors de l’utilisation de SSL. Si le navigateur LDAP ne peut pas accéder à , votre certificat ou serveur d’applications n’est pas configuré correctement. Si le navigateur LDAP fonctionne correctement et que vous rencontrez toujours des problèmes, User Management n’est pas configuré correctement.
