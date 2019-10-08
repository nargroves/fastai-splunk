# fastai_splunk
This library extends fastai to allow you import your Splunk data into a familiar fastai model/learner. fastai_splunk is based on the fastai.tabular API. To use it, just replace use the Splunk prefix instead of the Tabular prefix.

# PyPI Install
`pip install fastai_splunk`

# Importing the library
`from fastai.splunk import *`

# Creating a fastai Splunk DataBunch
SplunkList parameters:

  `search_query`: The SPL query you want to run
  
  `splunk_path`: The path to your Splunk directory
  
  `host`: The address of your Splunk instance
  
  `username`: Username for your Splunk login
  
  `password`: Password for your Splunk username
  
  `port`: The port to connect to
  
  `cat_names`: Categorical variable column names
  
  `cont_names`: Continuous variable column names
  
  `procs`: Procs
  

```
data = SplunkList.from_splunk(search_query='search *',
         splunk_path='/Applications/Splunk',
         host='localhost',
         username='admin',
         password='password',
         port=8890,
         cat_names=['Branch', 'Payment', 'Product line'],
         cont_names=['Quantity', 'Total'],
         procs=[FillMissing, Categorify, Normalize])
      .split_by_idx(list(range(1,50)))
      .label_from_df(cols=dep_var)
      .databunch()
```

# Creating a fastai Splunk Learner
This works the same way you create a TabularLearner in fastai. (https://docs.fast.ai/tabular.learner.html)
`learn = splunk_learner(data, layers=[200,100], metrics=accuracy)`
