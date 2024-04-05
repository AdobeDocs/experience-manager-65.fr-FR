---
title: Créer une lettre
description: Cette rubrique détaille comment créer une lettre, y ajouter des modules de données et des pièces jointes, puis la prévisualiser dans Correspondence Management.
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: 2f996a50-7c7d-41b6-84b2-523b6609254b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3982'
ht-degree: 100%

---

# Créer une lettre {#create-letter}

## Workflow de Correspondence Management {#correspondence-management-workflow}

Le workflow de Correspondance Management se divise en quatre phases :

1. Création d’un modèle
1. Création de fragments de document
1. Création de lettre
1. Post-traitement

### Création d’un modèle {#template-creation}

Le graphique suivant illustre un workflow type pour la création d’un modèle de correspondance.

![Procédure de création d’un modèle de correspondance](assets/01.png)

Dans ce workflow : 

1. Les concepteurs de formulaire créent des mises en page et des mises en page de fragments à l’aide d’Adobe Forms Designer et les téléchargent vers un référentiel CRX. Les mises en page contiennent des champs de formulaire classiques, des fonctions de mise en page (en-têtes et pieds de page, par exemple) et des « zones cibles » vides où placer du contenu. Les spécialistes d’applications interviennent ensuite pour mapper le contenu requis vers ces zones cible. En savoir plus sur [la conception de la disposition](/help/forms/using/layout-design-details.md).
1. Des spécialistes des services juridique, financier ou marketing créent et téléchargent du contenu tel que des clauses de protection légale ou des conditions générales, ainsi que des images, comme des logos, réutilisés dans divers modèles de correspondance.
1. Les spécialistes d’applications créent des modèles de correspondance. Le spécialiste d’application

   * Mappe des clauses et des images vers les zones cibles des modèles de disposition ;
   * Définit les conditions et règles de l’inclusion de contenu ;
   * Relie les champs et variables de la mise en page aux modèles de données sous-jacents.

1. Auteur : prévisualise la lettre et l’envoie en post-traitement. En savoir plus sur le [post-traitement](/help/forms/using/submit-letter-topostprocess.md).

#### Utilisation de modèles de lettre fournis avec Correspondence Management {#using-letter-templates-provided-with-correspondence-management}

Au lieu de créer un modèle de disposition entièrement nouveau, vous pouvez choisir de modifier et réutiliser des modèles fournis par Correspondence Management. Vous pouvez utiliser Designer pour modifier rapidement l’identité graphique et les données et les champs de contenu des modèles en fonction des besoins de votre entreprise. Pour plus d’informations sur les modèles Correspondence Management, voir [Modèles de lettre de référence](/help/forms/using/reference-cm-layout-templates.md).

### Création de fragments de document {#document-fragment-creation}

Les fragments de document sont les parties\composants réutilisables d’une correspondance avec laquelle vous pouvez composer des lettres\une correspondance.

Les fragments de document sont composés des types suivants :

#### Texte {#text}

Une ressource texte est un élément de contenu comprenant un ou plusieurs paragraphes de texte. Un paragraphe peut être statique ou dynamique. Un paragraphe dynamique contient des références à des éléments de données dont les valeurs sont fournies au moment de l’exécution.

#### Liste {#list}

Une liste est une série de fragments de document comprenant du texte, des listes (une même liste ne peut pas être ajoutée à elle-même), des conditions et des images. L’ordre des éléments de la liste peut être fixe ou modifiable. Lors de la création d’une lettre, vous pouvez utiliser certains ou tous les éléments de liste pour répliquer un modèle d’éléments réutilisable.

#### Condition {#condition}

Les conditions vous permettent de définir le contenu à inclure lors de la création d’une correspondance, en fonction des données fournies. La condition est décrite en termes de variables de contrôle. Les variables peuvent être soit un élément du dictionnaire de données, soit un espace réservé. Lorsque vous ajoutez une condition, vous pouvez choisir d’inclure un actif en fonction de la valeur de la variable de contrôle. Les conditions produisent une seule sortie, basée sur une expression. La première expression utilisée est vraie selon la variable de condition actuellement utilisée. Sa valeur devient la sortie produite par la condition.

#### Fragment de mise en page {#layout-fragment}

