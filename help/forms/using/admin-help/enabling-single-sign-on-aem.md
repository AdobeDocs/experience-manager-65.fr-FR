---
title: Activation de l’authentification unique dans AEM forms
description: Découvrez comment activer l’authentification unique (SSO) à l’aide d’en-têtes HTTP et de SPNEGO.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 89561ed0-d094-4ef7-9bc1-bde11f3c5bc3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '1520'
ht-degree: 100%

---

# Activation de l’authentification unique dans AEM forms{#enabling-single-sign-on-in-aem-forms}

AEM Forms offre deux méthodes d’activation de l’authentification unique (SSO) : via les en-têtes HTTP et SPNEGO.

Lorsque la fonction SSO est implémentée, les pages de connexion d’utilisateur ou d’utilisatrice d’AEM Forms ne sont plus obligatoires et ne s’affichent pas si la personne est déjà authentifiée via le portail d’entreprise.

Si AEM Forms ne peut pas authentifier une personne à l’aide de l’une de ces méthodes, elle est redirigée vers une page de connexion.

## Activer la fonction SSO à l’aide d’en-têtes HTTP {#enable-sso-using-http-headers}

Vous pouvez utiliser la page de configuration du portail pour activer l’authentification unique (SSO) entre les applications et toute application qui prend en charge le transport de l’identité via l’en-tête HTTP. Lorsque la fonction SSO est implémentée, les pages de connexion d’utilisateur ou d’utilisatrice d’AEM Forms ne sont plus obligatoires et ne s’affichent pas si la personne est déjà authentifiée via le portail d’entreprise.

Vous pouvez également activer la fonction SSO à l’aide de SPNEGO. (voir [Activation de la fonction SSO à l’aide de SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego)).

