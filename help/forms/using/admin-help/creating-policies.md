---
title: Création et gestion des stratégies
seo-title: Création et gestion des stratégies
description: Une stratégie est un jeu de paramètres de confidentialité et d’utilisateurs habilités à accéder au document auquel la stratégie est appliquée. Vous pouvez créer et gérer différents types de stratégies à l’aide des formulaires AEM.
seo-description: Une stratégie est un jeu de paramètres de confidentialité et d’utilisateurs habilités à accéder au document auquel la stratégie est appliquée. Vous pouvez créer et gérer différents types de stratégies à l’aide des formulaires AEM.
uuid: 72be06f3-3e90-495e-8425-72380d95704a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fa054d30-c7dc-4b64-acf1-cbcbe8827df5
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '4755'
ht-degree: 85%

---


# Création et gestion des stratégies {#creating-and-managing-policies}

Une *stratégie* définit un jeu de paramètres de confidentialité et d’utilisateurs habilités à accéder au document auquel la stratégie est appliquée. Un *jeu de stratégies* regroupe plusieurs stratégies ayant une finalité commune. Ces jeux de stratégies sont ensuite rendus accessibles à un sous-groupe d’utilisateurs du système. Pour plus d’informations sur les stratégies, voir [Stratégies et documents protégés par une stratégie](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents).

## Types de stratégies {#types-of-policies}

Document Security offre les types de stratégies suivants.

**Stratégies personnelles**

Les utilisateurs peuvent créer, modifier, copier, supprimer et appliquer leurs propres stratégies avec des paramètres appropriés à une situation donnée. Outre les administrateurs, seule la personne qui crée une stratégie peut accéder à cette stratégie personnelle. Les stratégies personnelles s’affichent sur l’onglet Mes stratégies de la page Stratégies.

Les utilisateurs invités peuvent également créer, modifier, copier et supprimer des stratégies personnelles si l’administrateur active cette fonctionnalité.

**Stratégies partagées**

Les administrateurs et les coordinateurs de jeux de stratégies créent des stratégies partagées adaptées aux besoins de confidentialité identifiés par votre entreprise pour différents types de documents et d’utilisateurs. Les stratégies partagées sont regroupées dans des jeux de stratégies et sont accessibles à tous les utilisateurs autorisés (éditeurs, coordinateurs de jeux de stratégies et destinataires de document) pour un jeu de stratégies donné. Les administrateurs et les coordinateurs de jeux de stratégies peuvent activer et désactiver les stratégies partagées. Les stratégies partagées apparaissent dans les jeux de stratégies, sur l’onglet Jeux de stratégies de la page Stratégies.

Lors de sa première installation, Document Security ne comporte qu’une seule stratégie partagée, appelée *Limiter à toutes les entités*. Lorsque cette stratégie est appliquée à un document, tout utilisateur qui peut se connecter à Document Security pourra accéder au document. Cette stratégie est stockée dans le jeu de stratégies nommé *Jeu de stratégies global*. Cette stratégie est désactivée par défaut. Vous pouvez l’activer si elle est adaptée aux besoins de votre entreprise.

**Stratégies générées automatiquement par Microsoft Outlook**

