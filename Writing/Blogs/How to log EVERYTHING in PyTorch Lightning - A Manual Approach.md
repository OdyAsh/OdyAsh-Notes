
1. explain each method in `HierarchalModelPL(pl.LightningModule)`
2. screenshot of all methods that will be explained
3. In `__init()__` explanation section, refer to [[Nested List and Dict Comprehension - Unravelling Confusing Syntax]]
4. mention how `loss` is returned by `training_step()` to be used later in `outputs` parameter in `training_epoch_end()` method, while other metrics are not returned, as we access them via the `torchmetrics` methods defined in `self.metrics`. Also mention how you must return a key called `loss` in `training_step()`
5. mention a best practice tip to always return values in training_step() as `return {'loss' : loss, ...} `instead of `return loss, ...`
# Source

graduation_project/model_v03_hnn_without_metadata.ipynb, 
`class HierarchalModelPL` cell,
 `__init()__` constructor