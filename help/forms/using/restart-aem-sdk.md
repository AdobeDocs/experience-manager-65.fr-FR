---
title: Comment redémarrer AEM SDK ?
description: Bonnes pratiques pour redémarrer AEM SDK
role: Admin, Developer, User
feature: Adaptive Forms, Troubleshooting
exl-id: f5d69d04-b842-4329-b1b3-57b88266d13d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 15%

---

# Redémarrage du SDK AEM

Si vous redémarrez le SDK AEM en arrêtant les processus Java™, peut entraîner des incohérences dans l’environnement de développement AEM et une erreur se produit comme suit :

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## Solution

Pour redémarrer le SDK AEM, accédez à la fenêtre de commande active et appuyez sur `Ctrl + C` pour redémarrer le SDK.

Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java™, peut entraîner des incohérences dans l’environnement de développement AEM.
