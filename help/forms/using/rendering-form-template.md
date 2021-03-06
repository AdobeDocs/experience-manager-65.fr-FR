---
title: Rendu du modèle de formulaire pour des formulaires HTML5
seo-title: Rendering form template for HTML5 forms
description: Les profils de formulaires HTML5 sont associés aux rendus de profils Les rendus de profils sont des pages JSP chargées de générer la représentation HTML du formulaire en appelant le service Forms OSGi.
seo-description: HTML5 forms profiles are associated with profile renders. Profile Renders are JSP pages responsible for generating HTML representation of the form by calling the Forms OSGi service.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '535'
ht-degree: 100%

---

# Rendu du modèle de formulaire pour des formulaires HTML5 {#rendering-form-template-for-html-forms}

## Point de fin du rendu {#render-endpoint}

Les formulaires HTML5 intègrent la notion de **Profils**, lesquels sont exposés en tant que points d’entrée REST pour activer le rendu sur périphériques mobile des modèles de formulaire. Ces profils sont associés à des **rendus de profil**. Ce sont des pages JSP chargées de générer la représentation HTML du formulaire en appelant le service Forms OSGi. Le chemin d’accès JCR du nœud de profil détermine l’URL du point de fin du rendu. Le point de fin du rendu par défaut du formulaire pointant vers le profil « par défaut» ressemble à :

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*path of the folder containg form xdp*>&amp;template=&lt;*name of the xdp*>

Par exemple, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Pour un profil personnalisé, le point de fin change en conséquence. Par exemple, le point de fin du profil personnalisé appelé hrforms est :

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Si votre modèle réside dans le référentiel AEM d’une application appelée FormSubmission, l’URI est :

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Paramètres de rendu {#render-parameters}

Les paramètres de requête pris en charge lors du rendu d’un formulaire au format HTML sont les suivants :

<table>
 <tbody>
  <tr>
   <th><strong>Paramètre </strong></th>
   <th><strong>Description</strong></th>
  </tr>
  <tr>
   <td>template<br /> </td>
   <td>Ce paramètre spécifie le nom du fichier de modèle.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>Ce paramètre spécifie le chemin d’accès à l’emplacement où résident le modèle et les ressources connexes. Ce chemin d’accès peut être le chemin d’accès au système de fichiers du serveur, au référentiel, ou un chemin d’accès http ou ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Ce paramètre spécifie l’adresse URL à laquelle sont envoyées les données du formulaire au format XML.<br /> </td>
  </tr>
 </tbody>
</table>

### Fusionner des données avec le modèle de formulaire {#merge-data-with-form-template}

| Paramètre | Description |
|---|---|
| dataRef | Ce paramètre indique le **chemin d’accès absolu** du fichier de données fusionné avec le modèle. Ce paramètre peut être une adresse URL d’accès à un service REST renvoyant les données au format XML. |
| data | Ce paramètre spécifie les octets de données codés au format UTF-8 qui sont fusionnés avec le modèle. Si ce paramètre est spécifié, le formulaire HTML5 ignore le paramètre dataRef. |

### Passage du paramètre de rendu {#passing-the-render-parameter}

Les formulaires HTML5 prennent en charge trois méthodes pour transmettre des paramètres de rendu. Vous pouvez transmettre des paramètres par le biais de l’URL, des paires de valeur de clé, et du nœud de profil. Dans le paramètre de rendu, la paire de valeur de clé a la priorité la plus élevée, suivie du nœud de profil. Le paramètre de requête d’URL a la priorité la plus faible.

* **Paramètres de requête URL** : Vous pouvez spécifier les paramètres de rendu dans l’URL. Dans les paramètres de requête d’URL, les paramètres sont visibles par l’utilisateur final. Par exemple, l’URL d’envoi suivante contient le paramètre de modèle dans l’URL : `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`.

* **Paramètres de demande SetAttribute** : Vous pouvez spécifier les paramètres de rendu sous la forme d’une paire de valeurs de clé. Dans les paramètres de demande SetAttribute, les paramètres ne sont pas visibles par l’utilisateur final. Vous pouvez transférer une requête depuis un autre JSP vers le JSP de rendu de profil HTML5 et utiliser *setAttribute* sur l’objet de la requête pour transmettre tous les paramètres de rendu. Cette méthode a la priorité la plus élevée.

* **Paramètres de demande de nœud de profil :** vous pouvez spécifier les paramètres de rendu en tant que propriétés de nœud d’un nœud de profil. Dans les paramètres de requête de nœud de profil, les paramètres ne sont pas visibles par l’utilisateur. Le nœud de profil est le nœud où la requête est envoyée. Pour spécifier des paramètres en tant que propriétés de nœud, utilisez CRXDE lite.

### Paramètres d’envoi {#submit-parameters}

Les formulaires HTML5 envoient des données ; exécutent les scripts et les services Web côté serveur sur des serveurs AEM. Pour plus d’informations sur les paramètres utilisés pour exécuter les scripts et les services Web côté serveur sur les serveurs AEM, voir le [Proxy de service des formulaires HTML5](/help/forms/using/service-proxy.md).
