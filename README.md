# fastai_splunk
fastai_splunk extends the fastai library to let you import your Splunk data using the familiar fastai databunch/model/learner API. It is based on the fastai.tabular implementation but uses the [Splunk Python SDK](https://github.com/splunk/splunk-sdk-python) to get your data from Splunk under the hood. For the most part, just replace the Tabular prefix for every class with Splunk and this library should do what you need it to.

# PyPI Install
`pip install fastai_splunk`

# Importing the library
`from fastai.splunk import *`

# Creating a fastai Splunk DataBunch
SplunkList parameters (similar to [TabularList from fastai.tabular](https://docs.fast.ai/tabular.data.html#TabularList
)):

  `search_query`: Splunk SPL query you want to run
  
  `splunk_path`: Path to your Splunk directory
  
  `host`: Address of your Splunk instance
  
  `username`: Username for your Splunk login
  
  `password`: Password for your Splunk username
  
  `port`: Port your Splunk instance is running on
  
  (Optional) `cat_names`: String list containing column names of your categorical variables
  
  (Optional) `cont_names`: String list containing column names of your continuous variables
  
  (Optional) `procs`: [The same procs from the fastai.tabular implementation](https://docs.fast.ai/tabular.transform.html#TabularProc)
  
Sample usage:
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

# Creating a SplunkLearner
This works the same way you [create a TabularLearner in fastai.](https://docs.fast.ai/tabular.learner.html)

Sample usage:
```
learn = splunk_learner(data, layers=[200,100], metrics=accuracy)
```


Big thanks to Jeremy Howard (jph00), Rachel Thomas (racheltho), and the other fastai contributors for such a great library!
