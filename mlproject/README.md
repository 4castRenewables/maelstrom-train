### In juwelsbooster
1. Set python to version 3.9. For this load the following modules:
```
ml --force purge
ml use $OTHERSTAGES
ml Stages/2022
ml GCCcore/.11.2.0
ml Python/3.9.6
```

2. Create a virtual enviroment and activate it:
```
python -m venv <venv-name>
source <venv-name>/bin/activate
```

3. Install ap1 dependencies with pip. The requirements file is in the `env_setup` file
```
pip install -r maelstrom-train/benchmark/requirements_wo_modules.txt
```

### In mantik

Set up a project in Mantik to enable the execution of your experiment. For a step-by-step guide, refer to the quickstart tutorial available [here](https://mantik-ai.gitlab.io/mantik/ui/quickstart.html)


### In your local mlproject

1. Set `PreRunCommand` in `unicore-config-venv.yaml` to the path of your virtual enviroment

<pre><code> PreRunCommand:
    Command: >
      module load Stages/2022 GCCcore/.11.2.0 NCCL/2.11.4-CUDA-11.5 Python/3.9.6;
      source <b>/path/to/&lt;venv-name&gt;</b>/bin/activate;
</code></pre>


2. Run your experiment with mantik
```
mantik runs submit <absolute path to maelstrom-train/mlproject directory> --backend-config unicore-config-venv.yaml --entry-point main --experiment-id <experiment ID> -v
```