1. Dans la console d’administration, cliquez sur Paramètres > User Management > Configuration > Configurer les attributs de portail.
1. Sélectionnez Oui pour activer l’authentification unique. Si vous sélectionnez Non, les paramètres restants de la page ne sont pas disponibles.
1. Définissez les autres options de la page selon les besoins, puis cliquez sur OK :

   * **Type d’authentification unique :** (obligatoire) sélectionnez En-tête HTTP pour activer la fonction SSO par le biais d’en-têtes HTTP.
   * **En-tête HTTP de l’identificateur de l’utilisateur :** (obligatoire) nom de l’en-tête dont la valeur contient l’identificateur unique de l’utilisateur connecté. User Management utilise cette valeur pour rechercher l’utilisateur ou l’utilisatrice dans la base de données User Management. La valeur obtenue de cet en-tête doit correspondre à l’identifiant unique de la personne synchronisée à partir du répertoire LDAP. (Voir [Paramètres d’utilisateur ou d’utilisatrice](/help/forms/using/admin-help/adding-configuring-users.md#user-settings).)
   * **La valeur de l’identificateur correspond à l’ID utilisateur de l’utilisateur et non à l’identificateur unique de l’utilisateur :** permet de mapper la valeur d’identificateur unique de l’utilisateur à l’ID utilisateur. Sélectionnez cette option si l’identificateur unique de l’utilisateur est une valeur binaire ne pouvant pas facilement être propagée sur les en-têtes HTTP (par exemple, objectGUID si vous synchronisez des utilisateurs à partir d’Active Directory).
   * **En-tête HTTP du domaine :**(facultatif) nom de l’en-tête dont la valeur contient le nom du domaine. Utilisez ce paramètre uniquement si aucun en-tête HTTP unique n’identifie la personne de manière unique. Utilisez ce paramètre lorsque plusieurs domaines existent et que l’identifiant unique n’est unique que dans un seul domaine. Dans ce cas, indiquez le nom de l’en-tête dans cette zone de texte et spécifiez le mappage des domaines pour les domaines multiples dans la zone Mappage des domaines. (Voir [Modification et conversion de domaines existants](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).)
   * **Mappage de domaine :**(obligatoire) permet de spécifier le mappage de plusieurs domaines, au format *valeur de l’en-tête=nom du domaine*.

     Prenons l’exemple d’une situation où l’en-tête HTTP d’un domaine est domainName et où il peut avoir des valeurs domain1, domain2 ou domain3. Dans ce cas, utilisez le mappage de domaine pour mapper les valeurs domainName aux noms de domaine User Management. Chaque mappage doit se trouver sur une ligne différente :

     domain1=UMdomain1

     domain2=UMdomain2

     domain3=UMdomain3

### Configurer les référents autorisés {#configure-allowed-referers}

Pour connaître les étapes de configuration des référents autorisés, voir [Configuration des référents autorisés](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers).

## Activer la fonction SSO à l’aide de SPNEGO {#enable-sso-using-spnego}

Vous pouvez utiliser le mécanisme de négociation GSSAPI simple et protégé (SPNEGO) pour activer l’authentification unique (SSO) lors de l’utilisation d’Active Directory comme serveur LDAP dans un environnement Windows. Lorsque l’authentification unique est activée, les pages de connexion d’utilisateur ou d’utilisatrice d’AEM Forms ne sont pas requises et n’apparaissent pas.

Vous pouvez également activer la fonction SSO à l’aide d’en-têtes HTTP. (Voir [Activation de la fonction SSO à l’aide d’en-têtes HTTP](enabling-single-sign-on-aem.md#enable-sso-using-http-headers).)

>[!NOTE]
>
>AEM Forms on JEE ne prend pas en charge la configuration de l’authentification unique à l’aide de Kerberos/SPNEGO dans plusieurs environnements d’un domaine enfant .

1. Déterminez le domaine à utiliser pour activer l’authentification unique. Le serveur AEM Forms et les utilisateurs et utilisatrices doivent appartenir au même domaine Windows ou au même domaine de confiance.
1. Dans Active Directory, créez un utilisateur ou une utilisatrice qui représente le serveur AEM Forms. (Voir [Créer un compte d’utilisateur ou d’utilisatrice](enabling-single-sign-on-aem.md#create-a-user-account).) Si vous configurez plusieurs domaines pour utiliser SPNEGO, assurez-vous que les mots de passe de chacun de ces utilisateurs et utilisatrices sont différents. Si les mots de passe ne sont pas différents, l’authentification unique SPNEGO ne fonctionne pas.
1. Mappez le nom principal du service. (Voir [Mappage d’un nom principal de service (SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. Configurez le contrôleur de domaine. (Voir [Prévention des échecs de contrôle d’intégrité de Kerberos](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures).)
1. Ajoutez ou modifiez un domaine d’entreprise comme décrit dans la section [Ajout de domaines](/help/forms/using/admin-help/adding-domains.md#adding-domains) ou [Modification et conversion de domaines existants](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains). Lorsque vous créez ou modifiez le domaine d’entreprise, effectuez les tâches suivantes :

   * Ajoutez ou modifiez un répertoire contenant vos informations Active Directory.
   * Ajoutez LDAP comme fournisseur d’authentification.
   * Ajoutez Kerberos comme fournisseur d’authentification. Fournissez les informations suivantes sur la page Nouvelle authentification ou Modifier l’authentification pour Kerberos :

      * **Fournisseur d’authentification :** Kerberos
      * **IP DNS :** l’adresse IP du serveur DNS qui exécute AEM forms. Vous pouvez déterminer cette adresse IP en exécutant `ipconfig/all` sur la ligne de commande.
      * **Hôte KDC :** nom d’hôte complet ou adresse IP du serveur Active Directory utilisé pour l’authentification
      * **Utilisateur du service :** nom principal de service (SPN) transmis à l’outil KtPass. Dans l’exemple précédent, l’utilisateur du service est `HTTP/lcserver.um.lc.com`.
      * **Domaine d’administration du service :** nom de domaine pour Active Directory. Dans l’exemple précédent, le nom de domaine est `UM.LC.COM.`
      * **Mot de passe du service :** mot de passe de l’utilisateur du service. Dans l’exemple précédent, le mot de passe du service est `password`.
      * **Activer SPNEGO :** active l’utilisation de SPNEGO pour l’authentification unique (SSO). Sélectionnez cette option.

1. Configurez les paramètres du navigateur client SPNEGO. (Voir [Configuration des paramètres du navigateur client SPNEGO](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings).)

### Créer un compte d’utilisateur ou d’utilisatrice {#create-a-user-account}

1. Dans SPNEGO, enregistrez un service en tant qu’utilisateur ou qu’utilisatrice dans Active Directory sur le contrôleur de domaine pour représenter AEM Forms. Sur le contrôleur de domaine, accédez au menu Démarrer > Outils d’administration > Utilisateurs et utilisatrices et ordinateurs Active Directory. Si Outils d’administration ne figure pas dans le menu Démarrer, utilisez le Panneau de Contrôle.
1. Cliquez sur le dossier Utilisateurs et utilisatrices pour afficher la liste des utilisateurs et utilisatrices.
1. Cliquez avec le bouton droit sur le dossier d’utilisateurs et d’utilisatrices et sélectionnez Nouveau > Utilisateur ou utilisatrice.
1. Saisissez le prénom/nom et le nom de connexion de l’utilisateur ou de l’utilisatrice, puis cliquez sur Suivant. Par exemple, définissez les valeurs suivantes :

   * **Prénom** : umspnego
   * **Nom de connexion de l’utilisateur ou de l’utilisatrice** : spnegodemo

1. Saisissez un mot de passe. Saisissez par exemple *password*. Assurez-vous que l’option Mot de passe n’expire jamais est sélectionnée et qu’aucune autre option n’est sélectionnée.
1. Cliquez sur Suivant, puis sur Terminer.

### Mapper un nom principal de service (SPN) {#map-a-service-principal-name-spn}

1. Procurez-vous l’utilitaire KtPass. Cet utilitaire est utilisé pour mapper un SPN à un REALM. Vous pouvez obtenir l’utilitaire KtPass dans le pack d’outils ou le kit de ressources Windows Server. (Voir [Outils d’assistance pour Windows Server 2003 Service Pack 1](https://support.microsoft.com/kb/892777).)
1. Dans une invite de commande, exécutez `ktpass` à l’aide des arguments suivants :

   `ktpass -princ HTTP/`*hôte* `-mapuser`*utilisateur* `@`*REALM*

   Par exemple, saisissez le texte suivant :

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   Les valeurs que vous devez fournir sont décrites comme suit :

   **Hôte :** nom qualifié complet du serveur Forms ou URL unique. Dans notre exemple, il s’agit de lcserver.um.lc.com.

   **REALM :** domaine Active Directory du contrôleur de domaine. Dans notre exemple, il s’agit de UM.LC.COM. Assurez-vous de saisir le domaine en majuscules. Pour déterminer le domaine pour Windows 2003, procédez comme suit :

   * Cliquez avec le bouton droit de la souris sur Mon ordinateur et sélectionnez Propriétés.
   * Cliquez sur l’onglet Nom de l’ordinateur. La valeur Nom du domaine est celle que vous recherchez.

   **Utilisateur ou utilisatrice :** nom de connexion du compte d’utilisateur ou d’utilisatrice que vous avez créé dans la tâche précédente. Dans notre exemple, il s’agit de spnegodemo.

Si vous rencontrez cette erreur :

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

essayez de spécifier l’utilisateur ou l’utilisatrice comme spnegodemo@um.lc.com :

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Prévenir les échecs de contrôle d’intégrité de Kerberos {#prevent-kerberos-integrity-check-failures}

1. Sur le contrôleur de domaine, accédez au menu Démarrer > Outils d’administration > Utilisateurs et utilisatrices et ordinateurs Active Directory. Si Outils d’administration ne figure pas dans le menu Démarrer, utilisez le Panneau de Contrôle.
1. Cliquez sur le dossier Utilisateurs et utilisatrices pour afficher la liste des utilisateurs et utilisatrices.
1. Cliquez avec le bouton droit sur le compte d’utilisateur ou d’utilisatrice que vous avez créé lors d’une tâche précédente. Dans notre exemple, le compte d’utilisateur est `spnegodemo`.
1. Cliquez sur Réinitialiser le mot de passe.
1. Saisissez et confirmez le mot de passe saisi précédemment. Dans notre exemple, il s’agit de `password`.
1. Désélectionnez Modifier le mot de passe lors de la prochaine connexion, puis cliquez sur OK.

### Configurer les paramètres du navigateur client SPNEGO {#configuring-spnego-client-browser-settings}

Pour que l’authentification SPNEGO fonctionne, l’ordinateur client doit faire partie du domaine dans lequel le compte d’utilisateur ou d’utilisatrice est créé. Vous devez également configurer le navigateur client pour autoriser l’authentification SPNEGO. De plus, le site qui nécessite une authentification SPNEGO doit être un site de confiance.

Si vous accédez au serveur au moyen du nom de l’ordinateur, par exemple https://lcserver:8080, aucun paramètre n’est nécessaire pour Internet Explorer. Si vous saisissez une URL qui ne contient aucun point (« . »), Internet Explorer traite le site comme un site intranet local. Si vous utilisez un nom qualifié complet pour le site, celui-ci doit être ajouté en tant que site de confiance.

**Configurer Internet Explorer 6.x**

1. Accédez à Outils > Options Internet et cliquez sur l’onglet Sécurité.
1. Cliquez sur l’icône Intranet local, puis sur Sites.
1. Cliquez sur Avancé et, dans la zone Ajouter ce site web à la zone, saisissez l’URL de votre serveur Forms. Par exemple, saisissez `https://lcserver.um.lc.com`
1. Cliquez sur OK jusqu’à la fermeture de toutes les boîtes de dialogue.
1. Testez la configuration en accédant à l’URL de votre serveur AEM Forms. Par exemple, dans la zone URL du navigateur, saisissez `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`.

**Configuration de Mozilla Firefox**

1. Dans la zone d’URL du navigateur, saisissez `about:config`.

   La boîte de dialogue about:config - Mozilla Firefox s’ouvre.

1. Dans la zone Filtre, saisissez `negotiate`
1. Dans la liste qui s’affiche, cliquez sur network.negotiate-auth.trusted-uri, puis saisissez l’une des commandes suivantes selon votre environnement :

   `.um.lc.com` : configure Firefox pour autoriser SPNEGO pour toute URL qui se termine par um.lc.com. Veillez à inclure le point (« . ») au début.

   `lcserver.um.lc.com` : configure Firefox en vue d’autoriser SPNEGO pour un serveur spécifique uniquement. Ne commencez pas cette valeur par un point (« . »).

1. Testez la configuration en accédant à l’application. La page d’accueil de l’application cible doit s’afficher.
