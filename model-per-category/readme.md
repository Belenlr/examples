# Modeling and prediction per category

These scripts allow selecting the field to be used as the first split
(or *root split*) when modeling and predicting with any supervised
algorithm in BigML.

With the [create-category-models script](create-category-models),
given an input dataset and one of its categorical fields, you'll
generate a collection of predictive models based on the input data,
each one corresponding to a subtree of the root node, which is set as
the first split by the caller (instead of letting the modeling
algorithm find it by itself).  The number of subtrees can be either
one per category if the root node is branching into as many children
as there are categories, or just two, if the root node is just a
binary node as in BigML trees.  The user can select which of the two
behaviours she prefers via the boolean input parameter `binary-split`.

To make predictions for new instances using those models, you can use
accompanying scripts [single-prediction](single-prediction)
and [batch-prediction](batch-prediction).  Both take as one of their
inputs the identifier of the execution that created the models (that
is, an execution of [create-category-models](create-category-models)),
and either a single instance or an input dataset to perform either a
single prediction or a batch prediction using the category models.

Predictions are made by selecting the appropriate model, according to
the category of the input instances.  In oder words, the split on the
root node is performed first *by hand*, dispatching then to the
adequate submodel to finish the prediction.

## How to install

### Using bigmler

If you have bigmler installed in your system, just checkout this
repository and, at its top level, issue the command:

        make compile PKG_DIR=model-per-category

That will create for you all three scripts.

### Using the web UI

- Install the `create-category-models` script, using
  [this url](./create-category-models).
- Install [single-prediction](./single-prediction) to be able to make
  single predictions given an execution of `create-category-models`.
- Install [batch-prediction](./batch-prediction) to be able to create
  batch predictions given an execution of `create-category-models`.