Un fragment de disposition est une disposition pouvant être utilisée dans une ou plusieurs lettres. Un fragment de disposition est utilisé pour créer des modèles répétables, en particulier des tableaux dynamiques. La disposition peut comporter des champs de formulaire types comme « Adresse » et « Numéro de référence ». Elle contient également des sous-formulaires vides indiquant les zones cible. Les dispositions (XDP) sont créées dans Designer, puis sont [téléchargées sur Forms et Documents](/help/forms/using/get-xdp-pdf-documents-aem.md).

### Création de lettre {#letter-creation}

Il existe deux manières de générer la correspondance à envoyer à votre clientèle : création par l’utilisateur ou l’utilisatrice et création par le système.

#### Création par l’utilisateur ou l’utilisatrice {#user-driven}

Les employés en contact avec la clientèle comme les experts en assurances ou les chargés d’assistance peuvent créer de la correspondance personnalisée. Dans une interface simple et intuitive présentant une mise en page simple de courrier, les utilisateurs peuvent ajouter du texte facultatif, personnaliser le contenu modifiable tout en prévisualisant la correspondance en temps réel. Ils peuvent ensuite envoyer la correspondance personnalisée à un processus d’arrière-plan.

![Correspondance créée par l’utilisateur et personnalisée](assets/02.png)

#### Création par le système {#system-driven}

La génération des correspondances est automatisée, basée sur des déclencheurs d’événement. Par exemple, un rappel envoyé à un contribuable l’invitant à remplir sa feuille d’impôts sera généré par la fusion du modèle prédéfini avec les données du citoyen. La lettre finale peut être envoyée par courrier électronique, imprimée, télécopiée ou archivée.

![Correspondence créée par le système](assets/us_cm_generate.png)

### Post-traitement {#post-processing}

La correspondance finalisée pourra être envoyée à un processus d’arrière-plan à des fins de post-traitement. La correspondance peut être :

1. traitée pour être envoyée par e-mail ou par fax, ou pour être imprimée par lots, ou encore pour être placée dans un dossier à des fins d’impression ou d’envoi par e-mail ;
1. soumise à révision et approbation ;
1. sécurisée par l’application de signatures numériques, de certification, de chiffrement ou de gestion des droits numériques ;
1. convertie en PDF où il est possible d’effectuer une recherche et qui contient toutes les métadonnées nécessaires à l’archivage et l’audit ;
1. Incluse dans un portfolio PDF qui comprend d’autres documents tels que des supports marketing. Le portfolio PDF peut ensuite être envoyé comme correspondance finale.

### Architecture de la solution Correspondence Management {#correspondence-management-solution-architecture}

Le graphique suivant présente un aperçu d’un exemple d’architecture de la solution de lettres.

![Architecture de la solution de lettre](assets/us_cm_architecture_es3.png)

## Découpage d’une lettre {#deconstructing-a-letter}

Ce document d’avis d’annulation est un exemple type de correspondance :

![Un modèle de lettre d’annulation](assets/5_deconstructingaletter.png)

<table> 
 <tbody> 
  <tr> 
   <td><strong>Eléments de lettre</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Formée avec</strong></td> 
  </tr> 
  <tr> 
   <td>Des données des systèmes back-end de l’entreprise</td> 
   <td>Des données provenant de systèmes d’arrière-plan de l’entreprise. Les données sont fusionnées dynamiquement avec le modèle de correspondance.</td> 
   <td><br /> Fichier de données créé à partir d’un dictionnaire de données</td> 
  </tr> 
  <tr> 
   <td>Données<br /> entrées par un collaborateur ou une collaboratrice du front office</td> 
   <td>Données pouvant être fournies par un collaborateur ou une collaboratrice du front office, qui personnalise la lettre avant de l’envoyer.<br /> </td> 
   <td><p>Eléments DD non protégés<br />Paragraphes modifiables<br /> Variables/espaces réservés<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Paragraphes de texte<br /> prévalidés.</td> 
   <td>Contenu du texte prévalidé. Le contenu du texte est en général rédigé par des experts dans les domaines financier, légal ou commercial qui comprennent le contexte commercial de la lettre. Le contenu comme l’en-tête, le pied de page, les clauses de non-responsabilité et les formules de politesse sont communes à la plupart des lettres. Toutefois, certains contenus, tels que la « cause de cessation », sont spécifiques à la lettre particulière.</td> 
   <td><p>Textes\Listes<br /> Conditions\Disposition</p> <p> </p> </td> 
  </tr> 
  <tr> 
   <td>Données<br /> basées sur une logique personnalisée ?</td> 
   <td>Dans le cas de certains courriers, comme une lettre demandant des précisions concernant une réclamation, certains utilisateurs de l’entreprise, comme l’expert en sinistres, peuvent ajouter du texte personnalisé.</td> 
   <td>Fragment de <br /> document de type Condition </td> 
  </tr> 
  <tr> 
   <td>Images stockées<br /> du référentiel central</td> 
   <td>Images (logos et signatures). Les images comme les logos de l’entreprise sont présentes dans la majorité des correspondances. Les images de signatures sont quant à elles spécifiques à la lettre et à la personne au nom de laquelle est envoyé le courrier.</td> 
   <td><p>Images stockées dans les ressources AEM (DAM)<br /> </p> <p> </p> </td> 
  </tr> 
 </tbody> 
