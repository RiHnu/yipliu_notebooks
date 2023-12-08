```python
def __init__()
# set manual optimization for multiple optimizers
self.automatic_optimization = False 

def configure_optimizers(self):
    all_params = {k: v for k, v in self.named_parameters()}
    lang_params = {k: v for k, v in all_params.items() if "text_encoder" in k}
    other_params = {k: v for k, v in all_params.items() if "text_encoder" not in k}
    return (
                {
                "optimizer": lang_optimizer,
                "lr_scheduler": {
                    "scheduler": lang_scheduler,
                    "interval": "step",
                    "frequency": 1,
                }},
                {"optimizer": other_optimizer}
                )

```


# 使用手动 optimization + 梯度累计

```python
def training_step(self, batch: Any, batch_idx: int):

    # access your optimizers
    lang_opt, other_opt = self.optimizers() 

    lang_sch = self.lr_schedulers()
    loss, preds, targets = self.model_step(batch)
    self.manual_backward(loss)

    # update your model parameters
    # accumulate gradients of 2 batches

    if (batch_idx + 1) % 2 == 0:
        other_opt.step()
        lang_opt.step()  
        
        # clear the gradients from the previous training step
        other_opt.zero_grad()
        lang_opt.zero_grad()         
        lang_sch.step()

```