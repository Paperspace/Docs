---
description: How to perform inference using a Deployment's TF Serving RESTful API
---

# Deployed Model RESTful APIs

When you specify the default Deployment type via `--deploymentType TFServing`, Gradient deploys your Model using a [TensorFlow ModelServer](https://www.tensorflow.org/tfx/guide/serving). This Deployment comes with a built-in RESTful API.

#### Request and Response Formats

The request and response to/from a Deployment's RESTful API is a JSON object.

The composition of this object depends on the request type or verb.

In case of an error, all API endpoints will return a JSON object in the response body with `error` as the key and the error message as the value:

```text
{
  "error": <error message string>
}
```

### Model Status API <a id="model_status_api"></a>

Returns the status of a model in the ModelServer.

#### URL <a id="url"></a>

```text
GET https://services.paperspace.io/model-serving/your-deployment-id/versions/${MODEL_VERSION}
```

`/versions/${MODEL_VERSION}` is optional. If omitted, status for all versions is returned in the response.

#### Response format <a id="response_format"></a>

If successful, returns a JSON representation of a [`GetModelStatusResponse`](https://github.com/tensorflow/serving/blob/5369880e9143aa00d586ee536c12b04e945a977c/tensorflow_serving/apis/get_model_status.proto#L64) protobuf.

### Model Metadata API <a id="model_metadata_api"></a>

Returns the metadata of a Model in the ModelServer.

#### URL <a id="url_2"></a>

```text
GET https://services.paperspace.io/model-serving/your-deployment-id/versions/${MODEL_VERSION}/metadata
```

`/versions/${MODEL_VERSION}` is optional. If omitted, the Model metadata for the latest version is returned in the response.

#### Response format <a id="response_format_2"></a>

If successful, returns a JSON representation of a [`GetModelMetadataResponse`](https://github.com/tensorflow/serving/blob/5369880e9143aa00d586ee536c12b04e945a977c/tensorflow_serving/apis/get_model_metadata.proto#L23) protobuf.

### Classify and Regress API <a id="classify_and_regress_api"></a>

This API closely follows the `Classify` and `Regress` methods of the [`PredictionService`](https://github.com/tensorflow/serving/blob/5369880e9143aa00d586ee536c12b04e945a977c/tensorflow_serving/apis/prediction_service.proto#L15) gRPC API.

#### URL <a id="url_3"></a>

```text
POST https://services.paperspace.io/model-serving/your-deployment-id/versions/${MODEL_VERSION}:(classify|regress)
```

`/versions/${MODEL_VERSION}` is optional. If omitted, the latest version is used.

#### Request format <a id="request_format"></a>

The request body for the `classify` and `regress` APIs must be a JSON object formatted as follows:

```text
{
  // Optional: serving signature to use.
  // If unspecified, the default serving signature is used.
  "signature_name": <string>,

  // Optional: Common context shared by all examples.
  // Features that appear here MUST NOT appear in examples (below).
  "context": {
    "<feature_name3>": <value>|<list>
    "<feature_name4>": <value>|<list>
  },

  // List of Example objects
  "examples": [
    {
      // Example 1
      "<feature_name1>": <value>|<list>,
      "<feature_name2>": <value>|<list>,
      ...
    },
    {
      // Example 2
      "<feature_name1>": <value>|<list>,
      "<feature_name2>": <value>|<list>,
      ...
    }
    ...
  ]
}
```

`<value>` is a JSON number \(whole or decimal\) or string, and `<list>` is a list of such values. See the [Encoding binary values](https://www.tensorflow.org/tfx/serving/api_rest#encoding_binary_values) section below for details on how to represent a binary \(stream of bytes\) value. This format is similar to gRPC's `ClassificationRequest` and `RegressionRequest` protos. Both versions accept a list of [`Example`](https://github.com/tensorflow/tensorflow/blob/92e6c3e4f5c1cabfda1e61547a6a1b268ef95fa5/tensorflow/core/example/example.proto#L13) objects.

#### Response format <a id="response_format_3"></a>

A `classify` request returns a JSON object in the response body, formatted as follows:

```text
{
  "result": [
    // List of class label/score pairs for first Example (in request)
    [ [<label1>, <score1>], [<label2>, <score2>], ... ],

    // List of class label/score pairs for next Example (in request)
    [ [<label1>, <score1>], [<label2>, <score2>], ... ],
    ...
  ]
}
```

`<label>` is a string \(which can be an empty string `""` if the model does not have a label associated with the score\). `<score>` is a decimal \(floating point\) number.

The `regress` request returns a JSON object in the response body, formatted as follows:

```text
{
  // One regression value for each example in the request in the same order.
  "result": [ <value1>, <value2>, <value3>, ...]
}
```

`<value>` is a decimal number.

Users of gRPC API will notice the similarity of this format with `ClassificationResponse` and `RegressionResponse`protos.

### Predict API <a id="predict_api"></a>

This API closely follows the [`PredictionService.Predict`](https://github.com/tensorflow/serving/blob/5369880e9143aa00d586ee536c12b04e945a977c/tensorflow_serving/apis/prediction_service.proto#L23) gRPC API.

#### URL <a id="url_4"></a>

```text
POST https://services.paperspace.io/model-serving/your-deployment-id/versions/${MODEL_VERSION}:predict
```

`/versions/${MODEL_VERSION}` is optional. If omitted the latest version is used.

#### Request format <a id="request_format_2"></a>

The request body for the `predict` API must be a JSON object formatted as follows:

```text
{
  // (Optional) Serving signature to use.
  // If unspecified, the default serving signature is used.
  "signature_name": <string>,

  // Input Tensors in row ("instances") or columnar ("inputs") format.
  // A request can have either of them but NOT both.
  "instances": <value>|<(nested)list>|<list-of-objects>
  "inputs": <value>|<(nested)list>|<object>
}
```

**Specifying input tensors in row format**

This format is similar to `PredictRequest` proto of gRPC API and the [CMLE predict API](https://cloud.google.com/ml-engine/docs/v1/predict-request). Use this format if all named input tensors have the **same 0-th dimension**. If they don't, use the columnar format described later below.

In the row format, inputs are keyed to the `instances` key in the JSON request.

When there is only one named input, specify the value of the `instances` key to be the value of the input:

```text
{
  // List of 3 scalar tensors.
  "instances": [ "foo", "bar", "baz" ]
}

{
  // List of 2 tensors each of [1, 2] shape
  "instances": [ [[1, 2]], [[3, 4]] ]
}
```

Tensors are expressed naturally in nested notation since there is no need to manually flatten the list.

For multiple named inputs, each item is expected to be an object containing input name/tensor key-value pairs, one for each named input. As an example, the following is a request with two instances, each with a set of three named input tensors:

```text
{
 "instances": [
   {
     "tag": "foo",
     "signal": [1, 2, 3, 4, 5],
     "sensor": [[1, 2], [3, 4]]
   },
   {
     "tag": "bar",
     "signal": [3, 4, 1, 2, 5]],
     "sensor": [[4, 5], [6, 8]]
   }
 ]
}
```

Note, each named input \("tag", "signal", "sensor"\) is implicitly assumed have same 0-th dimension \(_two_ in above example, as there are _two_ objects in the _instances_ list\). If you have named inputs that have different 0-th dimensions, use the columnar format described below.

**Specifying input tensors in column format**

Use this format to specify your input tensors, if individual named inputs do not have the same 0-th dimension or you want a more compact representation. This format is similar to the `inputs` field of the gRPC [`Predict`](https://github.com/tensorflow/serving/blob/a52e8181144a5d6acc96b3d57328c7f49f113ea9/tensorflow_serving/apis/predict.proto#L21) request.

In the columnar format, inputs are keyed to the **inputs** key in the JSON request.

The value for **inputs** key can either a single input tensor or a map of input name/tensors key-value pairs \(listed in their natural nested form\). Each input can have an arbitrary shape and does not need to share the same 0-th dimension \(aka batch size\) as required by the row format described above.

Columnar representation of the previous example is as follows:

```text
{
 "inputs": {
   "tag": ["foo", "bar"],
   "signal": [[1, 2, 3, 4, 5], [3, 4, 1, 2, 5]],
   "sensor": [[[1, 2], [3, 4]], [[4, 5], [6, 8]]]
 }
}
```

Note, **inputs** is a JSON object and _not_ a list like **instances** \(used in the row representation\). Also, all the named inputs are specified together, as opposed to unrolling them into individual rows done in the row format described previously. This makes the representation compact \(but maybe less readable\).

#### Response format <a id="response_format_4"></a>

The `predict` request returns a JSON object in the response body.

A request in [row format](https://www.tensorflow.org/tfx/serving/api_rest#specifying_input_tensors_in_row_format) has a response formatted as follows:

```text
{
  "predictions": <value>|<(nested)list>|<list-of-objects>
}
```

If the output of the model contains only one named tensor, we omit the name and have the `predictions` key map to a list of scalar or list values. If the model outputs multiple named tensors, we output a list of objects instead, similar to the request in the row format mentioned above.

A request in [columnar format](https://www.tensorflow.org/tfx/serving/api_rest#specifying_input_tensors_in_column_format) has a response formatted as follows:

```text
{
  "outputs": <value>|<(nested)list>|<object>
}
```

If the output of the model contains only one named tensor, we omit the name and have the `outputs` key map to a list of scalar or list values. If the model outputs multiple named tensors, we output an object instead. Each key of this object corresponds to a named output tensor. The format is similar to the request in column format mentioned above.

### Example Python REST API Client

Our [mnist-sample repository](https://github.com/Paperspace/mnist-sample) has an example of a REST client that serves as a quick showcase of using a prediction endpoint, reproduced below:

{% embed url="https://github.com/Paperspace/mnist-sample/blob/master/serving\_rest\_client\_test.py" %}

```text
def make_vector(image):
    vector = []
    for item in image.tolist():
        vector.extend(item)
    return vector


def make_prediction_request(image, prediction_url):
    vector = make_vector(image)
    json = {
        "inputs": [vector]
    }
    response = requests.post(prediction_url, json=json)

    print('HTTP Response %s' % response.status_code)
    print(response.text)
```

