---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real-time Machine Learning;node reference;
solution: Experience Platform
title: Guide de référence des noeuds d’apprentissage automatique en temps réel
topic: Nodes reference
translation-type: tm+mt
source-git-commit: dc63ad0c0764355aed267eccd1bcc4965b04dba4
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---


# Guide de référence des noeuds d’apprentissage automatique en temps réel (Alpha)

>[!IMPORTANT]
>L&#39;apprentissage automatique en temps réel n&#39;est pas encore disponible pour tous les utilisateurs. Cette fonction est en alpha et est encore en cours de test. Ce document est sujet à changement.

Un noeud est l’unité fondamentale dont les graphiques sont formés. Chaque noeud exécute une tâche spécifique et peut être chaîné ensemble à l’aide de liens afin de former un graphique représentant un pipeline ML. La tâche exécutée par un noeud représente une opération sur les données d’entrée, telle qu’une transformation de données ou de schéma, ou une inférence d’apprentissage automatique. Le noeud envoie la valeur transformée ou déduite au(x) noeud(s) suivant(s).

Le guide suivant décrit les bibliothèques de noeuds prises en charge pour l’apprentissage automatique en temps réel.

## Découverte de noeuds à utiliser dans votre pipeline ML

Copiez le code suivant dans un bloc-notes Python pour vue tous les noeuds disponibles pour l&#39;utilisation.

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

Les noeuds standard s&#39;appuient sur les bibliothèques de données open source telles que Pandas et ScikitLearn.

### ModelUpload

Le noeud ModelUpload est un noeud interne d’Adobe qui prend un chemin_modèle et télécharge le modèle depuis le chemin d’accès du modèle local vers la banque de blocs d’apprentissage automatique en temps réel.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode est un noeud interne d’Adobe qui utilise un ID de modèle pour extraire le modèle ONNX préentraîné et l’utilise pour marquer les données entrantes.

>[!TIP]
>Spécifiez les colonnes dans le même ordre que celui dans lequel vous souhaitez que les données soient envoyées au modèle ONNX pour obtenir un score.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

Le noeud Pandas suivant vous permet d’importer n’importe quelle `pd.DataFrame` méthode ou fonction générale de niveau supérieur pandas. Pour en savoir plus sur les méthodes Pandas, consultez la documentation [sur les méthodes](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)Pandas. Pour plus d&#39;informations sur les fonctions de niveau supérieur, consultez le guide de référence de l&#39;API [Pandas pour les fonctions](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html)générales.

Le noeud ci-dessous utilise `"import": "map"` pour importer le nom de la méthode sous la forme d’une chaîne dans les paramètres, puis pour entrer les paramètres sous la forme d’une fonction de mappage. L’exemple ci-dessous effectue cette opération en utilisant `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Une fois la carte en place, vous avez la possibilité de la définir `inplace` en tant que `True` ou `False`. Définissez `inplace` la variable comme `True` ou `False` selon si vous souhaitez appliquer ou non la transformation. Par défaut, `"inplace": False` crée une colonne. La prise en charge d’un nouveau nom de colonne est définie pour être ajoutée dans une version ultérieure. La dernière ligne `cols` peut être un nom de colonne unique ou une liste de colonnes. Spécifiez les colonnes sur lesquelles vous souhaitez appliquer la transformation. Dans cet exemple, `device` est spécifié.

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

Le noeud ScikitLearn vous permet d&#39;importer n&#39;importe quel modèle ou scaler ScikitLearn ML. Utilisez le tableau ci-dessous pour plus d’informations sur l’une des valeurs utilisées dans l’exemple :

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver" : 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Valeur | Description |
| --- | --- |
| fonctionnalités | Fonctionnalités d&#39;entrée du modèle (liste de chaînes). <br> Par exemple: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Nom de la colonne de Cible (chaîne). |
| mode | Train/test (chaîne). |
| model_path | Chemin d&#39;accès au modèle d&#39;enregistrement local au format unique. |
| params.model | Chemin d&#39;importation absolu du modèle (chaîne), par exemple : `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Les hyperparamètres du modèle, consultez la documentation de l’API [sklearn (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) pour plus d’informations. |
| node_instance.process(data_message_from_previous_node) | La méthode `process()` prend DataMsg du noeud précédent et applique la transformation. Cela dépend du noeud actif utilisé. |

### Partage

Utilisez le noeud suivant pour fractionner votre dataframe en train et tester en passant `train_size` ou `test_size`. Cette opération renvoie une base de données avec un index multiple. Vous pouvez accéder aux jeux de données de train et de test à l&#39;aide de l&#39;exemple suivant, `msg5.data.xs(“train”)`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Étapes suivantes

L’étape suivante consiste à créer des noeuds à utiliser pour marquer un modèle d’apprentissage automatique en temps réel. Pour plus d&#39;informations, consultez le guide [d&#39;utilisation du bloc-notes](./rtml-authoring-notebook.md)d&#39;apprentissage automatique en temps réel.
