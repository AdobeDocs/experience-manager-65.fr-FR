---
title: Créer et gérer des politiques
description: Une stratégie est un ensemble de paramètres de confidentialité et d’utilisateurs qui peuvent accéder au document auquel la stratégie est appliquée. Vous pouvez créer et gérer différents types de stratégies à l’aide d’AEM forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 5e57451c-1a89-442c-8404-841e95d5ceff
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '4713'
ht-degree: 16%

---

# Créer et gérer des politiques {#creating-and-managing-policies}

Une *politique* définit un jeu de paramètres de confidentialité et les utilisateurs et utilisatrices habilités à accéder au document auquel la politique est appliquée. A *jeu de stratégies* est utilisé pour regrouper un ensemble de stratégies ayant un objectif commercial commun. Ces jeux de stratégies sont ensuite mis à la disposition d’un sous-ensemble d’utilisateurs du système. Pour plus d’informations sur les stratégies, voir [Stratégies et documents protégés par une stratégie](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents).

## Types de stratégies {#types-of-policies}

Document Security fournit les types de stratégies suivants.

**Stratégies personnelles**

Les utilisateurs peuvent créer, modifier, copier, supprimer et appliquer leurs propres stratégies avec des paramètres appropriés à une situation donnée. Seule la personne qui crée une stratégie et l’administrateur peut accéder à cette stratégie personnelle. Les stratégies personnelles apparaissent dans l’onglet Mes stratégies de la page Stratégies.

Les utilisateurs invités peuvent également créer, modifier, copier et supprimer des stratégies personnelles si l’administrateur active cette fonctionnalité.

**Stratégies partagées**

Les administrateurs et les coordinateurs de jeux de stratégies créent des stratégies partagées en fonction des exigences de confidentialité que votre entreprise identifie pour différents types de documents et d’utilisateurs. Les stratégies partagées sont contenues dans des jeux de stratégies et sont disponibles pour tous les utilisateurs autorisés (éditeurs, coordinateurs de jeux de stratégies et destinataires de documents) pour un jeu de stratégies particulier. Les administrateurs et les coordinateurs de jeux de stratégies peuvent activer et désactiver des stratégies partagées. Les stratégies partagées apparaissent dans les jeux de stratégies, sous l’onglet Jeux de stratégies de la page Stratégies.

Lors de la première installation de Document Security, celle-ci contient une stratégie partagée nommée *Restreindre à toutes les entités*. Lorsque cette stratégie est appliquée à un document, tout utilisateur qui peut se connecter à Document Security peut accéder au document. Cette stratégie figure dans le jeu de stratégies nommé *Jeu de stratégies global*. Par défaut, cette stratégie n’est pas activée. Vous pouvez l’activer si elle correspond aux besoins de votre entreprise.

**Stratégies générées automatiquement par Microsoft® Outlook**

