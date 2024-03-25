## Running Application 1 with Mantik CLI
To run this application in juwels-booster with the mantik CLI follow these instructions:

1. Login to juwels-booster via SSH. To access juwels-booster via SSH, please follow the instructions provided in this [tutorial](https://apps.fz-juelich.de/jsc/hps/juwels/access.html#ssh-login)

2. Once you are logged in on juwels-booster, set python to version 3.9. For this load the following modules:
```
ml --force purge
ml use $OTHERSTAGES
ml Stages/2022
ml GCCcore/.11.2.0
ml Python/3.9.6
```

3. Create a virtual environment and activate it:
```
python -m venv <venv-name>
source <venv-name>/bin/activate
```

4. Install ap1 dependencies with pip. The requirements file is in the `env_setup` file
```
pip install -r maelstrom-train/benchmark/requirements_wo_modules.txt
```

5. The results will be logged to an Experiment on the MLflow tracking server on Mantik. Set up a project in Mantik and create a new Experiment. Note its experiment Id, which will be needed in the submission command. For a step-by-step guide, refer to the Quickstart tutorial available [here](https://mantik-ai.gitlab.io/mantik/ui/quickstart.html).

6. Update the `unicore-config-venv.yaml` file by specifying the `PreRunCommandOnComputeNode` with the path to your virtual environment.

<pre><code> PreRunCommandOnComputeNode: >
      module load Stages/2022 GCCcore/.11.2.0 NCCL/2.11.4-CUDA-11.5 Python/3.9.6;
      source <b>/path/to/&lt;venv-name&gt;</b>/bin/activate;
</code></pre>


7. Run your experiment with mantik
```
mantik runs submit <absolute path to maelstrom-train/mlproject directory> --backend-config unicore-config-venv.yaml --entry-point main --experiment-id <experiment ID> -v
```
