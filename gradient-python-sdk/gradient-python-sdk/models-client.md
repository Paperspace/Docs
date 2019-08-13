# Models Client

### Importing

```python
from gradient import ModelsClient
api_key='YOUR_API_KEY'

models_client = ModelsClient(api_key)
```

### Models List

List the models created by an experiment or within a project

```text
models = models_client.list(project_id = project_id)
print(models[0])
```

The model object

```text
Model(id='mo301q57sawrvw', name=None, project_id='prlvf0u05', 
    experiment_id='esxfbgzu7xanst', tags=None, model_type='Tensorflow', 
    url='s3://ps-projects/prlvf0u05/esxfbgzu7xanst/model/', 
    model_path='/storage/models/sdk_test', deployment_state='Stopped',
    summary={'accuracy': {'result': {'max': 0.8986999988555908, 'median': 0.8986999988555908, 
    'min': 0.8986999988555908, 'stddev': 0, 'var': 0, 'mean': 0.8986999988555908},
    'scalar': 'accuracy'}, 'loss': {'result': {'max': 0.3866434097290039, 'median': 0.3866434097290039,
    'min': 0.3866434097290039, 'stddev': 0, 'var': 0, 'mean': 0.3866434097290039}, 'scalar': 'loss'}},
    detail=None)
```

{% hint style="info" %}
Sorting models by accuracy is really easy since these are just python objects
{% endhint %}