Acrobat vous permet d’appliquer des stratégies aux documents que vous envoyez en tant que pièces jointes d’email dans Microsoft® Outlook. Dans Outlook, vous pouvez protéger un document à l’aide d’une stratégie existante. Vous pouvez également utiliser une stratégie générée automatiquement par Acrobat avec les paramètres de confidentialité par défaut et l’appliquer au document joint à un message électronique. (Voir *[Aide d’Acrobat](https://help.adobe.com/fr_FR/acrobat/pro/using/index.html)*.)

>[!NOTE]
>
>Pour qu’une stratégie soit disponible dans Outlook, vous devez la définir comme favori dans Acrobat. Toutes les autres stratégies, y compris celles que vous utilisez comme Éditeur, ne s’affichent pas dans Outlook.

## Qui peut créer et gérer des stratégies et des jeux de stratégies {#who-can-create-and-manage-policies-and-policy-sets}

La manière dont vous interagissez avec les stratégies et les jeux de stratégies dépend de votre rôle au sein de l’organisation :

**Utilisateurs :** les utilisateurs peuvent créer, modifier et supprimer leurs politiques personnelles. Les utilisateurs invités peuvent également créer des politiques personnelles si l’administrateur active cette fonctionnalité.

**Coordinateurs de jeux de politiques :** les coordinateurs de jeux de politiques peuvent créer et gérer les politiques partagées figurant dans les jeux de politiques pour lesquels ils ont été désignés en tant que coordinateur. Au sein de l’organisation, c’est généralement la personne la plus à même de créer des politiques dans un jeu donné.

**Administrateurs :** Les administrateurs peuvent modifier les stratégies personnelles de n’importe quel utilisateur. Ils peuvent créer des stratégies partagées. Ils peuvent également créer, modifier et supprimer des jeux de stratégies, et désigner des coordinateurs de jeux de stratégies.

Pour plus d’informations sur les différents rôles de Document Security, consultez la section [À propos des utilisateurs de Document Security](/help/forms/using/admin-help/document-security.md#about-document-security-users).

## Création et modification de stratégies {#creating-and-editing-policies}

Les utilisateurs peuvent créer ou modifier des stratégies personnelles pour leur propre usage. Les administrateurs et les coordinateurs de jeux de stratégies peuvent créer ou modifier des stratégies partagées pour votre organisation.

### Considérations relatives à la modification de stratégies {#considerations-for-editing-policies}

Lorsque vous modifiez une stratégie, les modifications affectent les documents actuellement protégés par la stratégie, ainsi que les documents protégés par la stratégie par la suite. Par exemple, si vous supprimez des destinataires d’une stratégie appliquée à un document, les destinataires ne peuvent plus ouvrir le document.

L’état du document détermine le moment où la modification prend effet :

* Si le document est en ligne, les modifications sont appliquées immédiatement, sauf si l’utilisateur l’a ouvert. Dans ce cas, l’utilisateur doit fermer le document pour que les modifications soient prises en compte.
* Si un destinataire utilise le document hors ligne (par exemple, sur un ordinateur portable), les modifications prennent effet lors de la prochaine mise en ligne du document par le destinataire. Il se synchronise ensuite avec Document Security en ouvrant un document protégé par une stratégie.

>[!NOTE]
>
>Les stratégies qu’Acrobat génère automatiquement pour les destinataires des documents joints aux emails dans Microsoft® Outlook n’apparaissent pas dans la liste des stratégies. Vous ne pouvez afficher ces stratégies qu’en ouvrant la page Détails du document du document associé.

Lorsque vous modifiez des stratégies, ces restrictions s’appliquent :

* Les utilisateurs invités ne peuvent modifier les stratégies que si l’administrateur active cette fonctionnalité. Si vous ne pouvez pas modifier de stratégies, l’option Modifier n’est pas disponible.
* Les coordinateurs de jeux de stratégies ne peuvent modifier les stratégies des jeux de stratégies que s’ils disposent des autorisations appropriées. Le super-utilisateur ou l’administrateur de jeux de stratégies définit ces autorisations dans l’interface d’administration de Document Security.
* Si un filigrane est configuré pour la stratégie et que l’administrateur l’a supprimé depuis la création de la stratégie, ce filigrane ne sera plus appliqué aux documents si vous modifiez et enregistrez la stratégie. Les filigranes supprimés restent en vigueur uniquement pour les stratégies existantes tant que vous ne modifiez pas la stratégie. Si vous modifiez la stratégie, vous devez sélectionner un autre filigrane pour remplacer celui qui a été supprimé.
* Vous ne pouvez pas accorder l’accès anonyme à un document en modifiant la stratégie appliquée. Si vous modifiez la stratégie, les utilisateurs doivent toujours se connecter pour accéder au document. Pour autoriser l’accès anonyme à ce document, vous devez d’abord supprimer la stratégie dans l’application cliente, puis appliquer une autre stratégie autorisant l’accès anonyme.
* Les stratégies qu’Acrobat génère automatiquement pour les destinataires d’un document joint à un message électronique dans Microsoft Outlook n’apparaissent pas dans la liste des stratégies. Pour accéder à cette stratégie, recherchez le document dans la page Documents, ouvrez la page Détails du document, puis cliquez sur le nom de la stratégie dans la liste des détails du document.

**Création ou modification d’une stratégie**

1. Dans la page Document Security, cliquez sur Stratégies, puis sur l’un des onglets suivants :

   * Pour créer ou modifier une stratégie personnelle, cliquez sur l’onglet Ma stratégie .
   * Pour créer ou modifier une stratégie partagée, si vous êtes autorisé, cliquez sur l’onglet Jeux de stratégies , sur le nom du jeu de stratégies approprié, puis sur l’onglet Stratégies .

1. Cliquez sur Nouveau ou sélectionnez la stratégie à modifier dans la liste.
1. Dans la zone Name, saisissez un nom qui identifie de manière unique la stratégie. Dans la zone Description, décrivez le rôle de la stratégie et le moment auquel l’utiliser. Si la stratégie se trouve dans un jeu de stratégies, le nom et la description s’affichent dans la liste des stratégies pour tous les utilisateurs spécifiés. Les stratégies personnelles sont disponibles uniquement pour l’utilisateur et les administrateurs.

   Les caractères suivants ne peuvent pas être utilisés dans le nom ou la description :

   * signe inférieur à (&lt;)
   * signe supérieur à (>)
   * esperluette (&amp;)
   * guillemet simple (&#39;)
   * guillemet double (&quot;)
   * barre oblique inverse (\)
   * Barre oblique (/)

   Si vous avez utilisé le caractère suivant dans le nom ou la description, il est converti en espaces :

   * Retour chariot (caractère ASCII 13)
   * nouvelle ligne (caractère ASCII 10).

   >[!NOTE]
   >
   >Vous pouvez créer un nom de stratégie contenant des caractères étendus. Toutefois, lors d’une comparaison entre deux chaînes, les caractères accentués et non accentués tels que &quot;e&quot; et &quot;é&quot; sont considérés comme identiques. Lorsqu’une personne crée une stratégie, une comparaison est effectuée pour vérifier s’il existe une stratégie portant le même nom. La comparaison ne peut pas distinguer les noms identiques, à l’exception des caractères accentués. On suppose que la stratégie a déjà été ajoutée à la base de données et que la nouvelle stratégie n&#39;a pas été ajoutée.

1. Ajoutez des utilisateurs et des groupes à la stratégie et définissez les autorisations appropriées. (Voir [Utilisateurs et groupes](creating-policies.md#users-and-groups).)
1. Sous Paramètres généraux, sélectionnez les options appropriées. (Voir [Paramètres généraux](creating-policies.md#general-settings).)
1. (Facultatif) Le cas échéant, sélectionnez un fournisseur d’autorisations externe et indiquez ses propriétés. Si vous ne souhaitez pas utiliser de fournisseur d’autorisations externe, cliquez sur Supprimer le fournisseur par défaut.

   Un fournisseur d’autorisations externe est utilisé pour configurer des propriétés dans la stratégie. Lorsqu’il est sélectionné, le fournisseur d’autorisations externe utilise ces informations pour évaluer la stratégie. Les propriétés disponibles sont configurées par l’administrateur et la personne qui installe le logiciel.

1. Sous Paramètres avancés, sélectionnez les options appropriées. (Voir [Paramètres avancés](creating-policies.md#advanced-settings).)
1. Sous Paramètres avancés non modifiables, sélectionnez les options appropriées. (Voir [Paramètres avancés non modifiables](creating-policies.md#unchangeable-advanced-settings).)
1. Cliquez sur Enregistrer. La stratégie apparaît dans la liste des stratégies. Une icône en forme de cercle rouge apparaît en regard de la nouvelle stratégie, indiquant qu’elle est toujours désactivée.

   Pour mettre la stratégie à la disposition des utilisateurs, activez-la. (Voir [Activation ou désactivation de stratégies partagées](creating-policies.md#enable-or-disable-shared-policies).)

### Utilisateurs et groupes  {#users-and-groups}

Dans la zone Utilisateurs et groupes , vous spécifiez les utilisateurs ayant accès aux documents protégés par la stratégie. Pour chaque utilisateur ou groupe que vous spécifiez, vous définissez également les privilèges d’utilisation du document.

>[!NOTE]
>
>L’éditeur est l’utilisateur qui protège le document avec la stratégie. Cet utilisateur est toujours inclus par défaut dans une stratégie, avec des droits d’accès complets, notamment des fonctionnalités de révocation et de changement de stratégie. Toutefois, les administrateurs peuvent modifier les droits d’accès de l’éditeur pour les stratégies partagées. Par exemple, l’administrateur peut empêcher l’éditeur de révoquer l’accès au document ou de changer de stratégie.

**Ajouter un utilisateur ou un groupe :** Pour ajouter un utilisateur ou un groupe d’utilisateurs, cliquez sur Ajouter un utilisateur ou un groupe, puis sur Recherche avancée afin de trouver des utilisateurs ou des groupes. Les utilisateurs incluent les utilisateurs internes de votre entreprise et les utilisateurs invités qui se sont enregistrés auprès de Document Security. Lorsque vous sélectionnez cette option, la page Ajouter un utilisateur ou un groupe s’affiche :

* Dans la zone Rechercher, saisissez le nom ou l’adresse électronique de l’utilisateur ou du groupe.
* Dans la liste Utilisation, sélectionnez Nom ou Adresse électronique.
* Dans la liste Type, sélectionnez Utilisateur ou Groupe.
* Sélectionnez le domaine dans lequel effectuer la recherche, puis cliquez sur Rechercher.
* Lorsque les résultats sont renvoyés, sélectionnez l’utilisateur ou le groupe à ajouter, puis cliquez sur Ajouter.

>[!NOTE]
>
>Si vous saisissez un nom d’utilisateur invité ou une adresse électronique correcte et qu’aucun résultat n’est renvoyé, l’utilisateur n’est peut-être pas encore enregistré ou le compte peut être supprimé. Vous pouvez essayer d’ajouter l’utilisateur en tant qu’utilisateur invité ou contacter votre administrateur.

**Inviter un nouvel utilisateur :** Pour ajouter un utilisateur invité, cliquez sur Inviter un nouvel utilisateur, saisissez l’adresse électronique de l’utilisateur dans la zone qui s’affiche, puis cliquez sur Inviter. Cette option est disponible uniquement si l’administrateur l’a activée. Lorsque vous ajoutez de nouveaux utilisateurs invités à une stratégie, Document Security envoie un courrier électronique d’invitation à l’enregistrement si les utilisateurs ne sont pas déjà invités à s’enregistrer. Les utilisateurs doivent utiliser le lien contenu dans l’e-mail pour créer un compte, puis activer le compte.

Après enregistrement, les utilisateurs invités peuvent utiliser les documents protégés par une stratégie pour lesquels ils disposent d’une autorisation. En fonction des fonctionnalités activées par l’administrateur, les utilisateurs externes peuvent être autorisés à appliquer des stratégies à des documents, à créer, modifier et supprimer des stratégies et à ajouter d’autres utilisateurs externes aux stratégies.

**Ajouter un utilisateur anonyme :** pour autoriser l’accès d’un utilisateur anonyme, cliquez sur Ajouter un utilisateur anonyme. Cette option n’est disponible que si l’administrateur a activé l’accès Utilisateur anonyme à Document Security (voir Configuration du serveur Document Security). Cette option permet à tous les utilisateurs d’accéder aux documents protégés par cette stratégie, qu’ils disposent ou non d’un compte Document Security. Si vous sélectionnez cette option, vous ne pouvez pas ajouter d’autres types d’utilisateurs à la stratégie.

>[!NOTE]
>
>Pour autoriser l’accès anonyme à un document protégé par une stratégie qui ne l’a pas actuellement, supprimez la stratégie existante, puis appliquez une stratégie qui autorise l’accès anonyme. Si vous changez de stratégie ou si vous la modifiez, les utilisateurs doivent toujours se connecter pour accéder au document.

#### Spécification des autorisations de document pour les utilisateurs et les groupes {#specify-the-document-permissions-for-users-and-groups}

Vous pouvez définir des autorisations de document pour un utilisateur ou un groupe à la fois, ou sélectionner plusieurs utilisateurs et groupes dans la liste et modifier leurs autorisations à l’aide des options de la zone des en-têtes de colonne.

Par défaut, tous les documents protégés par une stratégie disposent d’une autorisation qui permet aux utilisateurs de les ouvrir en ligne.

L’onglet Autorisations et options s’affiche dans Document Security.

Ces autorisations de document sont disponibles dans l’onglet Autorisations . Vous pouvez appliquer ces autorisations aux fichiers PDF, PTC Pro/E et Microsoft Office.

**Imprimer :** autorise l’utilisateur à imprimer un document protégé par cette politique. Pour les fichiers Office et Pro/E, vous pouvez cocher la case Imprimer pour autoriser l’impression ou la décocher pour empêcher l’impression. Si vous cochez la case Afficher les autorisations personnalisées pour le PDF , vous pouvez sélectionner l’une des options suivantes :

**Non autorisé :** l’utilisateur n’est pas autorisé à imprimer le PDF.

**Autorisé :** l’utilisateur est autorisé à imprimer le PDF.

**Basse résolution seulement :** l’utilisateur est autorisé à imprimer le PDF en basse résolution.

**Modifier :** autorise l’utilisateur à modifier un document protégé par cette politique. Pour les fichiers Office et Pro/E, vous pouvez cocher la case Modify (Modifier) pour autoriser les modifications ou la décocher pour empêcher les modifications. Si vous cochez la case Afficher les autorisations personnalisées pour le PDF , vous pouvez sélectionner l’une des options suivantes :

**Non autorisé :** l’utilisateur n’est pas autorisé à modifier le PDF.

**Autorisé :** l’utilisateur peut modifier le PDF.

**Collaborer :** l’utilisateur est autorisé à collaborer avec d’autres utilisateurs, en utilisant les options de collaboration d’Adobe Acrobat. Cette autorisation permet à l’utilisateur de copier les données d’un formulaire, même si l’autorisation Copier n’est pas explicitement donnée dans la politique.

**Modifier les pages :** l’utilisateur est autorisé à ajouter et à supprimer des pages, ainsi qu’à modifier du contenu dans le PDF.

**Remplir et signer :** l’utilisateur est autorisé à remplir les champs de formulaire du PDF et à le signer.

**Copier :** autorise l’utilisateur à copier du texte d’un document protégé par cette politique.

**Lecteur d’écran :** cette autorisation s’affiche si vous cochez la case Afficher les droits personnalisés pour PDF. Lorsque cette option est sélectionnée, Adobe Acrobat est autorisé à ajouter des balises temporaires au PDF afin d’améliorer sa lisibilité avec un lecteur d’écran.

Ces autorisations de document sont disponibles dans l’onglet Options . Vous pouvez appliquer ces autorisations aux fichiers PDF, PTC Pro/E et Microsoft Office :

**Hors ligne :** autorise l’utilisateur à afficher hors ligne un document protégé par cette politique.

**Validité des autorisations :** Sélectionnez Autorisations toujours valides ou définissez une période de validité d’autorisation de document. Si vous sélectionnez une période de validité, cliquez sur l&#39;icône de calendrier pour sélectionner une date et utilisez les flèches pour indiquer l&#39;heure au format 24 heures.

Pour les stratégies partagées, les administrateurs peuvent désactiver les privilèges suivants pour l’éditeur de document (l’utilisateur qui applique la stratégie à un document) :

**Révoquer :** autorise l’éditeur du document à révoquer les privilèges d’accès au document.

**Changer :** autorise l’éditeur du document à changer les privilèges des politiques.

### Paramètres généraux {#general-settings}

La zone Paramètres généraux contient les paramètres suivants :

**Période de validité :** période pendant laquelle le document protégé par une politique est accessible aux destinataires autorisés. Plusieurs périodes de validité sont proposées :

**Le document ne sera pas valide après :** le document est accessible pendant le nombre de jours spécifié à partir du moment où il a été protégé.

**Le document ne sera pas valide après cette date :** le document est valide à partir de la date d’application de la politique au document jusqu’à la date de fin spécifiée.

**Valide de, jusqu’à :** le document est valide pendant les dates que vous avez spécifiées. Le cas échéant, vous pouvez utiliser le calendrier pour sélectionner une date. Pour ce faire, cliquez sur l’icône de calendrier.

**Document toujours valide :** la période de validité du document n’expire pas.

>[!NOTE]
>
>les dates de validité reposent sur le fuseau horaire du système Document Security, et non sur celui de votre ordinateur local.

**Réaliser un audit :** permet d’activer ou de désactiver la réalisation d’un audit des événements associés à un document protégé par une politique. Par exemple, Document Security peut enregistrer des événements tels que des tentatives d’ouverture d’un document. Les événements contrôlés apparaissent dans la liste de la page Événements . Si vous ne sélectionnez pas cette option, Document Security n’enregistre pas les événements pour les documents associés à la stratégie.

>[!NOTE]
>
>L’administrateur doit également activer le contrôle du serveur sur la page de configuration des paramètres de contrôle et de confidentialité pour que la fonction de contrôle fonctionne.

**Suivi des utilisations étendues :** activez ou désactivez le suivi des utilisations étendues. Document Security prend en charge le suivi des événements utilisateur associés à diverses opérations effectuées sur un fichier de PDF. Vous pouvez accéder à l’objet Document Security à l’aide d’un script Java. Un clic sur un bouton, un fichier multimédia en cours de lecture ou l’enregistrement d’un fichier sont quelques exemples d’événements déclenchés à partir d’un PDF protégé par une stratégie. À l’aide de l’objet Document Security, vous pouvez également récupérer des informations sur l’utilisateur. Le suivi des événements peut être activé à partir du serveur Document Security au niveau global ou au niveau des stratégies.

**Période d’ouverture hors ligne :** nombre maximum de jours pendant lesquels le destinataire peut utiliser le document protégé par une politique hors ligne (c’est-à-dire sans être connecté à Internet ou à un réseau). À l’issue de cette période d’ouverture, le ou la destinataire doit resynchroniser le document pour continuer à l’utiliser.

### Fournisseurs d’autorisations externes {#external-authorization-providers}

Sélectionnez les fournisseurs d&#39;authentification externes si vous en avez déjà configuré un. Les fournisseurs disponibles sont répertoriés.

### Paramètres d’authentification {#authentication-settings}

Vous pouvez remplacer les paramètres d’authentification que vous avez configurés sur le serveur et spécifier les options d’authentification pertinentes pour cette stratégie. Sélectionnez Remplacer les paramètres d’authentification globaux, puis sélectionnez les options d’authentification pertinentes pour cette stratégie. Les options d’authentification suivantes sont disponibles :

**Autoriser l’authentification par mot de passe du nom d’utilisateur :** Sélectionnez cette option si vous souhaitez permettre aux applications clientes d’utiliser l’authentification par nom d’utilisateur/mot de passe lors de la connexion au serveur.

**Autoriser l’authentification Kerberos :** Sélectionnez cette option si vous souhaitez permettre aux applications clientes d’utiliser l’authentification Kerberos lors de la connexion au serveur.

**Autoriser l’authentification de certificat client :** Sélectionnez cette option si vous souhaitez permettre aux applications clientes d’utiliser l’authentification par certificat lors de la connexion au serveur.

**Autoriser l’authentification étendue :** sélectionnez cette option pour activer l’authentification étendue. La sélection de cette option permet aux applications clientes d’utiliser l’authentification étendue. L’authentification étendue fournit des processus d’authentification personnalisés et différentes options d’authentification configurées sur le serveur Document Security.

Si vous remplacez les paramètres d’authentification globale, vous pouvez choisir les options d’authentification pertinentes pour cette stratégie. Par exemple, si vous avez activé trois options d’authentification (nom d’utilisateur et mot de passe, certificat client et authentification étendue) sur le serveur, vous pouvez remplacer ce paramètre global et sélectionner uniquement l’authentification étendue pour cette stratégie. Assurez-vous que l’option d’authentification que vous sélectionnez ici est déjà configurée sur le serveur. Dans cet exemple, vous ne pouvez pas sélectionner Kerberos comme option d’authentification, car elle n’est pas configurée sur le serveur.

>[!NOTE]
>
>L’authentification étendue est prise en charge sur Apple Mac OS X avec Adobe Acrobat version 11.0.6 et ultérieure.

### Paramètres avancés {#advanced-settings}

La zone Paramètres avancés contient les paramètres suivants :

**Filigrane dynamique :** sélectionnez un filigrane à afficher dynamiquement dans les pages d’un document (par exemple lorsqu’un destinataire imprime le document). Les filigranes dynamiques identifient de manière unique un document, ce qui permet d’assurer la confidentialité de ce dernier et d’empêcher toute violation du droit d’auteur. Par exemple, l’administrateur peut configurer un filigrane dynamique qui affiche la date actuelle, le nom d’utilisateur ou l’identifiant de la personne qui utilise le document. ou le nom de la stratégie utilisée pour protéger le document. Un filigrane peut également afficher du texte ou des éléments graphiques personnalisés, s’ils sont configurés. Les administrateurs configurent les options de filigrane, et les administrateurs et les utilisateurs peuvent les appliquer aux stratégies.

(Voir [Configuration des filigranes dynamiques](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks).)

Si vous modifiez une stratégie et que l’administrateur a supprimé un filigrane configuré que vous avez précédemment sélectionné pour cette stratégie, une note s’affiche sur la page Modifier la stratégie . Dans ce cas, si vous enregistrez le document modifié, sélectionnez un nouveau filigrane si vous souhaitez qu’il apparaisse sur le document.

>[!NOTE]
>
>Dans le cas des stratégies qui autorisent l’accès anonyme d’un utilisateur, le nom d’utilisateur et l’identifiant d’un utilisateur anonyme ne s’affichent pas en filigrane, même si vous sélectionnez ce type de filigrane.

**N’utiliser que des modules externes Acrobat certifiés pour PDF :** lorsque cette option est sélectionnée pour une politique, elle spécifie qu’Acrobat version 8.0 ou ultérieure doit s’exécuter en mode certifié lors de l’ouverture de documents sécurisés par cette politique. Lorsqu’Acrobat s’exécute en mode certifié, il ne charge aucun module externe tiers.

Sélectionnez cette option si un destinataire de document crée un module externe susceptible de contourner les protections de documents dans Acrobat 8.0 et versions ultérieures. Ne sélectionnez pas cette option si les destinataires du document doivent utiliser des modules externes tiers dans Acrobat pour interagir avec les documents.

Cette option active uniquement le mode certifié dans Acrobat 8.0 ou version ultérieure ; l’administrateur doit désactiver l’accès à Acrobat 7.0.

(Voir [Configuration du serveur Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server).)

Cette option ne s’applique pas à Adobe Reader.

**Message d’erreur « Accès refusé » :** message qui s’affiche lorsqu’un utilisateur non autorisé tente d’ouvrir un document protégé par une politique. Ce message apparaît dans Acrobat. Les clients qui ne peuvent pas afficher ce message affichent un message par défaut pour indiquer que l’accès est refusé.

### Paramètres avancés non modifiables {#unchangeable-advanced-settings}

La zone Paramètres avancés non modifiables contient les paramètres suivants. Vous ne pouvez pas modifier ces paramètres une fois la stratégie enregistrée.

**Algorithme de chiffrement et longueur de la clé :** utilisé pour protéger vos documents. Vous pouvez choisir parmi les options suivantes :

* AES 128 bits
* AES 256 bits. Seuls Acrobat 9.0 et versions ultérieures prennent en charge cette option. Pour utiliser le chiffrement AES 256 pour les fichiers PDF, récupérez et installez les fichiers Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy. Ces fichiers remplacent les fichiers local_policy.jar et US_export_policy.jar dans le dossier [JAVE_HOME]/lib/security. Par exemple, si vous utilisez Sun JDK 1.6, copiez les fichiers téléchargés dans le dossier [racine_déploiement]/Java/jdk1.6.0_26/lib/security. Vous pouvez télécharger ces fichiers à partir de [Téléchargements de Java SE](https://java.sun.com/javase/downloads/index.jsp).
* Aucun chiffrement. Acrobat 9.0 et versions ultérieures prennent actuellement en charge cette option. Si vous sélectionnez cette option, les options Restrictions du document sont désactivées. Cette option peut s’avérer utile si vous souhaitez utiliser Document Security pour le contrôle des versions ou le contrôle des documents, mais que vous ne souhaitez pas chiffrer le document.

**Restrictions du document :** sélectionnez les composants du document PDF à chiffrer. D’autres applications clientes chiffrent le document entier, mais pas les fichiers liés ou incorporés. Vous pouvez choisir parmi les options suivantes :

* Le document entier, y compris ses pièces jointes et ses métadonnées. *Métadonnées* est des informations sur le document et son contenu que vous pouvez afficher dans la boîte de dialogue Propriétés du document ou dans le menu Avancé d’Acrobat. Dans Acrobat, vous pouvez joindre des fichiers de différents types (fichiers texte, audio et vidéo, par exemple) à des documents PDF.
* Le document et ses pièces jointes, mais pas les métadonnées.
* Les pièces jointes du document uniquement. Vous pouvez chiffrer les pièces jointes à un fichier de PDF sans chiffrer le contenu du document.

## Activation ou désactivation de stratégies partagées {#enable-or-disable-shared-policies}

Pour qu’une stratégie partagée soit disponible, l’administrateur ou le coordinateur de jeux de stratégies doit l’activer. Vous pouvez activer de nouvelles stratégies ou des stratégies précédemment désactivées. Une stratégie partagée que vous désactivez est toujours appliquée pour les documents protégés par cette stratégie.

Un X rouge apparaît en regard d’une stratégie désactivée.

>[!NOTE]
>
>Les administrateurs ne peuvent pas désactiver les stratégies personnelles, et les utilisateurs ne peuvent pas activer ni désactiver leurs propres stratégies.

1. Dans la page Document Security, cliquez sur Stratégies, puis sur l’onglet Jeux de stratégies.
1. Cliquez sur le nom du jeu de stratégies approprié, puis sur l’onglet Stratégies .
1. Cochez la case en regard de la stratégie appropriée, cliquez sur Activer ou Désactiver, puis sur OK.

## Affichage des informations sur une stratégie {#view-information-about-a-policy}

L’onglet Mes stratégies vous permet de rechercher des stratégies personnelles.

Les jeux de stratégies créés par les administrateurs sont répertoriés dans l’onglet Jeux de stratégies de la page Stratégies. Ils contiennent des informations sur le jeu de stratégies, notamment son nom, la date de création et de modification, ainsi qu’une description. Cliquez sur le nom d’un jeu de stratégies pour en afficher les détails. Les coordinateurs de jeux de stratégies autorisés à gérer les stratégies peuvent créer des stratégies partagées au sein d’un jeu de stratégies spécifique.

Lorsque vous créez ou modifiez une stratégie, une page s’affiche dans laquelle vous pouvez configurer le nom de la stratégie, les niveaux d’autorisation, les paramètres de confidentialité et les destinataires à inclure dans la stratégie.

L’administrateur peut configurer les paramètres de confidentialité suivants pour une stratégie :

* Options générales de confidentialité des documents, telles que la période de validité du document et la période d’ouverture hors connexion
* Les utilisateurs autorisés, ainsi que les restrictions et privilèges du document pour chacun de ces utilisateurs
* Options avancées de confidentialité des documents, notamment les filigranes dynamiques et le chiffrement des documents

Les utilisateurs peuvent afficher les stratégies qu’ils ont créées et les stratégies partagées auxquelles ils ont accès. Les administrateurs peuvent afficher toutes les stratégies partagées et personnelles de Document Security.

Vous pouvez afficher des informations plus détaillées sur une stratégie qui apparaît dans la liste, notamment les utilisateurs ou les groupes inclus dans la stratégie et les paramètres de confidentialité spécifiés pour ces utilisateurs.

>[!NOTE]
>
>Les stratégies qu’Acrobat génère automatiquement pour les destinataires des documents joints aux emails dans Microsoft Outlook n’apparaissent pas dans la liste des stratégies. Vous ne pouvez afficher ces stratégies qu’en ouvrant la page Détails du document du document associé.

1. Dans la page Document Security, cliquez sur Stratégies, puis sur l’onglet Mes stratégies.
1. Renseignez les informations de recherche afin de pouvoir rechercher des stratégies personnelles.
1. Sélectionnez la stratégie appropriée dans la liste.
1. Sur la page Détails de la stratégie, vous pouvez afficher des détails sur la stratégie, la modifier ou afficher les événements liés à la stratégie.

## Recherche de stratégies {#search-for-policies}

Les administrateurs peuvent rechercher des stratégies partagées et des stratégies personnelles créées par d’autres utilisateurs.

1. Pour rechercher une stratégie partagée, cliquez sur Stratégies, puis sur l’onglet Jeux de stratégies. Cliquez sur un jeu de stratégies dans la liste, puis sur l’onglet Stratégies .

   Pour rechercher une stratégie personnelle, dans la page Document Security, cliquez sur Stratégies, puis sur l’onglet Mes stratégies.

1. Dans la liste Rechercher, sélectionnez l’une des options suivantes :

   **ID de politique :** numéro d’identification de politique généré lors de la création de la politique par l’utilisateur. Saisissez l’identifiant de stratégie exact.

   **Nom de la politique :** nom de la politique. Vous pouvez rechercher une partie ou la totalité du nom de la stratégie.

1. Dans la zone de texte, saisissez la valeur correspondante. Par exemple, si vous avez sélectionné Nom de la stratégie, saisissez le nom de la stratégie que vous recherchez.
1. Dans la liste Afficher, sélectionnez le nombre de résultats à afficher, puis cliquez sur Rechercher. Les résultats de la recherche s’affichent.
1. (Facultatif) Pour afficher les détails de la stratégie, cliquez sur la stratégie.

## Copie d’une stratégie {#copy-a-policy}

Vous pouvez copier une stratégie existante et l’enregistrer avec un nouveau nom et une nouvelle description. La copie de stratégies est un moyen efficace de créer des stratégies à l’aide de paramètres existants.

Les utilisateurs externes ne peuvent copier des stratégies que si l’administrateur active cette fonctionnalité. Si vous ne pouvez pas créer de stratégies, l’option Copier n’est pas disponible.

1. Dans la page Document Security, cliquez sur Stratégies, puis sur l’onglet Ma stratégie .
1. Sélectionnez la stratégie appropriée dans la liste.
1. Sur la page Détails de la stratégie, cliquez sur Copier.
1. Dans la zone New Policy Name, saisissez le nouveau nom de la stratégie. Vous pouvez également saisir une nouvelle description.

   Les caractères suivants ne peuvent pas être utilisés dans le nom ou la description :

   * signe inférieur à (&lt;)
   * signe supérieur à (>)
   * esperluette (&amp;)
   * guillemet simple (&#39;)
   * guillemet double (&quot;)
   * barre oblique inverse (\)
   * Barre oblique (/)

   Si vous avez utilisé le caractère suivant dans le nom ou la description, il est converti en espaces :

   * Retour chariot (caractère ASCII 13)
   * nouvelle ligne (caractère ASCII 10).

   >[!NOTE]
   >
   >Vous pouvez créer un nom de stratégie contenant des caractères étendus. Toutefois, lors d’une comparaison entre deux chaînes, les caractères accentués et non accentués tels que &quot;e&quot; et &quot;é&quot; sont considérés comme identiques. Lorsqu’une personne crée une stratégie, une comparaison est effectuée pour vérifier s’il existe une stratégie portant le même nom. La comparaison ne peut pas distinguer les noms identiques, à l’exception des caractères accentués. On suppose que la stratégie a déjà été ajoutée à la base de données et que la nouvelle stratégie n&#39;a pas été ajoutée.

1. Cliquez sur OK.

## Suppression d’une stratégie {#delete-a-policy}

Vous pouvez supprimer les stratégies que vous avez créées. Les administrateurs peuvent supprimer les stratégies que tout utilisateur a créées. Les coordinateurs de jeux de stratégies peuvent supprimer des stratégies dans leurs jeux de stratégies. Une stratégie que vous supprimez est toujours appliquée pour les documents protégés par cette stratégie. Vous pouvez supprimer plusieurs stratégies à la fois.

Les utilisateurs invités ne peuvent supprimer des stratégies que si l’administrateur active cette fonctionnalité. Si vous ne pouvez pas supprimer de stratégies, l’option de suppression n’est pas disponible.

1. Dans la page Document Security, cliquez sur Stratégies.
1. Cliquez sur l’onglet Ma stratégie .
1. Pour supprimer une stratégie partagée, cliquez sur l’onglet Jeux de stratégies , puis sur le nom du jeu de stratégies approprié.
1. Cochez la case en regard de la stratégie appropriée, cliquez sur Supprimer, puis sur OK.

>[!NOTE]
>
>Utilisez l’application cliente pour supprimer des stratégies de documents. (Voir l’aide d’Acrobat ou l’aide des extensions Acrobat Reader DC appropriée.)

## Tri de la liste des stratégies {#sort-the-policy-list}

Vous pouvez trier la liste des stratégies par en-tête de colonne pour trouver plus facilement des stratégies. Une icône en forme de triangle située en regard de l’en-tête de colonne indique la colonne à trier. Un triangle orienté vers le haut indique l’ordre croissant, tandis qu’un triangle orienté vers le bas indique l’ordre décroissant.

1. Dans la page Document Security, cliquez sur Stratégies, puis sur l’onglet Jeu de stratégies .
1. Sélectionnez un jeu de stratégies, puis cliquez sur l’onglet Stratégies .
1. Cliquez sur l’en-tête de colonne approprié.
1. Pour modifier l’ordre de tri, cliquez de nouveau sur la colonne.
