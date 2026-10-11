---
title: Créer une racine de langue à l’aide de l’interface utilisateur classique
description: Découvrez comment créer une racine de langue dans Adobe Experience Manager à l’aide de l’interface utilisateur classique.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 1ae21d80-0683-4ab9-afaa-4d733ff47720
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: d9d38edd-df1b-480c-8f5e-72b62576f390
    internal-label: Site and page features
subfeature_v2:
  - id: e15a4109-ae5d-497d-b301-31149e35aed4
    internal-label: Language Copy Wizard
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 98%
---
# Créer une racine de langue à l’aide de l’interface utilisateur classique{#creating-a-language-root-using-the-classic-ui}

La procédure ci-dessous utilise l’interface utilisateur classique pour créer la racine de langue d’un site. Pour plus d’informations, consultez [Création d’une racine de langue](/help/sites-administering/tc-prep.md#creating-a-language-root).

1. Dans la console Sites web, dans l’arborescence des sites web, sélectionnez la page racine du site. ([http://localhost:4502/siteadmin#](http://localhost:4502/siteadmin#))
1. Ajoutez une nouvelle page enfant qui représente la version de la langue du site :

   1. Cliquez sur Nouveau > Nouvelle page
   1. Dans la boîte de dialogue, spécifiez le titre et le nom. Le nom doit être au format `<language-code>` ou `<language-code>_<country-code>`, par exemple, en, en_US, en_us, en_GB, en_gb.

      * Le code de langue pris en charge est le code à deux lettres en minuscules, tel que défini par la norme ISO-639-1.
      * Le code de pays pris en charge est le code à deux lettres, en minuscules ou en majuscules, comme défini par la norme ISO 3166.

   1. Sélectionnez un modèle, puis cliquez sur Créer.

   ![newpagefr](assets/newpagefr.png)

1. Dans la console Sites web, dans l’arborescence des sites web, sélectionnez la page racine du site.
1. Dans le menu Outils, sélectionnez Copie linguistique.

   ![toolslanguagecopy](assets/toolslanguagecopy.png)

   La boîte de dialogue Copie linguistique affiche un tableau des versions linguistiques et des pages web disponibles. Un x dans une colonne de langue signifie que la page est disponible dans cette langue.

   ![languagecopydialog](assets/languagecopydialog.png)

1. Pour copier une page existante ou une arborescence de pages d’une version de langue, sélectionnez la cellule de la page en question dans la colonne de langue. Cliquez sur la flèche et sélectionnez le type de copie à créer.

   Dans l&#39;exemple suivant, la page equipment/sunglasses/irian est copiée dans la version en français.

   ![languagecopydilogdropdown](assets/languagecopydilogdropdown.png)

   | Type de copie linguistique | Description |
   |---|---|
   | auto | Utilise le comportement des pages parentes. |
   | ignore | Ne crée pas de copie de cette page et de ses enfants. |
   | `<language>+` (par exemple, Français+) | Copie la page et tous ses enfants de cette langue. |
   | `<language>` (par exemple, français) | Copie uniquement la page à partir de cette langue. |

1. Cliquez sur OK pour fermer la boîte de dialogue.
1. Dans la boîte de dialogue suivante, cliquez sur Oui pour confirmer la copie.