</table>

## Analyse d&#39;une lettre avant sa construction {#analyze-a-letter-before-you-construct-it}

Analysez chaque lettre pour déceler ses différentes composantes. C’est au spécialiste de l’application qu’il revient d’analyser les correspondances qui sont générées.

* Les parties de la correspondance qui sont statiques et celles qui sont dynamiques ; les variables qui sont remplies à partir des sources de données d’arrière-plan ou par les utilisateurs et les utilisatrices finales ;
* l’ordre dans lequel apparaissent les différents paragraphes de texte dans la correspondance, par exemple si les paragraphes peuvent être modifiés par un utilisateur ou une utilisatrice de l’entreprise lors de la création de la correspondance ;
* si la correspondance est générée par le système ou s’il faut qu’un utilisateur final la modifie ; le nombre de correspondances générées par le système et le nombre de celles nécessitant l’intervention d’un utilisateur ou d’une utilisatrice ;
* la fréquence de changement de la correspondance modèle. Sera-t-elle mise à jour tous les ans, tous les trimestres, ou uniquement en cas de modification de la législation ? Quel type de changements est-il attendu ? Les changements consistent-ils à corriger des erreurs typographiques, à modifier une disposition, à ajouter des champs supplémentaires ou d’autres paragraphes, etc. ?
* Lorsque vous planifiez les besoins de votre correspondance, constituez la liste des nouveaux modèles de correspondance. Pour chaque modèle de correspondance, vous avez besoin des éléments suivants :

   * des clauses de texte, des images et des tableaux ;
   * des valeurs de données provenant des systèmes back-end ;
   * la disposition et les fragments de la disposition de la correspondance ;
   * l’ordre dans lequel le contenu apparaît dans la lettre et les règles d’inclusion et d’exclusion de contenu ;

* les conditions dans lesquelles des utilisateurs et utilisatrices professionnelles, comme les experts et expertes en sinistres ou les chargés et chargées d’assistance, sont amenés à modifier tout ou partie du contenu de la lettre.
* Les scénarios décrivent l’expérience des utilisateurs et utilisatrices, les conditions requises et les avantages de l’utilisation de la solution Lettres.
* Ils fournissent également : les compétences et les outils requis pour le projet ;
* les recommandations relatives à la planification de l’implémentation ; ``un bon aperçu général de l’implémentation.

## Avantages de l’analyse {#benefits-of-performing-the-analysis}

**Réutiliser du contenu** : vous disposez d’une liste consolidée de nouveau contenu dont vous avez besoin pour générer de la correspondance. Une grande partie des contenus (en-têtes, pieds de page, clauses de protection légale et introductions) est commune à de nombreux courriers et peut être réutilisée entre différents courriers. Il suffit alors que ces contenus communs soient créés et approuvés une seule fois par des experts et expertes pour pouvoir être réutilisés par la suite dans un grand nombre de courriers.

**Créer le dictionnaire de données** : certaines valeurs de données telles que « Identifiant client » et « Nom du client » sont communes à de nombreuses lettres. Vous pouvez établir une liste consolidée de toutes ces valeurs de données. En règle générale, on consulte une personne de l’équipe middleware de l’entreprise lors de la planification de la structure. Ces valeurs de données constituent la base à partir de laquelle est créé le dictionnaire de données.

**Obtenir des données des systèmes d’arrière-plan de l’entreprise** : vous connaîtrez également toutes les valeurs de données nécessaires et saurez où obtenir les données du système d’entreprise. Vous pouvez ensuite architecturer l’implémentation permettant d’extraire les données du système d’entreprise pour alimenter la solution Lettres.

**Estimer la complexité des lettres** : il est important de définir la complexité que représente la création d’une correspondance particulière. Cette analyse permet de déterminer le temps et les ensembles de compétences nécessaires pour créer les modèles de lettre. Cela vous permettra ensuite d’estimer les ressources et les coûts nécessaires à l’implémentation de la solution Lettres.

