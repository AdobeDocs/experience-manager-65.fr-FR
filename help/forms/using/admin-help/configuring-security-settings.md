---
title: Configuration des paramètres de sécurité
description: Découvrez comment configurer les paramètres de sécurité. Vous pouvez protéger les documents PDF en limitant l’accès. Vous pouvez chiffrer, certifier ou protéger le document par mot de passe.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator,Document Security
exl-id: be076477-2681-4570-953d-6c44d3c30843
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '1418'
ht-degree: 100%

---

# Configuration des paramètres de sécurité{#configuring-security-settings}

Vous pouvez limiter l’accès aux documents PDF en définissant des mots de passe et en limitant certaines fonctionnalités, telles que l’impression et la modification. Lorsqu’un document PDF comporte des fonctionnalités restreintes, les outils et les éléments de menu associés à ces fonctionnalités sont grisés. Vous pouvez utiliser d’autres méthodes pour créer des documents sécurisés, tels que le chiffrement ou la certification. Un paramètre de sécurité contient le mot de passe et des options spécifiques à utiliser pour certaines conversions de PDF.

Dans la page Paramètres de sécurité, vous pouvez effectuer les tâches suivantes :

## Créer ou modifier un paramètre de sécurité {#create-or-edit-a-security-setting}

Un *paramètre de sécurité* contrôle la sécurité et les autorisations des fichiers convertis avec ce paramètre de sécurité.

