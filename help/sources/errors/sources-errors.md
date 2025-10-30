---
title: Messages d’erreur liés aux sources
description: Prenez connaissance des messages d’erreur que vous pouvez rencontrer lors de l’utilisation du service de flux pour les sources.
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '3057'
ht-degree: 70%

---

# Messages d’erreur liés aux sources

Ce document fournit une liste des messages d’erreur liés aux sources, avec leur description et les résolutions possibles.

## Erreurs génériques

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1000-400` | Requête incorrecte | La requête n’est pas valide. Vérifiez la requête et réessayez. |
| `1001-401` | Non autorisé | La personne utilisatrice n’est pas autorisée à effectuer cette opération. Contactez l’administration pour obtenir l’accès à la ressource. |
| `1002-403` | Interdit | L’opération demandée est interdite. Vérifiez l’opération demandée et réessayez. |
| `1003-404` | Ressource introuvable | La ressource demandée est introuvable. Vérifiez la requête fournie et réessayez. |
| `1004-415` | Type de média non pris en charge | Le format de payload fourni n’est pas pris en charge. Vérifiez la requête fournie et réessayez. |
| `1005-500` | Erreur interne | Une erreur interne sʼest produite. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1006-408` | Délai d’expiration de la requête | Une erreur s’est produite lors du traitement de la requête. La requête a expiré. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1007-400` | Paramètre d’en-tête non valide | Paramètre d’en-tête non valide : {headerName} a été reçu. Vérifiez les paramètres d’en-tête et réessayez. |
| `1008-401` | | Jeton d’autorisation non valide | Le jeton d’autorisation n’a pas accès à cette organisation ou l’organisation n’existe pas. Assurez-vous que l’organisation existe ou contactez votre administration pour y accéder. |
| `1009-403` | ID d’organisation IMS manquant ou vide | L’en-tête de la requête d’ID d’organisation est manquant ou vide. Mettez à jour la valeur de l’en-tête et réessayez. |
| `1010-500` | Message détaillé non valide | Le paramètre du message détaillé n’a pas été correctement fourni. Vérifiez le paramètre dans le message détaillé et réessayez. |
| `1011-503` | Service indisponible | Le service est temporairement indisponible. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1012-504` | Délai d’expiration de la passerelle | Un délai d’expiration de passerelle s’est produit. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1013-412` | Échec de la précondition | La condition définie par les en-têtes « If-Unmodified-Since » ou « If-None-Match » n’est pas remplie. Vérifier et réessayez. |
| `1014-400` | Requête incorrecte - Argument interdit | Impossible de traiter la demande. {detailedMessage} |

## Erreurs de framework

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1100-400` | Requête incorrecte | Impossible de traiter la demande. {detailedMessage} |
| `1101-500` | Erreur interne | Une erreur interne sʼest produite. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1102-404` | Ressource introuvable | La ressource demandée est introuvable. {detailedMessage} |
| `1103-503` | Service indisponible | Le service est temporairement indisponible. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1104-504` | Délai d’expiration de la passerelle | Un délai d’expiration de passerelle s’est produit. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1105-401` | Non autorisé | L’utilisateur n’est pas autorisé. {detailedMessage} |
| `1106-403` | Interdit | L’opération demandée est interdite. {detailedMessage} |
| `1107-412` | Échec de la précondition | La condition définie par les en-têtes If-Unmodified-Since ou If-None-Match n’est pas remplie. {detailedMessage} |

## Erreurs de chiffrement

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1200-500` | Erreur interne | Une erreur interne sʼest produite. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1201-400` | Requête incorrecte | L’ID de flux ne peut pas être nul ou vide. Indiquez un ID de flux valide dans la requête et réessayez. |
| `1202-400` | Requête incorrecte | L’ID publicKeyId est manquant dans les transformations={transformations} du flux. Indiquez l’ID publicKeyId dans la requête et réessayez. |
| `1203-400` | Requête incorrecte | La clé de chiffrement n’existe pas par rapport à keyID={keyID} dans les transformations={transformations} du flux. Vérifiez l’ID keyID fourni et réessayez. |
| `1204-400` | Requête incorrecte | L’algorithme de chiffrement fourni n’est pas valide. Indiquez un algorithme de chiffrement valide et réessayez. |
| `1205-400` | Requête incorrecte | La phrase secrète est manquante dans la section des paramètres de la requête fournie. Indiquez une phrase secrète dans les paramètres et réessayez. |

## Erreurs de l’API REST

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1300-400` | Requête incorrecte | La requête de connexion PATCH n’est pas prise en charge pour le connecteur {connectorType}. Vérifiez la requête fournie et réessayez. |
| `1301-400` | Requête incorrecte | Le paramètre authSpecType fourni : {authSpecType} n’est pas pris en charge. Indiquez un type de spécification d’authentification valide et réessayez. |
| `1302-400` | Requête incorrecte | Le type d’authentification fourni = {authType} n’est pas pris en charge pour le connector={connectorType}. Indiquez un type d’authentification valide pour le connecteur donné. |
| `1303-400` | Requête incorrecte | L’URL n’a pas pu être codée avec les paramètres d’authentification donnés, car le codage d’URL n’est pas pris en charge pour {value}. Vérifiez les paramètres d’authentification et réessayez. |
| `1304-400` | Requête incorrecte | Le champ obligatoire {field} n’est pas fourni. Indiquez le {field} et réessayez. |
| `1305-400` | Requête incorrecte | Le type de connecteur fourni = {connectorType} n’est pas pris en charge pour cette opération. |
| `1306-400` | Requête incorrecte | La connexion cible ne peut pas être nulle lors de la validation de l’identifiant de spécification de connexion cible. Vérifiez la requête fournie et réessayez. |
| `1307-400` | Requête incorrecte | L’identifiant de spécification de connexion cible n’est pas valide={targetConnectionSpecId}. La valeur autorisée est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Requête incorrecte | La requête n’a pas pu être traitée. Message d’erreur : {msftErrorMessage} |
| `1309-400` | Requête incorrecte | La transformation de chiffrement fournie n’est pas valide, car {requiredParam} est manquant dans les paramètres. Indiquez le {requiredParam} et réessayez. |
| `1310-400` | Requête incorrecte | L’ID publicKeyId fourni dans les paramètres a expiré. Indiquez un ID publicKeyId valide et réessayez. |
| `1311-400` | Requête incorrecte | L’ID publicKeyId fourni dans les paramètres n’est pas valide. Indiquez un ID publicKeyId valide et réessayez. |
| 1312-400 | Requête incorrecte | La valeur de paramètre fournie {paramValue} n’est pas une entrée valide pour la propriété={requestParam}. Indiquez une valeur de paramètre valide et réessayez. |
| `1313-400` | Requête incorrecte | L’attribut de chemin {attribute} n’existe pas. Vérifiez que l’attribut existe et réessayez. |
| `1314-400` | Requête incorrecte | Un chemin complexe a été fourni mais n’est pas autorisé. Vérifiez que le chemin complexe n’est pas fourni et réessayez. |
| `1315-400` | Requête incorrecte | Le chemin d’accès fourni {path} doit pointer vers un tableau d’enregistrements. Assurez-vous que le chemin d’accès fourni pointe vers le tableau d’enregistrements et réessayez. |
| `1316-400` | Requête incorrecte | Les paramètres de pagination fournis ne doivent pas être vides. Indiquez des paramètres de pagination valides et réessayez. |
| `1317-400` | Requête incorrecte | Les paramètres de planification fournis sont vides mais ne devraient pas l’être. Indiquez des paramètres de planification valides et réessayez. |
| `1318-400` | Requête incorrecte | {combinedMessage}. Vérifiez la requête fournie et réessayez. |
| `1319-400` | Requête incorrecte | Le {param} doit faire partie de la collection parente. Indiquez le {param} dans la collection parente et réessayez. |
| `1320-400` | Requête incorrecte | Le {idType} ne peut pas être nul ou vide. Indiquez un {idType} valide et réessayez. |
| `1321-400` | Requête incorrecte | La longueur de {idType} doit être un, la taille fournie est {size}. Indiquez une taille valide et réessayez. |
| `1322-400` | Requête incorrecte | La connexion source ne peut pas être nulle pour la création de la référence de schéma. Indiquez une connexion source valide et réessayez. |
| `1323-400` | Requête incorrecte | Le {entity} ne peut pas être nul ou vide dans la connexion source : {sourceConnection}. Indiquez un {entity} valide et réessayez. |
| `1324-400` | Requête incorrecte | La connexion cible ne peut pas être nulle lors de l’extraction de l’ID du jeu de données. Indiquez une connexion cible valide et réessayez. |
| `1325-400` | Requête incorrecte | Le paramètre dataSetId ne peut pas être nul ou vide dans la connexion cible : {TargetConnection}. Indiquez un paramètre dataSetId valide et réessayez. |
| `1326-400` | Requête incorrecte | La connexion source ne peut pas être nulle lors de la récupération du format source. Indiquez une connexion source valide et réessayez. |
| `1327-400` | Requête incorrecte | Le format des données sources fourni={sourceFormat} dans SourceConnection n’est pas pris en charge. Les valeurs autorisées sont : {values}. Indiquez les valeurs autorisées et réessayez. |
| `1328-400` | Requête incorrecte | La transformation de mappage ne peut pas être nulle lors de l’extraction de {param}. Veuillez fournir une transformation de mappage valide et réessayer. |
| `1329-400` | Requête incorrecte | Le paramètre : {param} ne peut pas être nul ou vide dans la requête fournie. Indiquez un {param} valide et réessayez. |
| `1330-400` | Requête incorrecte | Aucune colonne n&#39;a été trouvée pour le tableau {tableName}. Indiquez un nom de tableau valide et réessayez. |
| `1331-400` | Requête incorrecte | Le délimiteur de colonne ne peut pas contenir plus d&#39;un caractère dans SourceConnection : {sourceConnection}. Indiquez un délimiteur de colonne valide, puis réessayez. |
| `1332-400` | Requête incorrecte | La demande de connexion source avec le connectionSpecId : {connectionSpecId} ne peut pas avoir de baseConnectionId. Supprimez le baseConnectionId et réessayez. |
| `1333-400` | Requête incorrecte | Le flowRunAction={flowRunAction} n’est pas pris en charge pour la source avec l’ID de spécification={specId}. Spécifiez une action d’exécution de flux valide et réessayez. |
| `1334-400` | Requête incorrecte | Le paramètre de requête : {param} ne peut pas être vide. Indiquez un {param} valide et réessayez. |
| `1335-400` | Requête incorrecte | Une erreur s’est produite lors de la sérialisation des paramètres de filtre à explorer. Vérifiez votre requête de paramètre de filtre, puis réessayez. |
| `1336-400` | Requête incorrecte | La connexion Explorer n’est pas prise en charge pour l’ID de spécification de connexion {connectionSpecId}. Indiquez un ID de spécification de connexion pris en charge et réessayez. |
| `1337-400` | Requête incorrecte | Le {QueryParam} ne peut pas être vide pour objectType={objectType}. Indiquez un {QueryParam} valide et réessayez. |
| `1338-400` | Requête incorrecte | L’ID de connexion {connectionType} ne peut pas être nul dans flowRequest. Indiquez un ID de connexion {connectionType} valide dans flowRequest. |
| `1339-400` | Requête incorrecte | Le format de l’organisation={imsOrg} fourni dans la requête n’est pas valide. Indiquez un ID d’organisation valide et réessayez. |
| `1340-400` | Requête incorrecte | Une erreur s’est produite lors de l’analyse de {time}. Vérifiez le format d’heure indiqué dans la requête et réessayez. |
| `1341-400` | Requête incorrecte | Le code Json ODI fourni est vide. Veuillez fournir un code Json ODI valide et réessayer. |
| `1342-400` | Requête incorrecte | Il manque des définitions au segment &#39;dls:folder&#39; du fichier &#39;odi.json&#39;. Indiquez les définitions appropriées dans « odi.json » et réessayez. |
| `1343-400` | Requête incorrecte | Les définitions des segments « dls:entityReferences » et « dls:partitionSpec » dans « odi.json » sont manquantes. Indiquez les définitions appropriées dans « odi.json », puis réessayez. |
| `1344-400` | Requête incorrecte | La définition de « dls :partitionSpec » dans « odi.json » n’est pas valide, car plusieurs partitionSpecs ont été trouvées. Indiquez les définitions appropriées dans « odi.json » et réessayez. |
| `1345-400` | Requête incorrecte | Il manque des définitions dans un ou plusieurs segments dans les chemins : « dls:partitionSpec/dls:fileFormat », « dls:partitionSpec/dls:partitionTemplate », « dls:partitionSpec/dls:fileFormat/@type », « dls:partitionSpec/dls:fileFormat/dls:csvDelimiters » dans « odi.json ». Indiquez les définitions appropriées dans « odi.json » et réessayez. |
| `1346-400` | Requête incorrecte | La définition « @type » fournie dans « dls :fileFormat » dans « odi.json » n’est pas valide. Indiquez les définitions appropriées dans « odi.json » et réessayez. |
| `1347-400` | Requête incorrecte | La définition de dls:csvDelimiters&#39; dans &#39;odi.json&#39; n’est pas prise en charge. Les csvDelimiters pris en charge sont les suivants : [ et ]. Indiquez les définitions appropriées dans « odi.json » et réessayez. |
| `1348-400` | Requête incorrecte | Une erreur s&#39;est produite lors de la désérialisation de &#39;dls:entityReferences&#39;. Vérifiez si les données sont dans un format valide et réessayez. |
| `1349-400` | Requête incorrecte | Les paramètres de filtre fournis ne sont pas valides. Indiquez des paramètres de filtre valides et réessayez. |
| `1350-400` | Requête incorrecte | Aucun opérateur n’a été fourni pour le filtre à la source. Indiquez une requête de filtre valide avec l’opérateur approprié et réessayez. |
| `1351-400` | Requête incorrecte | L’opérateur fourni {operator} n’est pas pris en charge pour le filtre à la source de ce connecteur. Indiquez un opérateur valide et réessayez. |
| `1352-400` | Requête incorrecte | L’opérateur fourni {operator} ne peut pas être mappé à un opérateur natif pris en charge pour {ql}. Indiquez un opérateur valide et réessayez. |
| `1353-400` | Requête incorrecte | Le filtre à la source n’est pas encore pris en charge pour le connecteur {connectorType}. Consultez les connecteurs pris en charge dans la documentation : https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html?lang=fr. |
| `1354-400` | Requête incorrecte | Le {ql} de langage de requête n’est pas encore pris en charge pour le filtre à la source. Indiquez un langage de requête valide et réessayez. |
| `1355-400` | Requête incorrecte | Le type de filtre fourni n’est pas valide. Le type de filtre pris en charge est le suivant : PQL. Indiquez un type de filtre valide et réessayez. |
| `1356-400` | Requête incorrecte | Le format de filtre fourni n’est pas valide. Le format de filtre pris en charge est le suivant : pql/json. Indiquez un format de filtre valide et réessayez. |
| `1357-400` | Requête incorrecte | Le filtre fourni n’est pas valide. La valeur doit être fournie avec des filtres détaillés. Indiquez un filtre valide et réessayez. |
| `1358-400` | Requête incorrecte | Le paramètre fourni « objectType » n’est pas valide. Indiquez un paramètre objectType valide et réessayez. |
| `1359-400` | Requête incorrecte | Le paramètre {param} est manquant dans la requête. Indiquez un {param} valide et réessayez. |
| `1360-400` | Requête incorrecte | L’heure de début ne peut pas être définie dans le passé. Indiquez une heure de début valide et réessayez. |
| `1361-400` | Requête incorrecte | L’intervalle n’est pas autorisé lors d’une ingestion unique. Supprimez l’intervalle ou modifiez la fréquence, puis réessayez. |
| `1362-400` | Requête incorrecte | L’intervalle ne peut pas être inférieur à {minInterval}. Indiquez une valeur d’intervalle valide et réessayez. |
| `1363-400` | Requête incorrecte | L’intervalle {interval} est interdit avec la fréquence suivante : {frequency}. Indiquez une valeur d’intervalle valide et réessayez. |
| `1364-400` | Requête incorrecte | L’indicateur de renvoi n’est pas autorisé lorsque la fréquence est définie sur une seule fois. Supprimez l’indicateur de renvoi lorsque la fréquence est définie sur une seule fois et réessayez. |
| `1365-400` | Requête incorrecte | Le chemin {path} fourni dans « ops » n’est pas valide. Indiquez un chemin d’accès valide {path} et réessayez. |
| `1366-400` | Requête incorrecte | L’heure de début est passée et l’opération de mise à jour n’est plus autorisée. |
| `1367-400` | Requête incorrecte | La colonne delta est obligatoire dans la transformation de copie lors de la création d’un connecteur CRM. Indiquez la colonne delta et réessayez. |
| `1368-400` | Requête incorrecte | Le mode n’est pas autorisé dans la requête de flux. Vérifiez la requête et réessayez. |
| `1369-400` | Requête incorrecte | La colonne delta de la transformation de copie n’est pas autorisée lorsque la fréquence est définie sur une seule fois. Supprimez la colonne delta et réessayez. |
| `1370-400` | Requête incorrecte | Les colonnes sources n’ont pas pu être récupérées pour l’ingestion, car la transformation de mappage est manquante. Ajoutez la transformation de mappage et réessayez. |
| `1371-400` | Requête incorrecte | La détection des propriétés du fichier n’est pas prise en charge pour le connecteur {connectorType}. Indiquez les propriétés du fichier manuellement. |
| `1372-400` | Requête incorrecte | L’opération actuelle n’est pas autorisée. L’exploration via la spécification de connexion n’est pas autorisée pour la spécification de connexion ID={connectionSpecId}. |
| `1373-400` | Requête incorrecte | Le type « flowSpecType » est manquant dans la requête. Indiquez un type « flowSpecType » valide et réessayez. |
| `1374-400` | Requête incorrecte | Les paramètres de requête fournis ne sont pas valides. L’indicateur determineProperties et les propriétés définies par l’utilisateur ou l’utilisatrice ne peuvent pas être présents dans la même requête. Corrigez la requête et réessayez. |
| `1375-400` | Requête incorrecte | Échec de la détection des propriétés du fichier. Indiquez les propriétés manuellement. |
| `1376-400` | Requête incorrecte | La détection des propriétés du fichier n’est pas prise en charge pour la spécification de connexion id={connectionSpecId}. Indiquez les propriétés du fichier manuellement. |
| `1377-400` | Requête incorrecte | Le paramètre de valeur fourni est nul et ne peut pas être comparé à l’opérateur {operator}. Indiquez un paramètre de valeur valide et réessayez. |
| `1378-400` | Requête incorrecte | Une erreur s’est produite lors de la validation du {column} de colonne d’entrée pour le filtre à la source. Le nom de la colonne doit être une colonne valide du tableau. Indiquez un nom de colonne valide et réessayez. |
| `1379-400` | Requête incorrecte | Une erreur s’est produite lors de la validation du {value} d’entrée pour le filtre à la source. Le type de données de la colonne à la source est {columnDataType} et la valeur DataType [String] ne correspond pas. Indiquez un {value} valide et réessayez. |
| `1380-400` | Requête incorrecte | Échec de la création de l’exécution du flux. Message d’erreur : {message} |
| `1381-400` | Requête incorrecte | WindowEndTime={endTime} ne peut pas être antérieur à Window StartTime={startTime}. Indiquez une heure de fin valide et réessayez. |
| `1382-400` | Requête incorrecte | La colonne delta doit correspondre à la valeur présente dans les transformations de copie du flux. Indiquez une colonne delta valide et réessayez. |
| `1383-400` | Requête incorrecte | La colonne delta est manquante dans les paramètres reçus pour la création d’une exécution de flux. Indiquez la colonne delta dans les paramètres et réessayez. |
| `1384-400` | Requête incorrecte | Les paramètres={params} fournis pour la création de l’exécution de flux ne sont pas valides ou sont vides. Indiquez des paramètres valides et réessayez. |
| `1385-400` | Requête incorrecte | Le type de connecteur={connectorType} fourni n’est pas pris en charge pour la création d’exécutions de flux. Indiquez un type de connecteur valide et réessayez. |
| `1386-400` | Requête incorrecte | flowId={flowId} avec la fréquence scheduleParams={frequency} n’est pas pris en charge pour la création d’exécutions de flux. Indiquez une fréquence valide et réessayez. |
| `1387-400` | Requête incorrecte | flowRunId={flowRunId} est dans un état non valide={state} pour le redéclenchement. Réessayez après un certain temps et contactez l’assistance clientèle si le problème persiste. |
| `1388-400` | Requête incorrecte | Le flux={flow} est dans l’état={state} et ne peut pas être redéclenché. Le flux doit avoir l’état activé pour le redéclenchement. |
| `1389-400` | Requête incorrecte | Une erreur s’est produite lors de l’analyse de la chaîne codée en base64 fournie. Indiquez une chaîne de filtre codée valide et réessayez. |
| `1390-400` | Requête incorrecte | L’opérateur « not » ne peut pas avoir plusieurs comparaisons. Indiquez un nombre valide de comparaisons et réessayez. |
| `1391-400` | Requête incorrecte | Échec de l’analyse de SchemaMetaData dans sourceConnection pour Id={sourceConnectionId}. Vérifiez le paramètre schemaMetaData de la requête et réessayez. |
| `1392-400` | Requête incorrecte | Échec de l’analyse des transformations dans la requête de flux pour flowId={flowId}. Vérifiez les transformations de la requête et réessayez. |
| `1393-400` | Requête incorrecte | Le paramètre fourni {parameter} est nul ou vide. Indiquez un {parameter} valide et réessayez. |
| `1394-400` | Requête incorrecte | La valeur minimale pour un paramètre {parameter} est de un. Indiquez un {parameter} valide et réessayez. |
| `1395-400` | Requête incorrecte | La connexion source trouvée dans le flux est nulle ou vide. Indiquez une connexion source valide dans le flux et réessayez. |
| `1396-400` | Requête incorrecte | Impossible de trouver un format correspondant. Veuillez fournir un format correspondant et réessayer. |
| `1397-400` | Requête incorrecte | La fréquence fournie : {frequency} n’est pas valide. Indiquez une fréquence valide et réessayez. |
| `1398-400` | Requête incorrecte | L’opération fournie : {action} n’est pas prise en charge. Vérifiez l’opération fournie et réessayez. |
| `1399-400` | Requête incorrecte | Un requestFileType valide est introuvable. Veuillez fournir un requestFileType valide et réessayer. |
| `1400-400` | Requête incorrecte | Le paramètre fourni « templateType » n’est pas valide. Indiquez un type de modèle valide et réessayez. |
| `1401-400` | Requête incorrecte | L’action d’exécution de flux={flowRunAction} fournie n’est pas prise en charge. Indiquez une action d’exécution de flux valide et réessayez. |
| `1402-500` | Erreur interne | Une erreur interne sʼest produite. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1403-400` | Requête incorrecte | L’heure de début est dépassée et vous ne pouvez plus changer la fréquence sur « une seule fois ». |
| `1404-400` | Requête incorrecte | L’heure de début est dépassée et vous ne pouvez plus mettre à jour le renvoi. |

## Exceptions de service de flux (1600-1699)

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1600-400` | Requête incorrecte | Impossible de traiter la demande. {detailedMessage} |
| `1601-500` | Erreur interne | Une erreur interne sʼest produite. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1602-404` | Ressource introuvable | La ressource demandée est introuvable. {detailedMessage} |
| `1603-503` | Service indisponible | Le service est temporairement indisponible. Veuillez réessayer. Contactez l’assistance clientèle si le problème persiste. |
| `1604-504` | Délai d’expiration de la passerelle | Un délai d’expiration de passerelle s’est produit. Veuillez réessayer. Contactez l’assistance clientèle si le problème persiste. |
| `1605-401` | Non autorisé | L’utilisateur n’est pas autorisé. {detailedMessage} |
| `1606-403` | Interdit | L’opération demandée est interdite. {detailedMessage} |
| `1607-412` | Échec de la précondition | La condition définie par les en-têtes If-Unmodified-Since ou If-None-Match n’est pas remplie. {detailedMessage} |

## Erreurs de zone d’atterrissage de données

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1700-500` | Erreur interne | Une erreur interne sʼest produite. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1701-400` | Requête incorrecte | La zone d’atterrissage fournie est inactive. Veuillez activer la zone d’atterrissage et réessayer. |
| `1702-400` | Requête incorrecte | Le type SAS={sasType} fourni pour la zone d’atterrissage n’est pas autorisé. Veuillez fournir un SAS valide et réessayer. |
| `1703-400` | Requête incorrecte | L’actualisation des informations d’identification n’est pas autorisée. |
| `1704-400` | Requête incorrecte | Les clés renvoyées pour storageAccountName={accountName} dans subscriptionId={subscriptionId} et resourceGroupName={resourceGroupName} sont incorrectes. Vérifiez la requête et réessayez. Veuillez contacter le support si le problème persiste. |
| `1705-400` | Requête incorrecte | L’action de zone d’atterrissage de données fournie n’est pas prise en charge. Veuillez fournir une action valide et réessayer. |
| `1706-400` | Requête incorrecte | La configuration des activations autorisées n’est pas correcte pour la zone d’atterrissage={landingZoneType}. Réessayez. Si le problème persiste, contactez l’assistance clientèle. |
| `1707-400` | Requête incorrecte | Le service n’a pas pu démarrer, car la configuration de la zone d’atterrissage ne peut pas être nulle ou vide. Assurez-vous que la configuration de la zone d’atterrissage n’est pas nulle et réessayez. |
| `1708-400` | Requête incorrecte | La configuration du conteneur ne peut pas être nulle dans landingZoneType={landingZoneType}. Assurez-vous que la configuration du conteneur n’est pas nulle et réessayez. |
| `1709-400` | Requête incorrecte | Les détails du SAS ne peuvent pas être nuls pour les {tokenConfig} dans landingZoneType={landingZoneType}. Indiquez un SAS valide dans la configuration et réessayez. |
| `1710-400` | Requête incorrecte | La zone d’atterrissage fournie de type : {landingZoneUseCase} n’est pas prise en charge. Indiquez un type de zone d’atterrissage valide et réessayez. |
| `1711-400` | Requête incorrecte | Les détails SAS sont introuvables pour la zone d’atterrissage de données fournie de type : {landingZoneUseCase}. Vérifiez si les détails du SAS sont fournis pour le type de zone d’atterrissage fourni. |
| `1712-400` | Requête incorrecte | L’action de zone d’atterrissage fournie : {actionType} n’est pas autorisée. Indiquez une action de zone d’atterrissage de données valide et réessayez. |
| `1713-400` | Requête incorrecte | Le {OperationType} n’est pas autorisé pour le {tokenType} fourni. Vérifiez la requête et réessayez. |
| `1714-400` | Requête incorrecte | Le clientId={clientId} n’est pas autorisé à effectuer cette opération. Vérifiez votre requête et les autorisations et réessayez. |
