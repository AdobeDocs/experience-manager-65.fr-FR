---
title: Utilisation de l’éditeur de texte enrichi pour créer du contenu
description: Utilisation de l’éditeur de texte enrichi pour créer du contenu dans Adobe Experience Manager 6.5.
exl-id: 90cb8893-65f3-4d82-9880-ce8dd80891b1
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 100%
---
# Utilisation de l’éditeur de texte enrichi pour créer du contenu {#use-rich-text-editor-to-author-content}

L’éditeur de texte enrichi (RTE) est une composante essentielle à la saisie de contenu textuel dans AEM. Il constitue la base de divers composants, notamment :

* [Texte](https://experienceleague.adobe.com/fr/docs/experience-manager-core-components/using/wcm-components/text)
* [Tableau](https://experienceleague.adobe.com/fr/docs/experience-manager-core-components/using/wcm-components/text#table)

## Édition statique {#in-place-editing}

Si vous sélectionnez un composant texte en cliquant une seule fois dessus, il s’affiche dans la [barre d’outils de composant](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste), comme pour n’importe quel composant.

![screen_shot_2018-03-21at163054](assets/screen_shot_2018-03-21at163054.png)

Appuyez/cliquez de nouveau ou sélectionnez initialement le composant avec un double clic lent pour ouvrir la modification sur place, qui possède sa propre barre d’outils. De là, vous pouvez modifier le contenu et apporter des modifications de base à la mise en forme.

![screen_shot_2018-03-21at163214](assets/screen_shot_2018-03-21at163214.png)

Cette barre d’outils propose les options suivantes :

* **Format** : permet de définir les styles Gras, Italique et Souligné.
* **Listes** : permet de créer des listes à puces ou numérotées, ou de définir une mise en retrait.
* **Lien hypertexte**
* **Dissocier**
* **Plein écran**
* **Fermer**
* **Enregistrer**

## Modification en plein écran {#full-screen-editing}

Dans le cas des composants texte, si vous sélectionnez le mode Plein écran dans la barre d’outils, ![Mode de modification en plein écran](do-not-localize/screen_shot_2018-03-21at163236.png), l’éditeur de texte enrichi s’ouvre et le reste du contenu de la page est masqué.

Le mode Plein écran affiche toutes les options configurées que vous pouvez utiliser pour la création. La disponibilité des options [dépend de la configuration](/help/sites-administering/rich-text-editor.md).

![screen_shot_2018-03-21at163248](assets/screen_shot_2018-03-21at163248.png)

Les options supplémentaires de l’éditeur de texte enrichi sont les suivantes :

* **Ancre** : crée une ancre dans le texte grâce à laquelle vous pourrez ensuite établir un lien ou créer une référence.
* **Aligner le texte à gauche**
* **Texte centré**
* **Aligner le texte à droite**

Pour fermer le mode Plein écran, cliquez sur l’icône Réduire.

![screen_shot_2018-03-21at163323](assets/screen_shot_2018-03-21at163323.png)

>[!NOTE]
>
>La copie de listes imbriquées depuis Microsoft Word dans l’éditeur de texte enrichi peut donner des résultats incohérents et peut nécessiter un ajustement manuel après avoir collé le texte dans l’éditeur de texte enrichi.
