# Main references: [Model soups: averaging weights of multiple fine-tuned models improves accuracy without increasing inference time](https://arxiv.org/abs/2203.05482)
## results
- [running results view](result.md)
- [figure result view](figure.png)
## Code

There are 5 steps to reproduced the figure above: 1) downloading the models, 2) evaluating the individual models, 3) running the uniform soup, 4) running the greedy soup, and 5) making the plot.

Note that any of these steps can be skipped, i.e, you can immediately generate the plot above via `python main.py --plot`.
You can also run the greedy soup without evaluating the individual models.
This is because we have already completed all of the steps and saved the results files in this repository (i.e., `individual_model_results.jsonl`).
If you do decide to rerun a step, the corresponding results file or plot is deleted and regenerated.

The exception is step 1, downloading the models. If you wish to run steps 2, 3, or 4 you must first run step 1.

### Install dependencies and downloading datasets

To install the dependencies either run the following code or see [environment.md](environment.md) for more information.
```bash
conda env create -f environment.yml
conda activate model_soups
```

To download the datasets see [datasets.md](datasets.md). When required, set `--data-location` to the `$DATA_LOCATION` used in [datasets.md](datasets.md).
Imagenet is very large, it is recommeneded to use the server repositroy's imagenet, such as autodl.

### Step 1: Downloading the models

```bash
python main.py --download-models --model-location <where models will be stored>
```
This will store models to `--model-location`.


### Step 2: Evaluate individual models

```bash
python main.py --eval-individual-models --data-location <where data is stored> --model-location <where models are stored>
```
Note that this will first delete then rewrite the file `individual_model_results.jsonl`.

### Step 3: Uniform soup

```bash
python main.py --uniform-soup --data-location <where data is stored> --model-location <where models are stored>
```
Note that this will first delete then rewrite the file `uniform_soup_results.jsonl`.

### Step 4. Greedy soup

```bash
python main.py --greedy-soup --data-location <where data is stored> --model-location <where models are stored>
```
Note that this will first delete then rewrite the file `greedy_soup_results.jsonl`.

### Step 5. Plot

```bash
python main.py --plot
```
Note that this will first delete then rewrite the file `figure.png`.

### Note

If you want, you can all steps with:
```bash
python main.py --download-models --eval-individual-models --uniform-soup --greedy-soup --plot --data-location <where data is stored> --model-location <where models are stored>
```

Also note: if you are interested in running ensemble baselines, check out [the ensemble branch](https://github.com/mlfoundations/model-soups/tree/ensemble).

Also note: if you are interested in running a minial example of [wise-ft](https://arxiv.org/abs/2109.01903), you can run `python wise-ft-example.py --download-models`. 

Also note: if you are interested in running minimal examples of zeroshot/fine-tuning, you can run `python zeroshot.py` or `python finetune.py`. See program arguments (i.e., run with `--help`) for more information. Note that these are minimal examples and do not contain rand-aug, mixup, or LP-FT.