1. Dans Administration Console, cliquez sur Services > PDF Generator > Paramètres de sécurité.
1. Cliquez sur Nouveau ou sur le nom d’un paramètre de sécurité.
1. Dans la page Nouveau/Modifier le paramètre de sécurité, renseignez les informations requises pour le paramètre de sécurité. (Voir [Configuration des paramètres de type de fichier](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Cliquez sur Enregistrer et, dans la boîte de dialogue qui s’affiche, saisissez un nom pour le paramètre, puis cliquez sur OK.

### Paramètres de sécurité {#security-settings}

Ces paramètres configurent la compatibilité et le chiffrement. Pour plus de précisions sur l’accès aux paramètres relatif aux polices, voir [Création ou modification d’un paramètre de protection](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilité :** permet de définir le type de chiffrement relatif à l’ouverture d’un document protégé par un mot de passe. L’option Acrobat 3.0 et versions ultérieures utilise un niveau de chiffrement faible, alors que les autres options utilisent un niveau élevé de chiffrement :

**Acrobat 3.0 et versions ultérieures :** utilise un chiffrement faible (RC4 40 bits).

**Acrobat 5.0 et versions ultérieures :** utilise un chiffrement élevé (RC4 128 bits).

**Acrobat 6.0 et versions ultérieures :** utilise un chiffrement élevé (RC4 128 bits). Cette option permet d’activer des métadonnées pour la recherche.

**Acrobat 7.0 et versions ultérieures :** utilise un chiffrement élevé (AES 128 bits). Cette option permet d’activer des métadonnées pour la recherche et le chiffrement des pièces jointes uniquement.

**Acrobat 9.0 et versions ultérieures :** utilise un niveau de chiffrement élevé (AES 256 bits). Cette option permet d’activer des métadonnées pour la recherche et le chiffrement des pièces jointes uniquement.

Une version antérieure d’Acrobat ne peut pas ouvrir un document PDF ayant un paramètre de compatibilité plus élevé. Par exemple, si vous sélectionnez l’option Acrobat 7.0 et versions ultérieures, vous ne pouvez pas ouvrir le document dans Acrobat 6.0 ou version antérieure.

Assurez-vous que le niveau de compatibilité est cohérent avec celui du PDF pour la même source. Par exemple, si un dossier de contrôle est configuré de manière à utiliser l’option PDF standard (compatible avec Acrobat 5.0 ou une version ultérieure), le niveau de compatibilité de l’option ne doit pas être plus élevé que Acrobat 5.0.

**Restrictions du document :** les restrictions du document disponibles dépendent de l’option Compatibilité sélectionnée.

**Pas de chiffrement :** ne chiffre aucune partie du document.

**Chiffrer tout le contenu du document :** chiffre le document et ses métadonnées. Lorsque cette option est sélectionnée, les moteurs de recherche n’ont pas accès aux métadonnées du document.

**Chiffrer tout le contenu du document à l’exception des métadonnées (compatible avec Acrobat
6 et versions ultérieures) :** chiffre le contenu d’un document tout en permettant aux moteurs de recherche d’accéder aux métadonnées du document. Cette option n’est disponible que si Acrobat 6.0 ou versions ultérieures, Acrobat 7.0 ou versions ultérieures, ou Acrobat 9.0 ou versions ultérieures est affecté à l’option Compatibilité.

**Chiffrer uniquement les pièces jointes (compatible avec Acrobat 7
et versions ultérieures) :** les utilisateurs peuvent ouvrir le document sans mot de passe, mais ils doivent saisir un mot de passe pour ouvrir les pièces jointes. Cette option n’est disponible que si l’option Compatibilité est définie sur Acrobat 7.0 ou version ultérieure, ou Acrobat 9.0 ou version ultérieure.

Ces paramètres permettent de configurer la protection par mot de passe :

>[!NOTE]
>
>Si vous oubliez un mot de passe, il ne peut pas être récupéré à partir du document. Il est recommandé de stocker les mots de passe à un autre emplacement sécurisé en cas d’oubli. Conservez également une copie de sauvegarde du document non protégé par mot de passe.

**Exiger un mot de passe pour l’ouverture du document :** active les options de mot de passe.

**Mot de passe d’ouverture du document :** permet d’empêcher les utilisateurs d’ouvrir le document à moins d’avoir saisi le mot de passe que vous avez défini. Les mots de passe respectent la casse. Acrobat utilise la méthode de sécurité RC4 de RSA Security Inc. pour protéger les documents PDF par mot de passe. Si vous limitez l’impression et la modification, nous vous recommandons d’ajouter un mot de passe d’ouverture du document afin de renforcer la sécurité.

**Saisir à nouveau le mot de passe d’ouverture du document :** vérifie que le mot de passe d’ouverture du document est correct.

**Exiger un mot de passe pour l’ouverture des pièces jointes :** active les options de mot de passe. Cette option n’est disponible que si l’option Compatibilité sélectionnée est Acrobat 7.0 ou versions ultérieures ou Acrobat 9.0 ou versions ultérieures, et si l’option Restrictions du document sélectionnée est Chiffrer les pièces jointes.

**Mot de passe d’ouverture de la pièce jointe :** vérifie qu’un mot de passe est requis pour ouvrir une pièce jointe. Les utilisateurs et utilisatrices peuvent ouvrir le document sans mot de passe. Cette option n’est disponible que si l’option Compatibilité sélectionnée est Acrobat 7.0 ou versions ultérieures ou Acrobat 9.0 ou versions ultérieures, et si l’option Restrictions du document sélectionnée est Chiffrer les pièces jointes.

**Saisir à nouveau le mot de passe d’ouverture des pièces jointes :** vérifie que le mot de passe est correct. Cette option n’est disponible que si l’option Compatibilité sélectionnée est Acrobat 7.0 ou versions ultérieures ou Acrobat 9.0 ou versions ultérieures, et si l’option Restrictions du document sélectionnée est Chiffrer les pièces jointes.

Ces options permettent de configurer les autorisations :

**Utiliser un mot de passe pour restreindre l’impression et la modification 
du document et de ses paramètres de protection :** permet de restreindre les autorisations.

**Mot de passe d’accès aux droits :** empêche les utilisateurs d’imprimer et de modifier. Les utilisateurs et utilisatrices ne peuvent pas modifier ces paramètres de sécurité à moins de saisir le mot de passe que vous avez spécifié. Vous ne pouvez pas utiliser le même mot de passe que celui utilisé pour l’ouverture du document. Lorsque vous définissez un mot de passe d’autorisation, seules les personnes qui saisissent ce mot de passe peuvent modifier les paramètres de sécurité. Si le document PDF a les deux types de mots de passe, il suffit de saisir l’un ou l’autre pour l’ouvrir. Toutefois, un utilisateur ou une utilisatrice a besoin du mot de passe d’accès aux droits pour définir ou modifier les fonctionnalités à accès restreint. Si le document PDF ne dispose que d’un mot de passe d’accès aux droits ou si une personne ouvre le document à l’aide du mot de passe d’ouverture du document, l’invite de saisie du mot de passe s’affiche dès que la personne tente de modifier les paramètres de protection.

**Saisir à nouveau le mot de passe d’accès aux droits :** vérifie que le mot de passe d’accès aux droits est correct.

**Impression autorisée :** permet de définir la qualité d’impression du document PDF :

**Aucune :** empêche les utilisateurs d’imprimer le document.

**Basse résolution (150 dpi) :** permet aux utilisateurs d’imprimer le document à une résolution maximale de 150 dpi. L’impression peut être plus lente, car chaque page est imprimée sous la forme d’une image bitmap. Cette option n’est disponible que si un niveau de chiffrement élevé (Acrobat 5.0, 6.0, 7.0 ou 9.0) est sélectionné.

**Haute résolution :** permet aux utilisateurs d’imprimer dans n’importe quelle résolution en dirigeant le document vers des imprimantes PostScript ou autres, qui prennent en charge des fonctions d’impression de haute qualité avancées.

**Modifications autorisées :** permet de définir les actions de modification autorisées dans le document PDF.

**Aucune :** empêche les utilisateurs de modifier le document, y compris de remplir des champs de formulaire et de signature.

**Insertion, suppression et rotation de pages :** permet aux utilisateurs et utilisatrices d’insérer, de supprimer et de faire pivoter des pages, ainsi que de créer des signets et des pages miniatures. Cette option n’est disponible que si un niveau de chiffrement élevé (Acrobat 5.0, 6.0, 7.0 ou 9.0) est sélectionné.

**Remplir des champs de formulaire et signer des 
champs de signature existants :** permet aux utilisateurs de remplir des formulaires et d’ajouter des signatures numériques. Toutefois, les utilisateurs et utilisatrices ne peuvent pas ajouter de commentaires ni créer de champs de formulaire. Cette option n’est disponible que si un niveau de chiffrement élevé (Acrobat 5.0, 6.0, 7.0 ou 9.0) est sélectionné.

**Commentaires, remplissage de champs de formulaire et signature de champs de signature existants :** permet aux utilisateurs de remplir des formulaires et d’ajouter des commentaires et des signatures numériques.

**Mise en page, retouche, remplissage de champs de formulaire et signature
de champs de signature existants :** permet aux utilisateurs d’insérer, de faire pivoter ou de supprimer des pages, ainsi que de créer des signets ou des images miniatures, de remplir des formulaires et d’ajouter des signatures numériques. Cette option ne permet pas aux utilisateurs et aux utilisatrices de créer des champs de formulaire. Cette option est uniquement disponible si un niveau de chiffrement faible (Acrobat 3.0) est sélectionné.

**Tout sauf extraire des pages :** permet aux utilisateurs de modifier le document à l’aide de la méthode répertoriée dans la liste Modifications autorisées, mais pas de supprimer des pages.

**Activer la copie de texte, d’images et d’autres contenus :** permet aux utilisateurs de sélectionner et de copier le contenu du document PDF. Elle permet également aux utilitaires ayant besoin du contenu d’un fichier PDF, comme un catalogue Acrobat, d’y avoir accès. Cette option est uniquement disponible si un niveau de chiffrement élevé est sélectionné.

**Activer l’accès au texte pour les lecteurs d’écran destinés aux
malvoyants :** permet aux utilisateurs ayant une déficience visuelle de lire le document à l’aide de lecteurs d’écran. Toutefois, les utilisateurs et utilisatrices ne peuvent pas copier ni extraire le contenu du document. Cette option est uniquement disponible si un niveau de chiffrement élevé est sélectionné.

## Suppression d’un paramètre de sécurité {#delete-a-security-setting}

Vous pouvez supprimer un paramètre de sécurité s’il n’est plus nécessaire. Toutefois, les paramètres de sécurité préconfigurés ne peuvent pas être supprimés.

1. Dans la console d’administration, cliquez sur **[!UICONTROL Services > PDF Generator > Paramètres de protection]**.
1. Cochez la case en regard du paramètre à supprimer. Vous pouvez sélectionner plusieurs paramètres.
1. Cliquez sur **[!UICONTROL Supprimer]**, puis, dans la page **[!UICONTROL Confirmation de suppression]**, cliquez à nouveau sur **[!UICONTROL Supprimer]**.
