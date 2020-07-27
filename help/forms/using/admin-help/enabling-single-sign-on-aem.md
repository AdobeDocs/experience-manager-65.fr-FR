---
title: Activation de l’authentification unique dans AEM forms
seo-title: Activation de l’authentification unique dans AEM forms
description: Découvrez comment activer l’authentification unique (SSO) en utilisant des en-têtes HTTP et SPNEGO.
seo-description: Découvrez comment activer l’authentification unique (SSO) en utilisant des en-têtes HTTP et SPNEGO.
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 95%

---


# Activation de l’authentification unique dans AEM forms{#enabling-single-sign-on-in-aem-forms}

AEM Forms fournit deux méthodes pour activer l’authentification unique (SSO) : les en-têtes HTTP et SPNEGO.

Lorsque la fonction SSO est implémentée, les pages d’ouverture de session utilisateur d’AEM forms ne sont plus obligatoires. Elles ne s’affichent pas si l’utilisateur s’est déjà authentifié via le portail de son entreprise.

Si AEM forms n’est pas en mesure d’authentifier un utilisateur à l’aide de l’une de ces méthodes, l’utilisateur est redirigé vers une page d’ouverture de session.

## Activation de la fonction SSO à l’aide d’en-têtes HTTP {#enable-sso-using-http-headers}

La page Configuration du portail permet d’activer l’authentification unique (SSO) entre les applications et les applications prenant en charge l’acheminement de l’identité via l’en-tête HTTP. Lorsque la fonction SSO est implémentée, les pages d’ouverture de session utilisateur d’AEM forms ne sont plus obligatoires. Elles ne s’affichent pas si l’utilisateur s’est déjà authentifié via le portail de son entreprise.

