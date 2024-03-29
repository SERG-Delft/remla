---
layout: page
title: ML Configuration Management
parent: Material
has_children: true
has_toc: true
---

# {{page.title}}

This page lists the material that is relevant for the *in-class exercises* of the *ML Configuration Management* lecture.
In this tutorial we are going to try ´mllint´ to test best practices, DVC to manage the ML pipeline
and version control artefacts, and we will use pylint to test a common ML scenario.

## Intro Outline

- Initial Project: https://github.com/luiscruz/sms1
    - still needs a ton of refactoring
- Teams of 2
- One team does a demo at the end

## 1. Setup

We will use the basic ML project used in the previous classes. You probably have already set it up, which means you might be able to skip this setup section.

Fork the Github repo <https://github.com/luiscruz/sms1>

{% highlight Batchfile %}
git clone https://github.com/luiscruz/sms1
cd sms1
mkdir output
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
{% endhighlight %}

## 2. mllint

In this tutorial we will use [`mllint`][mllint] to help improve our `sms1` project.

Run `mllint`:

{% highlight Batchfile %}
pip install mllint
mllint run
{% endhighlight %}

Analyse its output and verify what it says about data version control.

## 3. Data pipeline

**1-** Initiate DVC to set up our automated pipeline.

{% highlight Batchfile %}
pip install dvc
dvc init
dvc run -n get_data -d src/get_data.py -o smsspamcollection python src/get_data.py
{% endhighlight %}

Check the output. Make sure you understand why we are getting the error. Fix it based on the suggestion proposed by `dvc`.

In the above command we have added the first stage of the pipeline: `get_data`.
It depends on the script `src/get_data.py` (flag -d) and yields the output `dataset` (flag -o).
In the command above, we specify that the stage `get_data` is executed by running `python src/get_data.py`.

(describe the project and show how to check the scripts to see what are the inputs and outputs)

Check `dvc run` documentation to understand how it works.

**Note:** if you are experiencing any issues with a library called `fsspec` force install version `2022.7.1`:
```
pip uninstall fsspec
pip install fsspec==2022.7.1
```

**2-** Create a new stage, `preprocess`, that will run the script `src/text_preprocessing.py`
<!--dvc run -n preprocess -d smsspamcollection -d src/text_preprocessing.py -o output/preprocessor.joblib -o output/preprocessed_data.joblib python src/text_preprocessing.py
 -->

Use `dvc run` the same way we did in the previous stage. Think about the dependencies (`-d`), the outputs (`-o`), and the python script that it needs to run.

Now check how the pipeline looks like with the following command:

{% highlight Batchfile %}
dvc dag
{% endhighlight %}

You should get a directed acyclic graph (DAG) of all the stages in the pipeline.
You can also generate a DAG of the dependencies of all the artefacts:

{% highlight Batchfile %}
dvc dag --outs
{% endhighlight %}

Also check how the `dcv.yml` file looks like.

**3-** Add the `train` stage that runs the script `src/text_classification.py`:

{% highlight Batchfile %}
python src/text_classification.py
{% endhighlight %}

<!--dvc run -n train -d output/preprocessed_data.joblib -d src/text_classification.py -o output/misclassified_msgs.txt -o output/accuracy_scores.png -o output/model.joblib python src/text_classification.py  -->

### Demo

Someone in the class will be asked to present this part of the tutorial to the whole class.
Show how the pipeline looks like and explain how you have specified it.


## 4. Remotes

Previously, we have seen how to automate the execution of your data pipeline while avoiding to re-run it unnecessarily.

Now, imagine the case in which you changed something and executed the pipeline. If you have more people working in your project, everyone will have to re-run the pipeline to retrieve the same artefacts in their local repo.

To avoid such a waste of time and resources, DVC features the concept of `remote`: a storage that you can use to store your artefacts.

Remotes can live in your local storage (local remotes 🤷‍♂️) or in a cloud storage (e.g., Amazon S3, GDrive, etc.).

### Local Remotes

Set up a local "remote" called `mylocalremote`.

{% highlight Batchfile %}
dvc remote add -d mylocalremote ~/remotedvc
{% endhighlight %}

Check out how the project's config file stores this info:

{% highlight Batchfile %}
cat .dvc/config
{% endhighlight %}

To push all our artefacts to the remote, run the push command:
{% highlight Batchfile %}
dvc repro
dvc push
{% endhighlight %}

Now let's change something and see how the dvc is taking care of our artefacts: lets update the dataset. In the `src/get_data.py` change the URL to the following:
{% highlight python %}
URL = 'https://surfdrive.surf.nl/files/index.php/s/OZRd9BcxhGkxTuy/download' # v2, 2000 datapoints
{% endhighlight %}

