---
keywords: Experience Platform;guide de développement;Data Science Workspace;rubriques les plus consultées;apprentissage automatique en temps réel;référence de noeud ;
solution: Experience Platform
title: Référence des noeuds d’apprentissage automatique en temps réel
topic-legacy: Nodes reference
description: Un noeud est l’unité fondamentale de laquelle des graphiques sont formés. Chaque noeud effectue une tâche spécifique et peut être lié ensemble à l’aide de liens afin de former un graphique représentant un pipeline ML. La tâche effectuée par un noeud représente une opération sur les données d’entrée, telle qu’une transformation des données ou un schéma, ou une inférence d’apprentissage automatique. Le noeud sort la valeur transformée ou déduite au(x) noeud(s) suivant(s).
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# Référence du noeud d’apprentissage automatique en temps réel (Alpha)

>[!IMPORTANT]
>
>L’apprentissage automatique en temps réel n’est pas encore disponible pour tous les utilisateurs. Cette fonctionnalité est en version alpha et est encore en cours de test. Ce document peut faire l’objet de modifications.

Un noeud est l’unité fondamentale de laquelle des graphiques sont formés. Chaque noeud effectue une tâche spécifique et peut être lié ensemble à l’aide de liens afin de former un graphique représentant un pipeline ML. La tâche effectuée par un noeud représente une opération sur les données d’entrée, telle qu’une transformation des données ou un schéma, ou une inférence d’apprentissage automatique. Le noeud sort la valeur transformée ou déduite au(x) noeud(s) suivant(s).

Le guide suivant décrit les bibliothèques de noeuds prises en charge pour l’apprentissage automatique en temps réel.

## Découverte des noeuds à utiliser dans votre pipeline ML

Copiez le code suivant dans une [!DNL Python] notebook pour afficher tous les noeuds disponibles.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**Exemple de réponse**

```json
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## Noeuds standard

Les noeuds standard s’appuient sur les bibliothèques de science de données open source telles que Pandas et ScikitLearn.

### ModelUpload

Le noeud ModelUpload est un noeud d’Adobe interne qui prend un model_path et charge le modèle du chemin d’accès du modèle local vers la banque d’objets blob d’apprentissage automatique en temps réel.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode est un noeud d’Adobe interne qui utilise un ID de modèle pour extraire le modèle ONNX pré-entraîné et l’utilise pour noter les données entrantes.

>[!TIP]
>
>Indiquez les colonnes dans l’ordre selon lequel vous souhaitez que les données soient envoyées au modèle ONNX pour que le score soit effectué.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

Le noeud pandas suivant vous permet d’importer n’importe quel `pd.DataFrame` ou toute fonction générale de niveau supérieur pandas. Pour en savoir plus sur les méthodes Pandas, consultez la section [Documentation sur les méthodes de pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Pour plus d’informations sur les fonctions de niveau supérieur, consultez la section [Guide de référence de l’API pandas pour les fonctions générales](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

Le noeud ci-dessous utilise `"import": "map"` pour importer le nom de la méthode sous la forme d’une chaîne dans les paramètres, puis en saisissant les paramètres sous la forme d’une fonction map . L’exemple ci-dessous effectue cette opération en utilisant `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Une fois la carte en place, vous avez la possibilité de définir `inplace` as `True` ou `False`. Définir `inplace` as `True` ou `False` selon que vous souhaitez appliquer ou non une transformation statique. Par défaut `"inplace": False` crée une colonne. La prise en charge d’un nouveau nom de colonne doit être ajoutée dans une version ultérieure. La dernière ligne `cols` peut être un nom de colonne unique ou une liste de colonnes. Indiquez les colonnes sur lesquelles vous souhaitez appliquer la transformation. Dans cet exemple `device` est spécifié.

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitLearn

Le noeud ScikitLearn vous permet d’importer n’importe quel modèle ou scaler ScikitLearn ML. Pour plus d’informations sur l’une des valeurs utilisées dans l’exemple, reportez-vous au tableau ci-dessous :

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver": 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Valeur | Description |
| --- | --- |
| features | Fonctionnalités d’entrée du modèle (liste des chaînes). <br> Par exemple: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Nom de la colonne cible (chaîne). |
| mode | Train/test (chaîne). |
| model_path | Chemin d’accès local au modèle d’enregistrement au format unique. |
| params.model | Chemin d’accès absolu à l’importation du modèle (chaîne), par exemple : `sklearn.linear_model.LogisticRegression`. |
| params.model_params | hyperparamètres du modèle, voir [API sklearn (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) pour plus d’informations. |
| node_instance.process(data_message_from_previous_node) | La méthode `process()` prend DataMsg du noeud précédent et applique la transformation. Cela dépend du noeud actif utilisé. |

### Split

Utilisez le noeud suivant pour fractionner votre cadre de données en formation et test en transmettant `train_size` ou `test_size`. Cette opération renvoie un cadre de données avec un multi-index. Vous pouvez accéder aux jeux de données de formation et de test à l’aide de l’exemple suivant, `msg5.data.xs(“train”)`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Étapes suivantes

L’étape suivante consiste à créer des noeuds à utiliser dans la notation d’un modèle d’apprentissage automatique en temps réel. Pour plus d’informations, consultez la [Guide d’utilisation du notebook d’apprentissage automatique en temps réel](./rtml-authoring-notebook.md).
