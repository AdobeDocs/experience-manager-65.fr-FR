---
title: Vérificateur de lien
description: Le vérificateur de liens permet de valider les liens internes et externes et de réécrire les liens.
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 2%

---

# Vérificateur de lien {#the-link-checker}

Les auteurs de contenu ne doivent pas se soucier de valider chaque lien qu’ils incluent dans leurs pages de contenu.

Le vérificateur de liens s’exécute automatiquement pour aider les auteurs de contenu avec leurs liens, notamment :

* Validation des liens lorsqu’ils sont ajoutés au contenu
* Affichage d’une liste de tous les liens externes dans le contenu
* Réalisation de transformations de lien

Le vérificateur de liens comporte un certain nombre de [options de configuration](#configuring) par exemple, la définition de la validation interne, ce qui permet à certains liens ou à certains modèles de liens d’être omis de la validation et la réécriture des règles de réécriture de liens.

Le vérificateur de liens valide les deux [liens internes](#internal) et [liens externes.](#external)

>[!NOTE]
>
>Le vérificateur de liens vérifiant les liens de chaque page de contenu, il peut avoir un impact sur les performances des référentiels volumineux. Dans ce cas, vous devrez peut-être [configurer la fréquence d’exécution du vérificateur de liens](#configuring) ou [désactivez-le.](#disabling)

## Vérification des liens internes {#internal}

Les liens internes sont des liens vers d’autres contenus de votre référentiel AEM. Vous pouvez ajouter des liens internes à l’aide du sélecteur de chemin d’accès de l’éditeur de texte enrichi ou d’un composant personnalisé. Par exemple :

* Votre page `/content/wknd/us/en/adventures/ski-touring.html`
* Contenir un lien vers `/content/wknd/us/en/adventures/extreme-ironing.html` dans [Composant Texte.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=fr)

Les liens internes sont validés dès que l’auteur du contenu ajoute un lien interne à une page. Si le lien devient non valide :

* Il est supprimé de l’éditeur. Le texte du lien est conservé, mais le lien lui-même est supprimé.
* Il s’affiche sous la forme d’un lien rompu dans l’interface de création.

![Lien interne rompu lors de la création d’une page](assets/link-checker-invalid-link-internal.png)

## Vérification de lien externe {#external}

Les liens externes sont des liens vers du contenu en dehors de votre référentiel AEM. Vous pouvez ajouter des liens externes à l’aide de l’éditeur de texte enrichi ou d’un composant personnalisé. Par exemple :

* Votre page `/content/wknd/us/en/adventures/ski-touring.html`
* Contenir un lien vers `https://bunwarmerthermalunderwear.com` dans [Composant Texte.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

Les liens externes sont validés pour la syntaxe et en vérifiant leur disponibilité. Cette vérification est effectuée de manière asynchrone sur un système interne configurable. Si le vérificateur de liens trouve un lien externe non valide :

* Il est supprimé de l’éditeur. Le texte du lien est conservé, mais le lien lui-même est supprimé.
* Il s’affiche sous la forme d’un lien rompu dans l’interface de création.

![Lien interne rompu lors de la création d’une page](assets/link-checker-invalid-link-external.png)

En outre, la variable [Vérificateur de lien externe](#external-link-checker) fournit un aperçu de tous les liens externes de vos pages de contenu.

### Utilisation du vérificateur de lien externe {#external-link-checker}

Pour utiliser le vérificateur de lien externe :

1. Avec la **navigation**, sélectionnez **Outils**, puis **Sites**.
1. Sélectionner **Vérificateur de lien externe** et une liste de tous les liens externes s&#39;affiche.

![Fenêtre Vérificateur de lien externe](assets/external-link-checker.png)

Les informations affichées sont les suivantes :

* **État** - L’état de validation du lien, qui peut être l’un des suivants :
   * **Valide** - Le lien externe est accessible par le vérificateur de liens
   * **En attente** - Le lien externe a été ajouté au contenu du site, mais n’a pas encore été validé par le vérificateur de liens.
   * **Non valide** - Le vérificateur de liens ne peut pas accéder au lien externe.
* **URL** - Lien externe
* **Référent** - Page de contenu contenant le lien externe
   * Cette variable n’est renseignée que [s’il est configuré.](#configuring)
* **Dernière vérification** - Dernière fois que le vérificateur de lien a validé le lien externe
   * Fréquence de vérification des liens [est configurable.](#configuring)
* **Dernier état** - Code d’état du dernier HTML renvoyé lors de la dernière vérification du lien effectuée sur le lien externe
* **Dernier disponible** : durée depuis la dernière disponibilité du lien pour le vérificateur de liens
* **Dernier accès** : délai depuis le dernier accès à la page contenant le lien externe dans l’interface de création

Vous pouvez manipuler le contenu de la fenêtre en utilisant les deux boutons situés en haut de la liste des liens :

* **Actualiser** - Pour actualiser le contenu de la liste
* **Vérifier** - Pour vérifier un lien externe individuel sélectionné dans la liste

### Fonctionnement du vérificateur de lien externe {#how-it-works}

Bien qu’il soit facile à utiliser, le vérificateur de lien externe repose sur plusieurs services et comprend leur fonctionnement pour vous aider à comprendre comment [configuration du vérificateur de liens](#configuring) pour répondre à vos besoins.

1. Chaque fois qu’un auteur de contenu enregistre un lien vers une page, un gestionnaire d’événements est déclenché.
1. Le gestionnaire d’événements parcourt tout le contenu sous `/content` et recherche les liens nouveaux ou mis à jour et les ajoute à un cache pour le vérificateur de liens.
1. Le **Service de vérificateur de lien Day CQ** s’exécute ensuite selon un calendrier régulier afin de vérifier les entrées du cache pour une syntaxe valide.
1. Les liens validés par la syntaxe s’affichent alors dans la variable [Vérificateur de lien externe](#external-link-checker) fenêtre. Cependant, ils seront dans un **En attente** état.
1. Le **Tâche du vérificateur de lien Day CQ** s’exécute ensuite régulièrement pour valider les liens en effectuant un appel GET.
1. Le **Tâche du vérificateur de lien Day CQ** met ensuite à jour les entrées de la fenêtre Vérificateur de lien externe avec les résultats des appels de GET.

## Configuration du vérificateur de liens {#configuring}

Le vérificateur de lien est automatiquement disponible dans AEM. Cependant, plusieurs configurations OSGi peuvent être modifiées pour modifier son comportement :

* **Service de stockage d’informations sur le vérificateur de lien Day CQ** - Ce service définit la taille du cache du vérificateur de liens dans le référentiel.
* **Service de vérificateur de lien Day CQ** - Ce service effectue une vérification asynchrone de la syntaxe des liens externes. Vous pouvez définir la période de vérification et les types de liens qui sont ignorés par le vérificateur parmi d’autres options.
* **Tâche du vérificateur de lien Day CQ** - Ce service effectue la validation de GET des liens externes. Il permet de définir des intervalles distincts pour vérifier les liens bons et mauvais entre d’autres options.
* **Transformateur du vérificateur de liens Day CQ** - Permet de convertir des liens en fonction d’un jeu de règles défini par l’utilisateur.

Voir le document [Paramètres de configuration OSGi](/help/sites-deploying/osgi-configuration-settings.md) pour plus d’informations sur la modification des paramètres OSGi.

## Désactivation du vérificateur de liens {#disabling}

Vous pouvez choisir de désactiver entièrement le vérificateur de liens. Pour ce faire :

1. Ouvrez la console OSGi.
1. Modifiez la variable **Transformateur du vérificateur de liens Day CQ**
1. Cochez la ou les options que vous souhaitez désactiver :
   * **Désactiver la vérification** - pour désactiver la validation des liens
   * **Désactiver la réécriture** - pour désactiver les transformations de liens

>[!NOTE]
>
>Si vous désactivez la vérification des liens après avoir commencé à créer votre contenu, il se peut que des entrées apparaissent toujours dans la variable [Fenêtre Vérificateur de lien externe](#external-link-checker), mais elles ne seront plus mises à jour.