## Complexité de la correspondance {#correspondence-complexity}

La complexité de la correspondance peut être déterminée grâce à l’analyse des paramètres suivants :

**Complexité de la disposition** : quel est le niveau de complexité de la disposition ? La disposition de lettres comme l’avis d’annulation est simple. tandis que des courriers comme les demandes de confirmation de couverture ont une disposition complexe avec plusieurs tableaux et plus de soixante champs de formulaire. La création de dispositions complexes requiert plus de temps et nécessite des compétences avancées de maquettiste.

**Nombre de paragraphes et de conditions** : un contrat de prêt peut contenir dix pages et plus de quarante clauses de texte. Beaucoup de ces clauses dépendront des paramètres de prêt. Selon les termes et conditions exacts, les clauses seront incluses dans le contrat ou au contraire en seront exclues. La création de ce type de courrier nécessite une planification rigoureuse et une définition méticuleuse des conditions complexes.

Le tableau qui suit expose quelques règles utiles pour la classification de vos lettres :

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Niveau de complexité</strong></p> </td> 
   <td><p><strong>Complexité de la mise en page (subjective)</strong></p> </td> 
   <td><p><strong>Nombre de paragraphes de texte</strong></p> </td> 
   <td><p><strong>Nombre de textes conditionnels ou d’images</strong></p> </td> 
   <td><p><strong>Compétences requises</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Faible complexité</p> </td> 
   <td><p>Faible. La disposition comporte peu de champs de formulaire (moins de quinze).</p> <p>Généralement une page<span class="acrolinxCursorMarker"></span>.</p> </td> 
   <td><p>8</p> </td> 
   <td><p>1</p> </td> 
   <td><p>Compétences Designer moyennes.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Complexité moyenne</p> </td> 
   <td><p>Mise en page à complexité moyenne. Comprend des structures comme des tableaux. Généralement plus d’une page.</p> </td> 
   <td><p>16</p> </td> 
   <td><p>2</p> </td> 
   <td><p>Compétences Designer moyennes.</p> <p> </p> <p>Possibilité de créer des expressions complexes à l’aide d’interfaces utilisateur.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Complexité élevée</p> </td> 
   <td><p>Disposition complexe. Peut dépasser les trois pages. Contient des tableaux et plus de soixante champs de formulaire.</p> </td> 
   <td><p>40</p> </td> 
   <td><p>8</p> </td> 
   <td><p>Compétences Designer de niveau expert.</p> <p> </p> <p>Possibilité de créer des expressions complexes à l’aide d’interfaces utilisateur.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Présentation de la création d’une lettre {#overview-of-creating-a-letter}

1. Sélectionnez la disposition appropriée qui sert de base à la lettre et créez une lettre.
1. Ajoutez à la lettre des modules de données ou des fragments de disposition et configurez-les.
1. Sélectionnez l’aperçu de la correspondance.
1. Modifiez et configurez les champs, les variables, le contenu et les pièces jointes.

### Prérequis {#prerequisites}

Vous devez d’abord avoir les éléments suivants correctement configurés pour créer une correspondance :

* [Package de compatibilité](compatibility-package.md). Installez le package de compatibilité pour afficher l’option **Lettres** sur la page **Formulaires**.
* La lettre XDP ([mise en page](/help/forms/using/document-fragments.md)).
* Autres XDP ([fragment de mise en page](document-fragments.md#document-fragments)) qui constituent des parties de la lettre. Les XDP\mises en page sont créés dans [Designer](https://www.adobe.com/go/learn_aemforms_designer_65_fr).
* Le [dictionnaire de données](/help/forms/using/data-dictionary.md) approprié (facultatif).
* Les [modules de données](/help/forms/using/document-fragments.md) à utiliser dans la correspondance.
* [Les données de test](/help/forms/using/data-dictionary.md#p-working-with-test-data-p) correspondent au fichier XML contenant les données de test. Des données de test sont requises si vous utilisez un dictionnaire de données.

## Création d&#39;un modèle de lettre {#create-a-letter-template}

### Choisissez une disposition et entrez les propriétés de lettre. {#select-a-layout-and-enter-the-letter-properties}

1. Sélectionnez **Formulaires** > **Lettres**.

1. Sélectionnez **Créer > Lettre**. Correspondence Management affiche les dispositions disponibles (en XDP). Ces mises en page proviennent de Designer. Les dispositions incluent également les modèles de lettre prêts à l’emploi de Correspondence Management. Pour plus d’informations sur les modèles Correspondence Management, voir [Modèles de lettre de référence](/help/forms/using/reference-cm-layout-templates.md). Pour ajouter vos propres dispositions, créez des fichiers XDP (disposition) dans Designer, puis [téléchargez-les dans AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md).

   ![create-letter](assets/create-letter.png)

1. Choisissez une disposition en cliquant dessus, puis sélectionnez **Suivant**.

   ![Sélection de la mise en page pour créer une lettre](assets/selectlayout.png)

1. Saisissez les propriétés de la correspondance, puis sélectionnez **Enregistrer :**

   * **Titre (facultatif) :** saisissez le titre de la lettre. Le titre ne doit pas nécessairement être unique et peut contenir des caractères spéciaux et des caractères dans une langue autre que l’anglais.
   * **Nom :** nom unique de la lettre. Deux lettres ne peuvent en aucun cas porter le même nom. Dans le champ Nom, vous pouvez saisir uniquement des caractères, des chiffres et des tirets de langue anglaise. Le champ Nom est automatiquement renseigné en fonction du champ Titre. Les caractères spéciaux, les espaces, les chiffres et les caractères non anglais saisis dans le champ Titre sont remplacés par des tirets dans le champ Nom. Bien que la valeur du champ Titre soit automatiquement copiée dans Nom, vous pouvez la modifier.
   * **Description (facultatif) :** Décrivez la lettre à titre de référence.
   * **Dictionnaire de données (facultatif)** : le dictionnaire de données peut être associé à la correspondance. Les actifs que vous insérerez ultérieurement dans cette correspondance doivent avoir le même dictionnaire de données que celui choisi pour cette même correspondance ou ne pas avoir de dictionnaire de données.
   * **Balises (facultatif) :** sélectionnez les balises à appliquer à la correspondance. Vous pouvez également saisir un nom de balise nouveau ou personnalisé et appuyer sur Entrée pour créer la balise.
   * **Post-traitement (facultatif) :** sélectionnez le post-traitement à appliquer au modèle de lettre. Il existe des post-processus prêts à l’emploi ainsi que ceux que vous avez créés grâce à AEM, comme l’envoi par courrier électronique et l’impression.

   ![Propriétés de correspondance](assets/createcorrespondenceproperties.png)

1. Le système affiche le message suivant : « Lettre créée avec succès » (dans le message d’alerte) Sélectionnez **Ouvrir** afin de configurer les modules de données et les fragments de disposition à l’intérieur. Vous pouvez également cliquer sur **Terminé** pour revenir à la page précédente.

   ![Message d’avertissement : lettre créée avec succès](assets/createcorrespondencecreated.png)

   **Suivant** : lorsque vous sélectionnez **Ouvrir**, Correspondence Management affiche une représentation de la disposition répertoriant tous les composants présents dans la disposition (XDP). Poursuivez en insérant les [Modules de données et fragments de disposition et configuration](/help/forms/using/create-letter.md#p-insert-data-modules-and-layout-fragments-in-a-letter-and-configure-them-p).

### Insérez des modules de données et des fragments de disposition dans une lettre puis configurez-les. {#insert-data-modules-and-layout-fragments-in-a-letter-and-configure-them}

Une fois la correspondance créée, sélectionnez Ouvrir pour afficher dans Correspondence Management une représentation de la disposition répertoriant tous les sous-formulaires/zones cible de la disposition (XDP). Dans chaque zone cible, vous pouvez choisir d’insérer un module de données ou un fragment de disposition (puis des modules de données dans le fragment de disposition).

>[!NOTE]
>
>Vous pouvez également sélectionner l’icône Modifier d’une lettre dans la page Lettres pour insérer des modules de données et des fragments de disposition dans une lettre avant de les configurer.

1. Sélectionnez **Insérer** pour chacun des sous-formulaires et sélectionnez des modules de données ou un fragment de disposition à insérer dans chaque sous-formulaire.

   ![Insertion de modules de données et de fragments de mise en page](assets/insertdmandlf.png)

1. Sélectionnez le module de données ou le fragment de disposition de ces options pour chacun des sous-formulaires puis sélectionnez les modules de données ou les fragments de disposition à insérer. Un fragment de disposition vous permet d’insérer d’autres modules de données ou fragments de disposition dans le formulaire selon sa conception (jusqu’à quatre niveaux).

   ![nestedlf](assets/nestedlf.png)

1. Si vous insérez un fragment de disposition, le nom du fragment de disposition s’affiche dans le sous-formulaire. Et selon le fragment sélectionné, les sous-formulaires imbriqués s’affichent dans le sous-formulaire.
1. Après avoir inséré les modules de données sélectionnés dans la disposition, vous pouvez sélectionner Configurer le mode et définir les éléments suivants pour chaque module après avoir appuyé sur l’icône Modifier :

   1. **Modifiable** : lorsque cette option est sélectionnée, le contenu peut être modifié dans l’interface utilisateur de création de correspondance. Marquez le contenu comme modifiable uniquement s’il doit obligatoirement être modifié par un utilisateur ou une utilisatrice de l’entreprise (un expert ou une experte en assurance, par exemple).
   1. **Obligatoire** : lorsque cette option est sélectionnée, le contenu est obligatoire dans l’interface utilisateur de création de correspondance.
   1. **Sélectionné** : lorsque cette option est sélectionnée, le contenu est sélectionné par défaut dans l’interface utilisateur de création de correspondance.
   1. **Mise en retrait** : permet d&#39;augmenter ou diminuer la mise en retrait du module et du contenu de la lettre. La mise en retrait est spécifiée par niveaux, en commençant par 0. Chaque niveau correspond à un retrait de 36 points. Pour en savoir plus sur la personnalisation des formulaires, voir **[!UICONTROL Configurations de Correspondence Management]** dans [Workflow des formulaires](submit-letter-topostprocess.md#formsworkflow).
   1. **Saut de page avant** : si vous activez le Saut de page avant, le contenu de CE module s’affichera toujours sur une nouvelle page.
   1. **Saut de page après** : si vous activez le Saut de page après pour un module spécifique, le contenu du module SUIVANT s’affichera toujours sur une nouvelle page.

   ![Modules de données et fragments de mise en page insérés](assets/insertdmandlf2.png)

1. Pour modifier un module, sélectionnez l’icône Modifier située en regard de celui-ci. Après modification des modules, sélectionnez **Enregistrer**.

   Dans cette page, vous pouvez également procéder comme suit pour les sous-formulaires :

   1. **Activation du texte libre** : quand le texte libre est activé, un utilisateur peut ajouter du texte en ligne dans la lettre grâce à la vue CCR. Dans la vue CCR, une action « T » est activée pour ces zones cible. Le texte libre est activé dans cette action et lorsque l’utilisateur ou l’utilisatrice appuie dessus, le nom et la description du texte lui seront demandés. En appuyant sur OK, ce texte s’ouvre en mode de modification où l’utilisateur ou l’utilisatrice peut ajouter du texte. Il s’agit donc du même fonctionnement que pour d’autres modules de texte.
   1. **Verrouillage de l’ordre** : verrouille l’ordre des sous-formulaires dans la lettre. L’auteur ou l’autrice n’est pas autorisée à réorganiser les sous-formulaires et composants lors de la création de la lettre.

   Dans cette page, vous pouvez également procéder comme suit pour chaque actif des sous-formulaires :

   1. **Modifier l’ordre des ressources** : faites glisser et déposez une ressource contenant l’icône de réorganisation d’une ressource (![glisser-déposer](assets/dragndrop.png)).
   1. **Supprimer des ressources** : sélectionnez l’icône de suppression en regard d’une ressource pour la supprimer.
   1. **Prévisualiser des ressources** : sélectionnez l’icône d’aperçu (![showpreview](assets/showpreview.png)) en regard d’une ressource.

1. Sélectionnez **Suivant**.
1. La page de données détaille la façon dont les champs de données et les variables sont utilisés dans le modèle. Les données peuvent être associées à des sources de données comme un dictionnaire de données ou des entrées utilisateur. Chaque champ définit des propriétés que le dictionnaire de données associe aux données ou aux légendes affichées pour les champs d’entrée utilisateur.

   Liaison :

   * Les éléments de **champ** peuvent être associés à un élément littéral ou de dictionnaire de données, à un actif ou encore à une valeur spécifiée par l’utilisateur. Vous pouvez également ignorer un élément de champ en l’associant à l’option Ignorer.
   * Les éléments de **variable** peuvent être associés à un élément littéral ou de dictionnaire de données, un champ, une variable, un actif ou encore à une valeur spécifiée par l’utilisateur ou l’utilisatrice.

   Voici quelques champs de liaison importants :

   * **Multiligne** : vous pouvez spécifier si l’entrée de données d’un champ ou d’une variable est multiligne. Si vous sélectionnez cette option, la zone de saisie du champ ou de la variable s’affiche en tant que zone d’entrée multiligne dans la vue Edition de données. Le champ ou la variable est également multiligne dans les vues Données et Contenu de l’interface utilisateur de création de correspondance. Le champ d’entrée multiligne est identique au champ de saisie de commentaire dans un TextModule. L’option multiligne est disponible uniquement pour les champs et variables avec un type de liaison Utilisateur ou Eléments du dictionnaire de données non protégés.
   * **Facultatif** : vous pouvez préciser si la valeur du champ ou de la variable est facultative ou obligatoire. L’option de champ facultative est disponible pour les champs et variables avec un type de liaison Utilisateur ou Éléments du dictionnaire de données non protégés.

   * **Validation de champ/variable** : pour une validation améliorée de la valeur d’un champ ou d’une variable, vous pouvez affecter une validation au champ ou à la variable. Cette option est disponible uniquement pour les champs et variables avec un type de liaison Utilisateur ou Éléments du dictionnaire de données non protégés.
   * **Légende** et **Info-bulle** : la légende est le libellé du champ qui s’affiche avant le champ dans l’interface utilisateur CCR. Cette option est disponible pour les champs et variables avec un type de liaison Utilisateur ou Éléments du dictionnaire de données non protégés.

   Voici les types de validation que vous pouvez utiliser pour les champs :

   * **Validation des chaînes** : utilisez la validation des chaînes pour spécifier la longueur minimale et maximale de la chaîne saisie dans le champ ou la variable. Lorsque vous créez une validation des chaînes, veillez à spécifier des paramètres de validation valides. Saisissez une longueur valide pour les valeurs minimales et maximales. Dans la validation des chaînes, vous pouvez spécifier la longueur minimale et maximale de la valeur qui peut être saisie. Si la valeur saisie ne correspond pas à la longueur minimale et maximale spécifiées, le champ correspondant de l’interface utilisateur CCR apparaît en rouge.

   * **Validation des nombres** : utilisez la validation des nombres pour spécifier les valeurs numériques minimales et maximales saisies dans un champ ou une variable. Lorsque vous créez une validation des nombres, veillez à spécifier des paramètres de validation valides. Entrez des valeurs numériques pour les valeurs minimales et maximales.

   * **Validation des expressions régulières** : utilisez la validation des expressions régulières pour définir une expression régulière permettant de valider la valeur d’un champ ou d’une variable. Vous pouvez également personnaliser le message d’erreur. Lorsque vous créez une validation des expressions régulières, veillez à spécifier une expression régulière valide.

   >[!NOTE]
   >
   >La validation des champs et des variables est disponible uniquement pour les champs ou variables avec un type de liaison Utilisateur ou Utilisatrice ou Eléments du dictionnaire de données non protégés.

   ![linkages](assets/linkages.png)

1. Après avoir spécifié la liaison, sélectionnez **Suivant**. Correspondence Management affiche l’écran de pièces jointes.

### Configurez les pièces jointes {#set-up-the-attachments}

1. Sélectionnez **Ajouter un actif**.
1. Dans l’écran de sélection des ressources, sélectionnez les ressources à joindre à la lettre et choisissez **Terminé**. Les actifs doivent d’abord être chargés dans Actifs. Il est conseillé de joindre uniquement des documents PDF et Microsoft Office, mais vous pouvez également joindre des images. Pour en savoir plus sur le téléchargement des ressources dans la gestion des ressources numériques, consultez la section [Télécharger des ressources](/help/assets/manage-assets.md).
1. Pour verrouiller l’ordre des ressources dans la liste et empêcher l’expert ou l’experte en sinistre de le modifier, sélectionnez **Verrouiller l’ordre**. Si vous ne sélectionnez pas cette option, l’utilisateur pourra modifier l’ordre des éléments de la liste.
1. Pour modifier l’ordre des ressources, faites glisser et déposez une ressource contenant l’icône de réorganisation d’une ressource (![dragndrop](assets/dragndrop.png)).
1. Sélectionnez **Modifier** en regard d’une pièce jointe et indiquez que celle-ci est obligatoire si vous souhaitez que l’auteur ou autrice ne puisse pas la supprimer. Indiquez qu’une pièce jointe est sélectionnée si vous souhaitez qu’elle soit présélectionnée dans l’interface CCR.
1. Sélectionnez **Accès à la bibliothèque** pour donner accès à la bibliothèque. Si Accès à la bibliothèque est activé, l&#39;expert ou l’experte en sinistre peut accéder à la bibliothèque de contenu lors de la création d&#39;une lettre et insérer des pièces jointes.
1. Sélectionnez **Configuration de pièces jointes** et spécifiez le nombre maximal de pièces jointes.

1. Sélectionnez **Enregistrer**. Votre correspondance est créée et répertoriée dans la page Lettres.

Après la création d’un modèle de lettre dans Correspondence Management, l’utilisateur final/agent/expert en sinistre peut ouvrir la lettre dans l’interface utilisateur CCR et créer une correspondance en saisissant des données, en configurant le contenu et en gérant les pièces jointes. Pour en savoir plus, consultez la section [Créer une correspondance](/help/forms/using/create-correspondence.md).

## Types de liaison disponibles pour chaque champ {#types-of-linkage-available-for-each-of-the-fields}

Le tableau suivant décrit les types de liaisons disponibles pour les différents types de champs.

Les valeurs suivantes du tableau

* **Oui** : le type de champ de la colonne située le plus à gauche prend en charge ce type de mappage
* **Non** : le type de champ de la colonne située le plus à gauche ne prend pas en charge ce type de mappage.
* **N/A** : le type de champ de la colonne située le plus à gauche n’est pas applicable.

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td><strong>Littéral</strong></td> 
   <td><strong>Asset</strong></td> 
   <td><strong>Dictionnaire de données</strong></td> 
   <td><strong>Ignorer</strong></td> 
   <td><strong>User</strong></td> 
   <td><strong>Champ</strong></td> 
   <td><strong>Variable</strong></td> 
  </tr> 
  <tr> 
   <td><strong>date</strong></td> 
   <td>Oui</td> 
   <td>Non</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>l’heure.</strong></td> 
   <td>Oui</td> 
   <td>Non</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>datetime</strong></td> 
   <td>Oui</td> 
   <td>Non</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>integer</strong></td> 
   <td>Oui</td> 
   <td>Non</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>Oui<br /> </td> 
   <td>S/O</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>float</strong></td> 
   <td>Oui</td> 
   <td>Non</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>Oui<br /> </td> 
   <td>N/A</td> 
   <td>N/A<br /> </td> 
  </tr> 
  <tr> 
   <td><strong>richtext</strong></td> 
   <td>Oui</td> 
   <td>texte uniquement</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>plain</strong> <strong>text</strong></td> 
   <td>Oui</td> 
   <td>texte uniquement</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>Oui</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>image</strong></td> 
   <td>Non</td> 
   <td>image seule</td> 
   <td>Non</td> 
   <td>Oui</td> 
   <td>Non</td> 
   <td>N/A</td> 
   <td>N/A</td> 
  </tr> 
  <tr> 
   <td><strong>signature</strong></td> 
   <td>Non</td> 
   <td>Non</td> 
   <td>Non<br /> </td> 
   <td>Oui</td> 
   <td>Non</td> 
   <td>N/A</td> 
   <td>N/A<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Création d’une copie d’un modèle de lettre {#createcopylettertemplate}

Vous pouvez utiliser un modèle de lettre existant pour créer rapidement un modèle de lettre avec des propriétés, du contenu et des ressources héritées similaires, tels que des fragments de document et un dictionnaire de données. Pour ce faire, copiez et collez une lettre.

1. Dans la page Lettres, sélectionnez une ou plusieurs lettres. L’interface utilisateur affiche l’icône Copier.
1. Sélectionnez Copier. L’interface utilisateur affiche l’icône Coller. Vous pouvez également choisir d’accéder à un dossier avant de le coller. Différents dossiers peuvent contenir des ressources portant le même nom. Pour plus d’informations sur les dossiers, voir [Dossiers et organisation des actifs](/help/forms/using/import-export-forms-templates.md#folders-and-organizing-assets).
1. Sélectionnez Coller. La boîte de dialogue Coller s’affiche. Si vous copiez et collez les lettres au même emplacement, le système attribue automatiquement des noms et des titres aux nouvelles copies de lettres, mais vous pouvez les modifier.
1. Si nécessaire, modifiez le titre et le nom sous lesquels vous souhaitez enregistrer la copie de la lettre.
1. Sélectionnez Coller. La copie de la lettre est créée. À présent, vous pouvez effectuer les modifications nécessaires dans votre lettre nouvellement créée.