Vous pouvez également activer la fonction SSO via SPNEGO (voir [Activation de la fonction SSO à l’aide de SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego)).

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Configurer les attributs de portail.
1. Sélectionnez Oui pour activer l’authentification unique. Si vous sélectionnez Non, les autres paramètres de la page ne sont pas disponibles.
1. Définissez les autres options de la page au besoin, puis cliquez sur OK :

   * **Type d’authentification unique :** (obligatoire) sélectionnez En-tête HTTP pour activer la fonction SSO par le biais d’en-têtes HTTP.
   * **En-tête HTTP de l’identificateur de l’utilisateur :** (obligatoire) nom de l’en-tête dont la valeur contient l’identificateur unique de l’utilisateur connecté. Cette valeur sert à rechercher l’utilisateur dans la base de données User Management. La valeur obtenue via cet en-tête doit correspondre à l’identificateur unique de l’utilisateur synchronisé à partir de l’annuaire LDAP (voir [Options utilisateur](/help/forms/using/admin-help/adding-configuring-users.md#user-settings)).
   * **La valeur de l’identificateur correspond à l’ID utilisateur de l’utilisateur et non à l’identificateur unique de l’utilisateur :** permet de mapper la valeur d’identificateur unique de l’utilisateur à l’ID utilisateur. Sélectionnez cette option si l’identificateur unique de l’utilisateur est une valeur binaire ne pouvant pas facilement être propagée sur les en-têtes HTTP (par exemple, objectGUID si vous synchronisez des utilisateurs à partir d’Active Directory).
   * **En-tête HTTP du domaine :**(facultatif) nom de l’en-tête dont la valeur contient le nom du domaine. Utilisez ce paramètre uniquement si plusieurs en-têtes HTTP identifient l’utilisateur de façon unique. Utilisez ce paramètre lorsqu’il existe plusieurs domaines et que l’identificateur n’est unique que dans un seul domaine. Dans ce cas, indiquez le nom de l’en-tête dans cette zone de texte et spécifiez le mappage des domaines dans le champ Mappage de domaine (voir [Modification et conversion de domaines](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)).
   * **Mappage de domaine :**(obligatoire) permet de spécifier le mappage de plusieurs domaines, au format *valeur de l’en-tête=nom du domaine*.

      Par exemple, prenons une situation où l’en-tête HTTP d’un domaine est domainName et où il peut avoir les valeurs domain1, domain2 ou domain3. Dans ce cas, vous devez utiliser le mappage de domaine pour associer des valeurs domainName à des noms de domaine User Management. Chaque mappage doit se trouver sur une ligne distincte :

      domain1=UMdomain1

      domain2=UMdomain2

      domain3=UMdomain3

### Configuration des référents autorisés {#configure-allowed-referers}

Pour connaître la procédure de configuration des référents autorisés, voir [Configuration des référents autorisés](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers).

## Activation de la fonction SSO à l’aide de SPNEGO {#enable-sso-using-spnego}

Vous pouvez recourir au mécanisme SPNEGO (Simple and Protected GSSAPI Negotiation Mechanism) pour activer l’authentification unique (SSO) lors de l’utilisation d’Active Directory sur votre serveur LDAP dans un environnement Windows. Lorsque la fonction SSO est activée, les pages de connexion d’utilisateur AEM forms ne sont pas requises et n’apparaissent pas.

Vous pouvez également activer la fonction SSO à l’aide d’en-têtes HTTP (voir [Activation de la fonction SSO à l’aide d’en-têtes HTTP](enabling-single-sign-on-aem.md#enable-sso-using-http-headers)).

>[!NOTE]
>
>AEM forms on JEE ne prend pas en charge la configuration de l’authentification unique à l’aide de Kerberos/SPNEGO dans plusieurs environnements d’un domaine enfant .

1. Déterminez le domaine à utiliser pour activer la fonction SSO. Les utilisateurs et le serveur AEM forms doivent appartenir au même domaine Windows ou à un domaine de confiance.
1. Dans Active Directory, créez un utilisateur représentant le serveur AEM forms (voir [Création d’un compte utilisateur](enabling-single-sign-on-aem.md#create-a-user-account)). Si vous configurez plusieurs domaines pour qu’ils utilisent SPNEGO, vérifiez que les mots de passe de tous les utilisateurs sont différents. Si des mots de passe sont identiques, l’authentification unique de SPNEGO ne fonctionne pas.
1. Mappez le nom principal de service (voir [Mappage d’un nom principal de service (SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn)).
1. Configurez le contrôleur de domaine (voir [Prévention des échecs de contrôle d’intégrité de Kerberos](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures)).
1. Ajoutez ou modifiez un domaine d’entreprise, comme indiqué dans les sections [Ajout de domaines](/help/forms/using/admin-help/adding-domains.md#adding-domains) ou [Modification et conversion de domaines](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains). Lors de la création ou de la modification du domaine d’entreprise, procédez comme suit :

   * Ajoutez ou modifiez un annuaire qui contient vos informations Active Directory.
   * Ajoutez LDAP en tant que fournisseur d’authentification.
   * Ajoutez Kerberos en tant que fournisseur d’authentification. Fournissez les informations suivantes dans la page Nouvelle authentification ou Modifier l’authentification pour Kerberos :

      * **Fournisseur d’authentification :** Kerberos
      * **IP DNS :** l’adresse IP du serveur DNS qui exécute AEM forms. Vous pouvez déterminer cette adresse IP en exécutant `ipconfig/all` sur la ligne de commande.
      * **Hôte KDC :** nom d’hôte complet ou adresse IP du serveur Active Directory utilisé pour l’authentification
      * **Utilisateur du service :** nom principal de service (SPN) transmis à l’outil KtPass. Dans l’exemple précédent, l’utilisateur du service est `HTTP/lcserver.um.lc.com`.
      * **Domaine d’administration du service :** nom de domaine pour Active Directory. Dans l’exemple précédent, le nom de domaine est `UM.LC.COM.`
      * **Mot de passe du service :** mot de passe de l’utilisateur du service. Dans l’exemple précédent, le mot de passe du service est `password`.
      * **Activer SPNEGO :** active l’utilisation de SPNEGO pour l’authentification unique (SSO). Sélectionnez cette option.

1. Configurez les paramètres du navigateur client SPNEGO (voir [Configuration des paramètres du navigateur client SPNEGO](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings)).

### Création d’un compte utilisateur {#create-a-user-account}

1. Dans SPNEGO, enregistrez un service en tant qu’utilisateur dans Active Directory sur le contrôleur de domaine pour représenter AEM forms. Dans le contrôleur de domaine, sélectionnez Démarrer > Outils d’administration > Utilisateurs et ordinateurs Active Directory. Si les Outils d’administration ne figurent pas dans le menu Démarrer, utilisez le Panneau de configuration.
1. Cliquez sur le dossier Utilisateurs pour afficher une liste des utilisateurs.
1. Cliquez avec le bouton droit de la souris sur le dossier Utilisateurs, puis sélectionnez Nouveau > Utilisateur.
1. Saisissez le prénom/nom et le nom d’ouverture de session de l’utilisateur, puis cliquez sur Suivant. Par exemple, définissez les valeurs suivantes :

   * **Prénom** : umspnego
   * **Nom d’ouverture de session de l’utilisateur** : spnegodemo

1. Saisissez un mot de passe. Saisissez par exemple *password*. Veillez à ce que la seule option activée soit Le mot de passe n’expire jamais.
1. Cliquez sur Suivant, puis sur Terminer.

### Mappage d’un nom principal de service (SPN) {#map-a-service-principal-name-spn}

1. Procurez-vous l’utilitaire KtPass. Cet utilitaire sert au mappage d’un SPN sur un DOMAINE. Vous pouvez obtenir l’utilitaire KtPass dans le pack d’outils ou dans le Kit de ressources techniques de Windows Server (Voir [Outils de support de Windows Server 2003 Service Pack 1](https://support.microsoft.com/kb/892777).)
1. Dans une invite de commande, exécutez `ktpass` à l’aide des arguments suivants :

   `ktpass -princ HTTP/`*hôte *`@`** REALM `-mapuser`*utilisateur *

   Par exemple, saisissez le texte suivant :

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   Les valeurs à fournir sont décrites ci-dessous :

   **hôte :** nom complet du serveur Forms ou URL univoque. Dans notre exemple, il s’agit de lcserver.um.lc.com.

   **DOMAINE :** domaine Active Directory du contrôleur de domaine. Dans notre exemple, il s’agit de UM.LC.COM. Assurez-vous de saisir le domaine en lettres majuscules. Pour déterminer le domaine pour Windows 2003, procédez comme suit :

   * Cliquez sur Poste de travail avec le bouton droit de la souris et sélectionnez Propriétés.
   * Cliquez sur l’onglet Nom de l’ordinateur. La valeur Nom du domaine est celle que vous recherchez.

   **utilisateur :** nom d’ouverture de session du compte utilisateur créé dans la tâche précédente. Dans notre exemple, il s’agit de spnegodemo.

Si vous rencontrez cette erreur :

```java
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

Essayez de spécifier l’utilisateur comme étant spnegodemo@um.lc.com :

```java
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Prévention des échecs de contrôle d’intégrité de Kerberos {#prevent-kerberos-integrity-check-failures}

1. Dans le contrôleur de domaine, sélectionnez Démarrer > Outils d’administration > Utilisateurs et ordinateurs Active Directory. Si les Outils d’administration ne figurent pas dans le menu Démarrer, utilisez le Panneau de configuration.
1. Cliquez sur le dossier Utilisateurs pour afficher une liste des utilisateurs.
1. Cliquez avec le bouton droit de la souris sur le compte utilisateur créé à l’étape précédente. Dans notre exemple, le compte utilisateur est `spnegodemo`.
1. Cliquez sur Réinitialiser le mot de passe.
1. Saisissez puis confirmez le mot de passe saisi précédemment. Dans notre exemple, il s’agit de `password`.
1. Désélectionnez la case à cocher Modifier le mot de passe à la prochaine ouverture de session, puis cliquez sur OK.

### Configuration des paramètres du navigateur client SPNEGO {#configuring-spnego-client-browser-settings}

Pour que l’authentification SPNEGO fonctionne, l’ordinateur client doit faire partie du domaine dans lequel le compte utilisateur a été créé. Vous devez également configurer le navigateur client pour autoriser l’authentification SPNEGO. De même, le site exigeant une authentification SPNEGO doit être un site de confiance.

Si le serveur est accessible à l’aide du nom de l’ordinateur, par exemple https://lcserver:8080, aucun paramètre n’est requis pour Internet Explorer. Si vous saisissez une URL ne contenant aucun point (« . »), Internet Explorer traite le site comme un site intranet local. Si vous utilisez un nom qualifié complet pour le site, ce site doit être de confiance.

**Configuration d’Internet Explorer 6.x**

1. Sélectionnez Outils > Options Internet, puis cliquez sur l’onglet Sécurité.
1. Cliquez sur l’icône Intranet local, puis sur Sites.
1. Cliquez sur Avancé et dans le champ Ajouter ce site Web à la zone, saisissez l’URL du serveur Forms. Par exemple, saisissez `https://lcserver.um.lc.com`
1. Cliquez plusieurs fois sur OK pour fermer toutes les boîtes de dialogue.
1. Testez la configuration en accédant à l’URL du serveur AEM forms. Par exemple, dans la zone URL du navigateur, saisissez `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**Configuration de Mozilla Firefox**

1. In the browser URL box, type `about:config`

   La boîte de dialogue about:config - Mozilla Firefox s’ouvre.

1. Dans la zone Filtre, saisissez `negotiate`
1. Dans la liste qui s’affiche, cliquez sur network.negotiate-auth.trusted-uri, puis saisissez l’une des commandes suivantes selon votre environnement :

   `.um.lc.com`- Configure Firefox pour autoriser SPNEGO pour toute URL se terminant par um.lc.com. Veillez à inclure le point (&quot;.&quot;) au début.

   `lcserver.um.lc.com`  : configure Firefox en vue d’autoriser SPNEGO pour un serveur spécifique uniquement. Ne faites pas précéder cette valeur d’un point (« . »).

1. Testez la configuration en accédant à l’application. La page d’accueil de l’application cible s’affiche.

