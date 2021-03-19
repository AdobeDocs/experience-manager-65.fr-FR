---
title: Envoi sécurisé de gros volumes d’information
seo-title: Envoi sécurisé de gros volumes d’information
description: Dans des environnements de production de masse, Document Security prend en charge l’association des licences aux utilisateurs plutôt qu’aux documents.
seo-description: Dans des environnements de production de masse, Document Security prend en charge l’association des licences aux utilisateurs plutôt qu’aux documents.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 98%

---


# Envoi sécurisé de gros volumes d’information {#high-volume-secure-information-delivery}

Dans une environnement de production de masse tel que celui qui génère des factures mensuelles sécurisées pour une société de télécommunications, la création de licences propres à chaque document peut devenir un processus coûteux. Dans de tels cas, Document Security prend en charge l’association des licences aux utilisateurs plutôt qu’aux documents. La licence générée pour un utilisateur est utilisée pour tous les documents protégés pour l’utilisateur en question.

L’avantage de cette approche est que la taille de la base de données Document Security ne s’étend pas de façon linéaire avec les documents mais avec le nombre d’utilisateurs. En outre, étant donné qu’un seule licence par utilisateur suffit, la protection ultérieure des documents par le biais de ces stratégies devient plus rapide. Des fonctions telles que l’accès hors connexion, l’expiration des documents, et la révocation sont prises en charge pour tous les documents.

Document Security prend également en charge les stratégies abstraites. Les stratégies abstraites sont des modèles de stratégie contenant tous les attributs de stratégie tels que les paramètres de sécurité des documents et les droits d’utilisation mais ne contenant aucune liste des entités. Les administrateurs peuvent créer autant de stratégies qu’ils le souhaitent à partir de la stratégie abstraite avec différentes entités ayant accès aux documents. Les modifications apportées à une stratégie abstraite n’ont pas d’incidence sur les stratégies réelles qui sont générées à partir des stratégies abstraites.

Dans le cas de la génération mensuelle de factures pour une société de télécommunications, vous créez une stratégie abstraite, des utilisateurs, puis générez des licences uniques pour chaque utilisateur. Les licences sont ensuite appliquées aux documents pour chaque utilisateur.

La création de stratégies abstraites est prise en charge uniquement par le biais du SDK Java de Document Security. Vous pouvez cependant administrer les stratégies que vous créez à partir des stratégies abstraites des pages Web de Document Security. Le comportement des stratégies créées à l’aide de cette méthode est identique à celui des stratégies créées à partir des pages Web de Document Security.

Pour plus d’informations, consultez [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).