Acrobat vous permet d’appliquer des stratégies aux documents que vous envoyez en tant que pièces jointes dans Microsoft Outlook. Dans Outlook, vous pouvez protéger un document en appliquant une stratégie existante ou une stratégie générée automatiquement par Acrobat avec des paramètres de confidentialité par défaut, au document mis en pièce jointe d’un courrier électronique (Voir *[Aide d’Acrobat](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*.)

>[!NOTE]
>
>pour qu’une stratégie soit disponible dans Outlook, vous devez la définir comme favori dans Acrobat. Toutes les autres stratégies, y compris celles dont vous êtes l’éditeur, ne s’affichent pas dans Outlook.

## Personnes habilitées à créer et gérer des stratégies et des jeux de stratégies  {#who-can-create-and-manage-policies-and-policy-sets}

La façon dont vous interagissez avec les stratégies et les jeux de stratégies dépend de votre rôle au sein de l’entreprise :

**Utilisateurs :** les utilisateurs peuvent créer, modifier et supprimer leurs stratégies personnelles. Les utilisateurs invités peuvent également créer des stratégies personnelles si l’administrateur active cette fonctionnalité.

**Coordinateurs de jeux de stratégies : les coordinateurs de jeux de** stratégies peuvent créer et gérer des stratégies partagées dans les jeux de stratégies où ils sont désignés comme coordinateurs. Au sein de l’organisation, c’est généralement la personne la plus à même de créer des stratégies dans un jeu donné.

**Administrateurs :** les administrateurs peuvent modifier les stratégies personnelles de n’importe quel utilisateur. Ils peuvent créer des stratégies partagées. Ils peuvent également créer, modifier et supprimer des jeux de stratégies et désigner des coordinateurs de jeux de stratégies.

Pour plus d&#39;informations sur les différents rôles de Document Security, consultez la section [À propos des utilisateurs de Document Security](/help/forms/using/admin-help/document-security.md#about-document-security-users).

## Création et modification de stratégies  {#creating-and-editing-policies}

Les utilisateurs peuvent créer ou modifier des stratégies personnelles pour leur propre usage. Les administrateurs et les coordinateurs de jeux de stratégies peuvent créer ou modifier des stratégies partagées pour votre entreprise.

### Eléments à prendre en compte concernant la modification de stratégies  {#considerations-for-editing-policies}

Lorsque vous modifiez une stratégie, les modifications affectent les documents qui sont protégés par cette dernière, ainsi que ceux qui le seront. Par exemple, si vous supprimez des destinataires d’une stratégie appliquée à un document, ces destinataires ne peuvent plus ouvrir le document.

L’état du document détermine le moment où la modification prend effet :

* Si le document est en ligne, la modification est appliquée immédiatement, sauf si l’utilisateur a ouvert le document. Si tel est le cas, l’utilisateur doit fermer le document pour que la modification soit prise en compte.
* Si un destinataire utilise le document hors connexion (par exemple, sur un ordinateur portable), les modifications prennent effet lorsque le destinataire remet le document en ligne et se synchronise avec Document Security en ouvrant un document protégé par une stratégie.

>[!NOTE]
>
>une stratégie générée automatiquement par Acrobat pour les destinataires d’un document joint à un courrier électronique dans Microsoft Outlook n’apparaît pas dans la liste des stratégies. Pour la voir, vous devez impérativement ouvrir la page Détails du document correspondant au document associé.

Lorsque vous modifiez des stratégies, les restrictions ci-après s’appliquent :

* Les utilisateurs invités ne peuvent modifier des stratégies que si l’administrateur active cette fonctionnalité. Si vous n’êtes pas autorisé à modifier des stratégies, l’option Modifier n’est pas disponible.
* Les coordinateurs de jeux de stratégies ne peuvent modifier que les stratégies appartenant à des jeux s’ils possèdent les autorisations appropriées. Ces autorisations sont définies par le super-utilisateur ou l’administrateur de jeux de stratégies dans l’interface d’administration de Document Security.
* Si l’administrateur a supprimé le filigrane configuré pour la stratégie après la création de celle-ci, ce filigrane n’est pas appliqué aux documents si vous modifiez et enregistrez la stratégie. Les filigranes supprimés restent appliqués aux stratégies existantes tant que vous ne modifiez pas la stratégie. Si vous modifiez la stratégie, vous devez sélectionner un autre filigrane pour remplacer celui que vous avez supprimé.
* Vous ne pouvez pas autoriser l’accès anonyme à un document en modifiant la stratégie appliquée. Si vous la modifiez, les utilisateurs doivent ouvrir une session pour accéder au document. Pour autoriser un accès anonyme à ce document, vous devez commencer par supprimer la stratégie dans l’application cliente, puis appliquer une autre stratégie autorisant l’accès anonyme.
* Une stratégie générée automatiquement par Acrobat pour les destinataires d’un document joint à un courrier électronique dans Microsoft Outlook n’apparaît pas dans la liste des stratégies. Pour y accéder, recherchez le document dans la page Documents, ouvrez la page Détails du document et cliquez sur le nom de la stratégie dans la liste des détails du document.

**Création ou modification d’une stratégie**

1. Dans la page Document Security, cliquez sur Stratégies, puis sur l’un des onglets suivants :

   * Pour créer ou modifier une stratégie personnelle, cliquez sur l’onglet Ma stratégie.
   * Pour créer ou modifier une stratégie partagée, cliquez sur l’onglet Jeux de stratégies, si vous y êtes autorisé, puis sur le nom du jeu de stratégies approprié, et enfin sur l’onglet Stratégies.

1. Cliquez sur Créer ou sélectionnez la stratégie à modifier dans la liste.
1. Dans la zone Nom, entrez un nom identifiant la stratégie de manière univoque. Dans la zone Description, décrivez le rôle de la stratégie et ses conditions d’utilisation. Si la stratégie relève d’un jeu de stratégies, le nom et la description apparaissent dans la liste des stratégies pour tous les utilisateurs spécifiés. Les stratégies personnelles ne sont accessibles qu’à l’utilisateur et aux administrateurs.

   Les caractères suivants ne sont pas autorisés dans le nom ou la description :

   * Inférieur à (&lt;)
   * Supérieur à (>)
   * Perluète (&amp;)
   * Apostrophe (’)
   * Guillemet (« »)
   * barre oblique inverse (\)
   * Barre oblique (/)

   Si vous utilisez le caractère suivant dans le nom ou la description, il sera converti en espaces :

   * Retour chariot (caractère ASCII numéro 13)
   * Saut de ligne (caractère ASCII numéro 10)

   >[!NOTE]
   >
   >vous pouvez créer un nom de stratégie qui contient des caractères étendus. Cependant, en cas de comparaison entre deux chaînes, aucune différence n’est faite entre les caractères accentués et non accentués (« e » et « é », par exemple). Si quelqu’un crée une stratégie, une comparaison est lancée pour vérifier s’il en existe déjà une portant le même nom. La comparaison ne fait pas de distinction entre les noms identiques, à l’exception des caractères accentués. La stratégie étant considérée comme existante dans la base de données, aucun ajout n’est possible.

1. Ajoutez des utilisateurs et des groupes à la stratégie et définissez les droits appropriés (voir [Utilisateurs et groupes](creating-policies.md#users-and-groups)).
1. Sous Paramètres généraux, sélectionnez les options appropriées (voir [Paramètres généraux](creating-policies.md#general-settings)).
1. (Facultatif) Sélectionnez un fournisseur d’autorisations externe et spécifiez ses propriétés, le cas échéant Si vous ne souhaitez pas utiliser de fournisseur d’autorisations externe, cliquez sur Supprimer le fournisseur par défaut.

   Le fournisseur d’autorisations externe permet de configurer des propriétés dans la stratégie. Lorsqu’elles sont sélectionnées, le fournisseur les utilise pour évaluer la stratégie. Les propriétés disponibles sont configurées par l’administrateur et par la personne chargée de l’installation du logiciel.

1. Sous Paramètres avancés, sélectionnez les options appropriées (voir [Paramètres avancés](creating-policies.md#advanced-settings)).
1. Sous Paramètres avancés non modifiables, sélectionnez les options appropriées (voir [Paramètres avancés non modifiables](creating-policies.md#unchangeable-advanced-settings)).
1. Cliquez sur Enregistrer. La stratégie apparaît dans la liste des stratégies. Une icône en forme de cercle rouge apparaît en regard de la nouvelle stratégie, indiquant qu’elle est désactivée.

   Pour rendre la stratégie disponible aux utilisateurs, vous devez l’activer (voir [Activation ou désactivation de stratégies partagées](creating-policies.md#enable-or-disable-shared-policies)).

### Utilisateurs et groupes {#users-and-groups}

Dans la zone Utilisateurs et groupes, vous spécifiez les utilisateurs autorisés à accéder aux documents protégés avec la stratégie. Pour chaque utilisateur ou groupe mentionné, vous définissez également les privilèges d’utilisation des documents.

>[!NOTE]
>
>l’éditeur est l’utilisateur qui protège le document avec la stratégie. Cet utilisateur est toujours inclus par défaut dans une stratégie, avec des droits d’accès complets, tels que la capacité de révoquer un accès et de changer de stratégie. Toutefois, les administrateurs peuvent modifier les droits d’accès de l’éditeur relatifs aux stratégies partagées. Ils peuvent par exemple désactiver la capacité de l’éditeur à révoquer l’accès à un document ou à changer de stratégie.

**Ajouter un utilisateur ou un groupe :** pour ajouter un utilisateur ou un groupe d’utilisateurs, cliquez sur Ajouter un utilisateur ou un groupe, puis sur Recherche avancée pour rechercher des utilisateurs ou des groupes. Les utilisateurs disponibles englobent les utilisateurs internes de l’entreprise et les utilisateurs invités enregistrés dans Document Security. Si vous sélectionnez cette option, la page Ajouter un utilisateur ou un groupe s’affiche :

* Dans la zone Rechercher, saisissez le nom ou l’adresse électronique de l’utilisateur ou du groupe.
* Dans la liste Utilisation, sélectionnez Nom ou Adresse électronique.
* Dans la liste Type, sélectionnez Groupe ou Utilisateur.
* Sélectionnez dans la liste le domaine depuis lequel effectuer la recherche, puis cliquez sur Rechercher.
* Lorsque les résultats apparaissent, sélectionnez l’utilisateur ou le groupe à ajouter, puis cliquez sur Ajouter.

>[!NOTE]
>
>si vous avez saisi un nom d’utilisateur invité ou une adresse électronique valide et qu’aucun résultat ne s’affiche, cela signifie que l’utilisateur n’est pas encore enregistré ou que le compte a été supprimé. Vous pouvez soit essayer d’ajouter l’utilisateur en tant qu’utilisateur invité, soit contacter votre administrateur.

**Inviter un nouvel utilisateur :** pour ajouter un utilisateur invité, cliquez sur Inviter un nouvel utilisateur, entrez l’adresse électronique de l’utilisateur dans la zone qui s’affiche, puis cliquez sur Inviter. Cette option n’est disponible que si l’administrateur l’a activée. Lorsque vous ajoutez des utilisateurs invités à une stratégie, Document Security leur envoie par courrier électronique une invitation à s’enregistrer si cela n’a pas déjà été fait. Les utilisateurs doivent cliquer sur le lien dans le courrier électronique pour créer un compte, puis activer ce compte. 

Après leur enregistrement, les utilisateurs invités peuvent utiliser les documents protégés par une stratégie, pour lesquels ils possèdent les autorisations appropriées. Selon les fonctionnalités activées par l’administrateur, les utilisateurs externes peuvent également recevoir l’autorisation d’appliquer des stratégies à des documents, de créer, modifier et supprimer des stratégies, et d’ajouter d’autres utilisateurs externes à des stratégies.

**Ajouter un utilisateur anonyme :** pour autoriser l’accès d’un utilisateur anonyme, cliquez sur Ajouter un utilisateur anonyme. Cette option n’est disponible que si l’administrateur a activé l’accès Utilisateur anonyme à Document Security (voir Configuration du serveur Document Security). Elle permet à n’importe quel utilisateur d’accéder à des documents protégés par cette stratégie, qu’il possède un compte Document Security ou non. Si vous sélectionnez cette option, vous ne pouvez pas ajouter d’autres types d’utilisateurs à la stratégie.

>[!NOTE]
>
>si vous souhaitez autoriser un accès anonyme à un document protégé par une stratégie qui ne permet pas ce type d’accès, vous devez supprimer la stratégie existante, puis en appliquer une qui autorise l’accès anonyme. Si vous changez de stratégie ou si vous la modifiez, les utilisateurs doivent ouvrir une session pour accéder au document.

#### Spécification des droits de documents pour les utilisateurs et les groupes  {#specify-the-document-permissions-for-users-and-groups}

Vous pouvez spécifier les droits de documents pour un utilisateur ou un groupe à la fois, ou sélectionner plusieurs utilisateurs et groupes dans la liste et modifier leurs droits en utilisant les options de la zone des en-têtes de colonne.

Par défaut, tous les documents protégés par une stratégie disposent d’un droit autorisant les utilisateurs à les ouvrir alors qu’ils sont en ligne.

Les onglets Droits et Options apparaissent dans Document Security.

Ces droits de document sont disponibles dans l’onglet Droits. Vous pouvez les appliquer aux fichiers PDF, PTC Pro/E et Microsoft Office.

**Imprimer :** autorise l’utilisateur à imprimer un document protégé par cette stratégie. Pour les fichiers Office et Pro/E, vous pouvez cocher la case Imprimer pour autoriser l’impression, ou la décocher dans le cas contraire. Si vous cochez la case Afficher les droits personnalisés pour PDF, vous pouvez choisir l’une des options suivantes :

**Non autorisé :** l’utilisateur n’est pas autorisé à imprimer le PDF.

**Autorisé :** l’utilisateur est autorisé à imprimer le PDF.

**Basse résolution only :** L’utilisateur est autorisé à imprimer le PDF à basse résolution.

**Modifier :** autorise l’utilisateur à modifier un document protégé par cette stratégie. Pour les fichiers Office et Pro/E, vous pouvez cocher la case Modifier pour autoriser les modifications, ou la décocher dans le cas contraire. Si vous cochez la case Afficher les droits personnalisés pour PDF, vous pouvez choisir l’une des options suivantes :

**Non autorisé :** l’utilisateur n’est pas autorisé à modifier le PDF.

**Any:** User peut modifier le PDF.

**Collaboration :** l’utilisateur est autorisé à collaborer avec d’autres utilisateurs, à l’aide des options de collaboration dans Adobe Acrobat. Cette autorisation permet à l’utilisateur de copier les données d’un formulaire, même si l’autorisation Copier n’est pas explicitement donnée dans la stratégie.

**Modifier les pages :** l’utilisateur est autorisé à ajouter et supprimer des pages et à modifier le contenu du PDF.

**Fill &amp; Sign:** L’utilisateur est autorisé à remplir les champs de formulaire du PDF et à le signer.

**Copier :** autorise l’utilisateur à copier du texte d’un document protégé par cette stratégie.

**Reader d’écran :** cette autorisation s’affiche si vous cochez la case Afficher les autorisations personnalisées pour PDF. Lorsque cette option est sélectionnée, Adobe Acrobat a l’autorisation d’ajouter des balises temporaires sur le PDF pour améliorer sa lisibilité sur un lecteur d’écrans.

Ces droits de document sont disponibles dans l’onglet Options. Vous pouvez les appliquer aux fichiers PDF, PTC Pro/E et Microsoft Office :

**Hors connexion :** autorise l’utilisateur à vue hors connexion d’un document protégé par cette stratégie.

**Validité des autorisations :** sélectionnez Autorisations toujours valides ou définissez une période de validité des autorisations document. Si vous sélectionnez une période de validité, cliquez sur les icônes de calendrier pour sélectionner une date et utilisez les flèches pour spécifier l’heure au format 24 heures. 

Pour les stratégies partagées, les administrateurs peuvent désactiver les privilèges de l’éditeur (l’utilisateur qui applique la stratégie à un document) ci-dessous :

**Révoquer :** autorise l’éditeur du document à révoquer les privilèges d’accès au document.

**Switch :** autorise l’éditeur de document à changer de privilèges de stratégie.

### Paramètres généraux {#general-settings}

La zone Paramètres généraux contient les paramètres suivants :

**Période de validité :** période pendant laquelle le document protégé par une stratégie est accessible aux destinataires autorisés. Plusieurs périodes de validité sont proposées :

**Le document ne sera pas valide après :** Le document est accessible pendant le nombre de jours spécifié à partir du moment où le document a été sécurisé.

**Le document ne sera pas valide après cette date :** Le document est valide à partir de la date d’application de la stratégie au document jusqu’à la date de fin spécifiée.

**Valide de, à:** Le document est valide pendant les dates spécifiées. Le cas échéant, vous pouvez utiliser le calendrier pour sélectionner une date. Pour ce faire, cliquez sur l’icône de calendrier.

**Document toujours valide :** la période de validité du document n’expire pas.

>[!NOTE]
>
>les dates de validité reposent sur le fuseau horaire du système Document Security, et non sur celui de votre ordinateur local.

**Audit :** activez ou désactivez le contrôle des événements associés à un document protégé par une stratégie. Par exemple, Document Security peut enregistrer des événements tels que les tentatives d’ouverture d’un document. Les événements contrôlés sont répertoriés dans la liste de la page Evénements. Si vous ne sélectionnez pas cette option, Document Security n’enregistre pas les événements concernant les documents associés à cette stratégie.

>[!NOTE]
>
>pour rendre la fonction de contrôle opérationnelle, l’administrateur doit également activer le contrôle du serveur dans la page Options de contrôle et de confidentialité.

**Suivi des utilisations étendues :** activez ou désactivez le suivi des utilisations étendues. Document Security prend en charge le suivi des événements d’utilisateur associés aux diverses opérations réalisées sur un fichier PDF. L’objet Document Security peut être accessible à l’aide d’un script Java. Le fait de cliquer sur un bouton, un fichier multimédia en cours de lecture ou l’enregistrement d’un fichier sont quelques exemples d’événements pouvant être envoyés par un fichier PDF protégé par une stratégie. A l’aide de l’objet Document Security, vous pouvez également récupérer des informations sur l’utilisateur. Le suivi des événements peut être activé dans le serveur Document Security au niveau global ou au niveau stratégique.

**Période de location hors connexion :** nombre maximal de jours pendant lesquels le destinataire peut utiliser le document protégé par une stratégie hors connexion (sans une principale connexion Internet ou réseau). A l’issue de cette période d’ouverture, le destinataire doit resynchroniser le document pour continuer à l’utiliser.

### Fournisseurs d’autorisations externes  {#external-authorization-providers}

Sélectionnez les fournisseurs d’authentification externe si vous en avez déjà configuré. Les fournisseurs disponibles sont répertoriés.

### Paramètres d’authentification {#authentication-settings}

Vous pouvez remplacer les paramètres d’authentification que vous avez configuré sur le serveur et spécifier les options d’authentification pertinentes pour cette stratégie. Cochez la case Remplacer les paramètres d’authentification globaux, puis sélectionnez les options d’authentification pertinentes pour cette stratégie. Les options d’authentification suivantes sont disponibles :

**Autoriser l’authentification par mot de passe par nom d’utilisateur :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification par nom d’utilisateur/mot de passe lors de la connexion au serveur.

**Autoriser l’authentification Kerberos :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification Kerberos lors de la connexion au serveur.

**Autoriser l’authentification de certificat client :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification de certificat lors de la connexion au serveur.

**Autoriser l&#39;** authentification étendueSélectionnez pour activer l&#39;authentification étendue. Le fait de sélectionner cette option autorise les applications clientes à utiliser l’authentification étendue. L’authentification étendue fournit des processus d’authentification personnalisés et différentes options d’authentification configurées sur le serveur Document Security.

Si vous remplacez les paramètres d’authentification globaux, vous pouvez choisir les options d’authentification pertinentes pour cette stratégie. Par exemple, si vous aviez activé trois options d’authentification (nom d’utilisateur et mot de passe, certificat du client et authentification étendue) sur le serveur, vous pouvez annuler ce paramètre global et sélectionnez seulement l’authentification étendue pour cette stratégie. Vous devez vous assurer que l’option d’authentification que vous sélectionnez ici est déjà configurée sur le serveur. Dans cet exemple, vous ne pouvez pas sélectionner Kerberos comme option d’authentification, car elle n’est pas configurée sur le serveur.

>[!NOTE]
>
>L’authentification étendue est prise en charge sur Mac OS X doté de la version 11.0.6 d’Adobe Acrobat et ultérieure.

### Paramètres avancés {#advanced-settings}

La zone Paramètres avancés contient les paramètres suivants :

**Filigrane dynamique :** sélectionnez un filigrane à afficher dynamiquement sur les pages d’un document (par exemple, lorsqu’un destinataire imprime le document). Les filigranes dynamiques identifient un document de manière unique, garantissant ainsi sa confidentialité et empêchant toute violation du copyright. Par exemple, l’administrateur peut configurer un filigrane dynamique qui affiche la date, le nom de l’utilisateur ou l’ID de la personne utilisant le document, ou encore le nom de la stratégie utilisée pour protéger le document. Un filigrane permet également d’afficher du texte personnalisé ou des éléments graphiques si la configuration le permettant a été effectuée. Les administrateurs configurent les options des filigranes et, tout comme les utilisateurs, peuvent les appliquer à des stratégies 

(voir [Configuration des filigranes dynamiques](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks)). 

Si vous modifiez une stratégie et que l’administrateur a supprimé un filigrane que vous aviez sélectionné pour cette stratégie, un message apparaît dans la page Modifier la stratégie. Dans ce cas, si vous enregistrez le document modifié, vous devez sélectionner un autre filigrane pour le faire apparaître sur le document.

>[!NOTE]
>
>pour les stratégies qui autorisent les accès anonymes, le nom d’utilisateur et l’ID d’un utilisateur anonyme ne s’affichent pas en filigrane si vous sélectionnez ce type de filigrane.

**Utiliser uniquement les modules externes Acrobat certifiés pour PDF:** lorsque cette option est sélectionnée pour une stratégie, elle spécifie que Acrobat 8.0 et les versions ultérieures doivent s’exécuter en mode certifié lors de l’ouverture de documents sécurisés par la stratégie. Lorsqu’Acrobat s’exécute en mode certifié, il n’ouvre aucun module externe tiers. 

Sélectionnez cette option si un destinataire d’un document crée un module externe susceptible de contourner les systèmes de protection des documents dans Acrobat 8.0 et versions ultérieures. Ne la sélectionnez pas si les destinataires du document doivent utiliser des modules externes tiers dans Acrobat pour interagir avec des documents.

Cette option n’active le mode certifié que dans Acrobat 8.0 ou versions ultérieures ; l’administrateur doit désactiver l’accès pour Acrobat 7.0 

(voir [Configuration du serveur Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server)). 

Cette option ne concerne pas Adobe Reader.

**Message d’erreur d’accès refusé : message** qui s’affiche pour quiconque tente d’ouvrir un document protégé par une stratégie sans autorisation. Ce message apparaît dans Acrobat. Les clients qui ne peuvent pas afficher ce message affichent un message par défaut pour indiquer que l’accès est refusé.

### Paramètres avancés non modifiables  {#unchangeable-advanced-settings}

La zone Paramètres avancés non modifiables contient les paramètres suivants : Vous ne pouvez pas modifier ces paramètres après avoir enregistré la stratégie.

**Algorithme de chiffrement et longueur de clé :** utilisé pour protéger vos documents. Faites votre choix parmi les options suivantes :

* AES 128 bits
* AES 256 bits. Cette option est uniquement prise en charge par Acrobat 9.0 et versions ultérieures. Pour utiliser le chiffrement AES 256 pour les fichiers PDF, récupérez et installez les fichiers Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy. Ces fichiers remplacent les fichiers local_policy.jar et US_export_policy.jar dans le dossier [JAVE_HOME]/lib/security. Par exemple, si vous utilisez Sun JDK 1.6, copiez les fichiers téléchargés dans le dossier [dep root]/Java/jdk1.6.0_26/lib/security. Vous pouvez télécharger ces fichiers à partir de la page de [téléchargements de Java SE](https://java.sun.com/javase/downloads/index.jsp).
* Aucun chiffrement. Cette option est actuellement prise en charge par Acrobat 9.0 et versions ultérieures. Si vous sélectionnez cette option, les options Restrictions du document sont désactivées. Cette option peut s’avérer utile si vous souhaitez recourir à Document Security pour le contrôle des versions ou le suivi d’un document sans chiffrer le document.

**Restrictions du document :** sélectionnez les composants du document PDF à chiffrer. D’autres applications clientes chiffrent le document entier, mais pas les fichiers liés ou incorporés. Faites votre choix parmi les options suivantes :

* Le document en entier, avec ses pièces jointes et ses métadonnées. Les *métadonnées* décrivent le document et son contenu, et vous pouvez les consulter dans la boîte de dialogue Propriétés du document ou à partir du menu avancé d’Acrobat. Dans Acrobat, vous pouvez joindre des fichiers de différents types (fichiers texte, audio et vidéo, par exemple) à des documents PDF.
* Le document et ses pièces jointes, mais pas ses métadonnées.
* Uniquement les pièces jointes du document. Vous pouvez chiffrer les pièces d’un fichier PDF sans chiffrer le contenu du document.

## Activation ou désactivation de stratégies partagées  {#enable-or-disable-shared-policies}

Pour rendre une stratégie partagée disponible, l’administrateur ou le coordinateur de jeux de stratégies doit l’activer. Vous pouvez activer de nouvelles stratégies ou des stratégies qui ont été désactivées. Une stratégie partagée que vous désactivez s’applique toujours aux documents qui sont protégés par celle-ci.

Une croix (X) rouge apparaît en regard d’une stratégie désactivée.

>[!NOTE]
>
>les administrateurs ne peuvent pas désactiver les stratégies personnelles, et les utilisateurs ne peuvent pas activer ou désactiver leurs propres stratégies.

1. Dans la page Document Security, cliquez sur Stratégies, puis sur l’onglet Jeux de stratégies.
1. Cliquez sur le nom du jeu de stratégies approprié, puis sur l’onglet Stratégies.
1. Sélectionnez la case à cocher située en regard de la stratégie appropriée, cliquez sur Activer ou sur Désactiver, puis sur OK.

## Affichage des informations sur une stratégie  {#view-information-about-a-policy}

L’onglet Mes stratégies vous permet de rechercher des stratégies personnelles.

Les jeux de stratégies créés par des administrateurs sont répertoriés dans l’onglet Jeux de stratégies de la page Stratégies, avec plusieurs informations concernant chaque jeu, notamment le nom, la date de modification et la description. Cliquez sur un nom de jeu de stratégies pour afficher ses détails. Les coordinateurs de jeux de stratégies, qui possèdent l’autorisation de gérer les stratégies, peuvent créer des stratégies partagées dans un jeu donné.

Lorsque vous créez ou modifiez une stratégie, une page apparaît dans laquelle vous pouvez configurer des détails comme le nom de la stratégie, les autorisations, les paramètres de confidentialité et les destinataires à inclure dans la stratégie.

L’administrateur peut configurer les paramètres de confidentialité suivants pour une stratégie :

* les options de confidentialité générales, comme la période de validité et la période d’ouverture hors connexion des documents ;
* les utilisateurs autorisés, ainsi que les restrictions et privilèges de document pour chacun de ces utilisateurs ;
* les options de confidentialité avancées, notamment les filigranes dynamiques et le chiffrage de document.

Les utilisateurs peuvent afficher les stratégies qu’ils ont créées, ainsi que les stratégies partagées auxquelles ils ont accès. Les administrateurs peuvent afficher toutes les stratégies partagées et les stratégies personnelles stockées dans Document Security.

Vous pouvez afficher d’autres informations plus détaillées sur une stratégie de la liste, notamment les utilisateurs ou groupes inclus dans la stratégie et les paramètres de confidentialité spécifiés pour ces utilisateurs.

>[!NOTE]
>
>une stratégie générée automatiquement par Acrobat pour les destinataires d’un document joint à un courrier électronique dans Microsoft Outlook n’apparaît pas dans la liste des stratégies. Pour la voir, vous devez impérativement ouvrir la page Détails du document correspondant au document associé.

1. Dans la page Document Security, cliquez sur Stratégies, puis sur l’onglet Mes stratégies.
1. Remplissez les informations de recherche pour rechercher des stratégies personnelles.
1. Sélectionnez la stratégie appropriée dans la liste.
1. Sur la page Détails de la stratégie, vous pouvez afficher les détails se rapportant à la stratégie, la modifier ou afficher les événements liés à cette stratégie.

## Recherche de stratégies  {#search-for-policies}

Les administrateurs peuvent rechercher des stratégies partagées, ainsi que des stratégies personnelles créées par d’autres utilisateurs.

1. Pour rechercher une stratégie partagée, cliquez sur Stratégies, puis sur l’onglet Jeux de stratégies. Cliquez sur un jeu de stratégies puis sur l’onglet Stratégies.

   Pour rechercher une stratégie personnelle, dans la page Document Security, cliquez sur Stratégies, puis sur l’onglet Mes stratégies.

1. Dans la liste Rechercher, sélectionnez une de ces options :

   **ID de stratégie :** numéro d’identification de stratégie généré lorsque l’utilisateur crée la stratégie. Vous devez saisir l’ID de stratégie exact.

   **Nom de la stratégie :** nom de la stratégie. Vous pouvez lancer une recherche sur une partie ou sur l’ensemble de ce nom.

1. Dans la zone de texte, saisissez la valeur correspondante. Par exemple, si vous avez sélectionné Nom de la stratégie, saisissez le nom de la stratégie que vous recherchez.
1. Dans la liste Afficher, indiquez le nombre de résultats de recherche à afficher et cliquez sur Rechercher. Les résultats de la recherche s’affichent.
1. (Facultatif) Pour afficher des informations détaillées sur une stratégie, cliquez dessus.

## Copie d’une stratégie  {#copy-a-policy}

Vous pouvez copier une stratégie existante et l’enregistrer sous un nouveau nom avec une autre description. La copie permet de créer des stratégies en réutilisant des paramètres existants.

Les utilisateurs externes ne peuvent copier des stratégies que si l’administrateur active cette fonctionnalité. Si vous n’êtes pas autorisé à créer des stratégies, l’option Copier n’est pas disponible.

1. Dans la page Document Security, cliquez sur Stratégies, puis sur l’onglet Ma stratégie.
1. Sélectionnez la stratégie appropriée dans la liste.
1. Dans la page Détails de la stratégie, cliquez sur Copier.
1. Dans la zone Nouveau nom de stratégie, saisissez le nom de la nouvelle stratégie. Si vous le souhaitez, vous pouvez indiquer une description dans le champ Description.

   Les caractères suivants ne sont pas autorisés dans le nom ou la description :

   * Inférieur à (&lt;)
   * Supérieur à (>)
   * Perluète (&amp;)
   * Apostrophe (’)
   * Guillemet (« »)
   * barre oblique inverse (\)
   * Barre oblique (/)

   Si vous utilisez le caractère suivant dans le nom ou la description, il sera converti en espaces :

   * Retour chariot (caractère ASCII numéro 13)
   * Saut de ligne (caractère ASCII numéro 10)

   >[!NOTE]
   >
   >vous pouvez créer un nom de stratégie qui contient des caractères étendus. Cependant, en cas de comparaison entre deux chaînes, aucune différence n’est faite entre les caractères accentués et non accentués (« e » et « é », par exemple). Si quelqu’un crée une stratégie, une comparaison est lancée pour vérifier s’il en existe déjà une portant le même nom. La comparaison ne fait pas de distinction entre les noms identiques, à l’exception des caractères accentués. La stratégie étant considérée comme existante dans la base de données, aucun ajout n’est possible.

1. Cliquez sur OK.

## Suppression d’une stratégie  {#delete-a-policy}

Vous pouvez supprimer les stratégies que vous avez créées. Les administrateurs peuvent supprimer les stratégies créées par n’importe quel utilisateur. Les coordinateurs de jeux de stratégies peuvent supprimer des stratégies dans leurs jeux. Une stratégie supprimée continue de s’appliquer aux documents qui sont protégés par celle-ci. Vous pouvez supprimer plusieurs stratégies à la fois.

Les utilisateurs invités ne peuvent supprimer des stratégies que si l’administrateur active cette fonctionnalité. Si vous n’êtes pas autorisé à supprimer des stratégies, l’option Supprimer n’est pas disponible.

1. Dans la page Document Security, cliquez sur Stratégies.
1. Cliquez sur l’onglet Ma stratégie.
1. Pour supprimer une stratégie partagée, cliquez sur l’onglet Jeux de stratégies, puis sur le nom du jeu de stratégies approprié.
1. Sélectionnez la case à cocher située en regard de la stratégie appropriée, cliquez sur Supprimer, puis sur OK.

>[!NOTE]
>
>vous devez utiliser l’application cliente pour supprimer des stratégies dans des documents (voir l’Aide d’Acrobat ou l’Aide des extensions d’Acrobat Reader DC appropriée).

## Tri de la liste des stratégies  {#sort-the-policy-list}

Pour faciliter la recherche de stratégies, vous pouvez en trier la liste par en-tête de colonne. Un triangle situé à côté de l’en-tête de colonne indique la colonne triée. Lorsque le triangle est dirigé vers le haut, l’ordre de tri est croissant et lorsqu’il est dirigé vers le bas, l’ordre de tri est décroissant.

1. Dans la page Document Security, cliquez sur Stratégies, puis sur l’onglet Jeu de stratégies.
1. Sélectionnez un jeu de stratégies, puis cliquez sur l’onglet Stratégies.
1. Cliquez sur l’en-tête de colonne approprié.
1. Pour modifier l’ordre de tri, cliquez de nouveau sur l’en-tête de colonne.

