# interactive-widget-for-PyTerrier-on-Colab-notebook
This notebook will provide guidance to use our proposed fig_display() method to simplify your IR experimental process using PyTerrier.  Please read the API and then follow the guidance to try each function of the method.

# API
fig_display(pipelines, topics=None, qrels=None, eval_metrics=None, names=None,perquery=False, baseline=None, **kwargs)

# Introduction

fig_display() is a UI tool for PyTerrier based on ipywidgets, i.e. a user interface for IR experiments that can be used within Jupyter notebooks.

Users can use this method to see the results of IR experiments and compare them under different situations through tables and figures by only entering parameters instead of a long piece of code using Pyterrier.

The tool offers various functionalities. When the preconditions of a given functionality is satisfied, the functionalities is available. If more than one function's condition is satisfied, multiple functionalities will be available.

# Functionalities

# 1. Display results for a query ("SINGLE QUERY" tab)

If the parameter 'topics' is None, the result of retrieval transformation will be shown after the user enters a text-based query.

If the parameter 'topics' contains a DataFrame of topics (e.g. obtained from a dataset, c.f. dataset.get_topics()), then users can select a system and a query from those they input to view the result. If qrels are also provided, the label documents of documents will also be displayed (c.f. relevant or not).

# 2. Comparison of two systems side by side ("COMPARE" tab)

If there is more than one transformer pipeline, a comparison of the results of two transformer pipelines can be shown side by side.

# 3. Average performance ("AVERAGE PERFORMANCE" tab)

When there is more than one transformer pipeline, if the parameter 'perquery' is True, a figure of the difference of the value of a pt.Experiment() between two transformer pipelines with the specificed evaluation measures can be shown. Users can select any two pipelines and any one measure from the parameter they input and they also can choose the threshold of the difference to filter the result whereas (perquery is False), the table of the result of the experiment() will be shown.

!Note: the figure file of the picture can be downloaded from "Files" by clicking the file icon on the left side, then putting the mouse on fig.jpg and clicking "..." to choose "download".

#Parameters:

In general, the parameters to fig_display() correspond to the parameters supported by pt.Experiment(), and should be familiar to any experienced PyTerrier user.

pipelines(list, pyterrier.Transformer) - A list of transformers or a transformer to evaluate. If you already have the results for one (or more) of your systems, a results dataframe can also be used here. Results produced by the transformers must have “qid”, “docno”, “score”, “rank” columns.

topics(str, pandas.DataFrame)(default: None) - Either a String form of the query or a path to a topics file or a pandas.Dataframe with columns=[‘qid’, ‘query’]. If 'topics' is None, users can enter a string form of query on page "SINGLE QUERY" for further operations.

qrels(pandas.DataFrame) - Either a path to a qrels file or a pandas.Dataframe with columns=[‘qid’,’docno’, ‘label’]

eval_metrics(list)(default: [‘map’]) - Which evaluation metrics to use. e.g. [‘map’]

name(list) - List of names for each retrieval system when presenting the results. Default=None. If None: Obtains the str() representation of each transformer as its name.

perquery(bool)(default: False) – If True returns each metric for each query, else return mean metrics across all queries. Default=False.

baseline(int)(default: None) – If set to the index of an item of the retr_system list, will calculate the number of queries improved, degraded and the statistical significance (paired t-test p value) for each measure. Default=None: If None, no additional columns will be added for each measure.
