---
title: Utilisation des commentaires
seo-title: Utilisation des commentaires
description: La fonction Commentaires permet aux visiteurs connectés du site de partager leurs opinions et leurs connaissances.
seo-description: La fonction Commentaires permet aux visiteurs connectés du site de partager leurs opinions et leurs connaissances.
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 30%

---

# Utilisation des commentaires {#using-comments}

## Présentation {#introduction}

La fonction Commentaires permet aux visiteurs connectés (membres) d’échanger leurs opinions et leurs connaissances concernant le contenu du site. Cette fonction est souvent déjà présente dans d’autres fonctions, mais peut être ajoutée à n’importe quel site web.

Le document décrit :

* Ajout de `Comments` à une page.
* Paramètres de configuration du composant `Comments`.

>[!NOTE]
>
>La publication anonyme d’un commentaire n’est pas possible. Les visiteurs du site doivent s’inscrire (devenir membres) et se connecter pour participer.

### Ajout de commentaires à une page {#adding-comments-to-a-page}

Pour ajouter un composant `Comments` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Comments`

et faites glisser le composant sur une page, par exemple à un endroit relatif à la fonction pour que les utilisateurs puissent commenter, ou simplement au bas de la page.

Pour plus d’informations, voir [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque les [bibliothèques côté client requises](/help/communities/essentials-comments.md#essentials-for-client-side) sont incluses, voici comment le composant `Comments` apparaît.

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>Un seul composant `Comments` peut exister sur une page. Sachez que de nombreuses fonctions d’AEM Communities incluent déjà des commentaires. C’est le cas des blogs, des calendriers, des forums, des Q&amp;R et des révisions.

### Configuration des commentaires {#configuring-comments}

Sélectionnez le composant `Comments` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![icône de configuration](assets/configure.png)

![comments settings](assets/commentssettings.png)

#### Onglet Commentaires {#comments-tab}

Sous l’onglet **Commentaires**, indiquez la façon dont les commentaires seront entrés par les visiteurs.

* **Autoriser les réponses**

   Si cette case est cochée, les membres ont la possibilité de répondre aux commentaires existants. La valeur par défaut est désélectionnée.

* **Commentaires par page**

   Limite le nombre de commentaires affichés par page et le nombre de réponses affichées. La valeur par défaut est 10.

* **Autoriser les transferts de fichiers**

   Si cette case est cochée, l’option permettant de télécharger un fichier est présentée avec la zone de saisie de texte. La valeur par défaut est désélectionnée.

* **Taille maximale du fichier**

   À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Cette valeur limite la taille du fichier téléchargé. La limite par défaut est de 10 Mo.

* **Longueur de message max.**

   Nombre maximal de caractères pouvant être saisis dans la zone de texte. La valeur par défaut est de 4 096 caractères.

* **Types de fichier autorisés**

   À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Liste d’extensions de nom de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne sont pas autorisés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **Éditeur de texte enrichi**

   Si cette case est cochée, les commentaires sont saisis avec un balisage. La valeur par défaut est désélectionnée.

* **Autoriser le vote**

   Si cette case est cochée, l’option permettant de voter vers le haut ou vers le bas est présentée avec la zone de saisie de texte. La valeur par défaut est désélectionnée.

* **Autoriser abonnement**

   Si cette option est cochée, les membres ont le droit de suivre les commentaires. La valeur par défaut est désélectionnée.

* **Afficher les badges**

   Si cette case est cochée, les badges mérités et attribués doivent s’afficher. La valeur par défaut est désélectionnée.

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous l’onglet **Modération d’utilisateur** , indiquez comment les commentaires publiés sont gérés. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

* **Prémodération**

   Si cette case est cochée, les commentaires doivent être approuvés avant d’apparaître sur un site de publication. La valeur par défaut est désélectionnée.

* **Supprimer les commentaires**

   Si cette case est cochée, le membre qui a publié le commentaire peut le supprimer. La valeur par défaut est désélectionnée.

* **Refuser les commentaires**

   Si cette case est cochée, autorisez les modérateurs à refuser les commentaires. La valeur par défaut est désélectionnée.

* **Fermer/rouvrir les commentaires**

   Si cette case est cochée, les modérateurs peuvent fermer et rouvrir les commentaires. La valeur par défaut est désélectionnée.

* **Marquer les commentaires**

   Si cette case est cochée, les membres ont le droit de signaler les commentaires comme inappropriés. La valeur par défaut est désélectionnée.

* **Marquer la liste de motifs**

   Si cette case est cochée, les membres ont le droit de choisir dans une liste déroulante la raison pour laquelle ils ont marqué un commentaire comme étant inapproprié. La valeur par défaut est désélectionnée.

* **Motif de la marque personnalisée**

   Si cette case est cochée, autorisez les membres à indiquer leur propre raison de signaler un commentaire comme inapproprié. La valeur par défaut est désélectionnée.

* **Seuil de modération**

   Saisissez le nombre de fois qu’un commentaire doit être marqué par les membres avant que les modérateurs ne soient informés. La valeur par défaut est une fois (1).

* **Limite de marquage**

   Saisissez le nombre de fois qu’un commentaire doit être marqué avant qu’il ne soit plus visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au **seuil de modération**. La valeur par défaut est 5.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet **Paramètres de tri**, indiquez comment les commentaires publiés sont triés lorsqu’ils sont affichés.

* **Champ de tri**

   Appuyez sur la touche pour sélectionner `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed` ou `Most Liked`.

* **Ordre de tri**

   Appuyez sur la touche pour sélectionner l’une des valeurs `Ascending` ou `Descending`.

### Modification d’un type de commentaire personnalisé {#changing-to-a-custom-comment-type}

En modifiant le type de ressource de commentaire, le système de commentaires ne génère plus une instance d’un commentaire à l’aide de la valeur par défaut, mais une instance qui a été personnalisée (étendue) par les développeurs.

Une fois les types de ressources personnalisés connus, saisissez [Mode de conception](/help/sites-authoring/default-components-designmode.md) et double-cliquez sur le composant `Comments` inséré pour ouvrir une boîte de dialogue avec un onglet supplémentaire.

Sous l’onglet **Types de ressource** , spécifiez le type de ressource personnalisé pour les nouvelles instances des composants `Comments or Voting` :

![resource-type](assets/resource-type.png)

* **Type de ressource de commentaire**

   Accédez au resourceType d’un composant `comment` étendu (commentaire unique) dans /apps. Par exemple, `/apps/social/commons/components/hbs/comments/comment`

   Cette ressource identifie le type de ressource du contenu créé par un visiteur lorsqu’il publie un commentaire.

* **Type de ressource de vote**

   Accédez au resourceType d’un composant `voting` étendu dans /apps. Par exemple, `/apps/social/components/hbs/voting`

   Cette ressource identifie le type de ressource du contenu créé par un visiteur lorsqu’il publie un vote.

* **Type de ressource système de commentaires**

   Accédez au resourceType d’un composant `comments`étendu (système de commentaires) dans /apps. Laissez vide, sauf si le modèle de page [inclut dynamiquement](/help/communities/scf.md#add-or-include-a-communities-component) le système de commentaires dans le script sous-jacent au lieu d’être ajouté à la page en tant que ressource (noeud de commentaires). Pour en savoir plus, consultez la section [{{include} Helper](/help/communities/handlebars-helpers.md#include).

### Expérience des visiteurs {#site-visitor-experience}

#### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut se charger d’activités de modération autorisées par la configuration du composant, peu importe qui a créé le commentaire.

#### Membres {#members}

Lorsque le visiteur est connecté, selon la configuration, il peut :

* Publier un nouveau commentaire
* Modifier son propre commentaire
* Supprimer son propre commentaire
* Marquer les commentaires des autres

#### Anonyme {#anonymous}

Les visiteurs non connectés peuvent lire les commentaires et les traduire lorsque cela est possible. Toutefois, ils ne sont pas autorisés à ajouter un commentaire, ni à marquer les commentaires d’autres membres.

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur les commentaires](/help/communities/essentials-comments.md) pour les développeurs.

Pour plus d’informations sur la modération des commentaires publiés, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour des informations sur la traduction des commentaires publiés, voir [Traduction de contenu généré par les utilisateurs](/help/communities/translate-ugc.md).
