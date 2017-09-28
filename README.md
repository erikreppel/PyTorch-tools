# PyTorch tools

Some tools to help with PyTorch.

## Example

Currently this repo revolves around the `Experiment` class which wraps a PyTorch model with a Keras inspired API.

First, create an instance of a PyTorch model, then wrap the model in an experiement

```
model = Model()
exp = Experiment(model)
```

Note: Experiment supports [Visdom](https://github.com/facebookresearch/visdom)
logging via `Experiment(model, viz_logging=True)`. A visdom server must be running (`python -m visdom.server`)

Then create a `criterion` (loss function) and an `optimizer` and compile the model.

```
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters())

exp.compile(optimizer, criterion)
```

The model can then be fit and evaluated
```
exp.fit(train_loader, n_epoch=10)
exp.evaluate(test_loader)
```

note that `train_loader` and `test_loader` are PyTorch `Dataloader`s

`.fit` also supports validation sets

```
exp.fit(train_loader, n_epoch=10, valid_loader=test_loader, valid_freq=2)
```