Now follow the next 3 steps:

**1-** reproduce the repo

**2-** commit changes to git

**3-** push the changes to the local dvc remote.

Voila. Your new version of the data pipeline is now backed up.

Revert the project to the old commit with the old dataset and reproduce the pipeline.
Explain what happened.

Confirm that the dataset is in fact the old version by checking its size (should be 1000):
{% highlight Batchfile %}
wc smsspamcollection/SMSSpamCollection
{% endhighlight %}


Revert to the head of the branch and check again that dvc took care of retrieving the latest artefacts (dataset should have 2000 data points).


### Cloud Remotes

Instead of having a *remote* stored locally, we can store it using cloud storage. In this example, we will use google drive.
In this step you can have only one teammate setting this up while the others 

To make things clear, start by removing the local remote:

```
dvc remote remove mylocalremote
git commit -am "delete dvc remote 'mylocalremote'"
```

1. Create a folder in your Google drive
    1.1 Share it with your teammate.
    1.2 Copy the folder id from its page url (e.g., `1zUHN-qHKDKvQE8igLPVZ2JMQvrAjyxa`)

2. Follow the instructions in the following documentation page to add a GDrive remote:

https://dvc.org/doc/user-guide/setup-google-drive-remote#url-format

<!-- dvc remote add --default myremote gdrive://11La8oGad0GuB52lHMECxX0yrFZOBZJSz/dvcstore
dvc push -->

3. Change something and see how the dvc is taking care of our artefacts. For example, update the dataset to version v3 by updating `URL` in `src/get_data.py`:

{% highlight python %}
URL = 'https://surfdrive.surf.nl/files/index.php/s/H4e35DvjaX18pTI/download' # v3 3000 datapoints
{% endhighlight %}

4. Rerun the pipeline. Commit **and push** your changes to Github; push them to the dvc remote.

5. Ask your colleagues to `pull` the pipeline (git and dvc) and notice that all the artefacts are there.

## 5. Experiment Management

ML is an experimental process.
Each new experiment needs to be analysed and compare against certain metrics.
Here's how to manage experiments using dvc.

1. You will have to change the training script (`src/text_classification.py`) to output its metrics to a JSON file (could also be YAML).
    - Do a `json.dump` to store the accuracy of the model.
    - It should output a JSON file like the following:
    
```json
{"accuracy": 0.9566666666666667}
```

2. Change the `dvc.yml` file to include the metrics of the stage `train`. Hint: check the docs to see an example of a `dvc.yml` with metrics: https://dvc.org/doc/command-reference/metrics

3. Run the experiment `dvc exp run`

4. See the difference by running `dvc metrics diff`

5. Change something in your project (e.g., change the random state) and run a new experiment.

6. Check the experiment log:

```
$ dvc exp show
┏━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━┓
┃ Experiment              ┃ Created  ┃ accuracy ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━┩
│ workspace               │ -        │ 0.94167  │
│ dvc-tutorial            │ 09:46 AM │ 0.945    │
│ ├── 3f12aef [exp-7f800] │ 09:51 AM │ 0.94167  │
│ └── 8f30720 [exp-44136] │ 09:48 AM │ 0.945    │
└─────────────────────────┴──────────┴──────────┘
```

## 6. Testing with Pylint

Create a test that will test the difference of running two models with 2 different random seeds.
The test should fail if the difference is above 0.1.

You should have a new folder, named tests:

```
.
├── src
│   ├── __init__.py
│   ├── get_data.py
│   ├── read_data.py
│   ├── serve_model.py
│   ├── text_classification.py
│   └── text_preprocessing.py
    └── tests
        ├── __init__.py
        └── test_simple.py
```

**Hint:** You will probably have to import the method `text_classification.main` and change it to accept a parameter with the random seed.

Execute the test by running `pytest`:

{% highlight Batchfile %}
pytest
{% endhighlight %}


## 7. Final Discussion

- What were your main challenges in this tutorial?
- What are the main drawbacks of using DVC for ML projects?

## Datasets

- v1 (1000 datapoints): https://surfdrive.surf.nl/files/index.php/s/WCPP8WJPrtCbUO5/download
- v2 (2000 datapoints): https://surfdrive.surf.nl/files/index.php/s/OZRd9BcxhGkxTuy/download
- v3 (3000 datapoints): https://surfdrive.surf.nl/files/index.php/s/H4e35DvjaX18pTI/download
- v4 (4000 datapoints): https://surfdrive.surf.nl/files/index.php/s/HU5mY29RzxRlHCU/download

[mllint]: https://bvobart.github.io/mllint/