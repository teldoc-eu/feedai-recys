Based on `nvcr.io/nvidia/merlin/merlin-tensorflow-inference:22.05`

# Preparing & running `nvcr.io/nvidia/merlin/merlin-tensorflow-inference:22.05`

The NVidia example doesn't work out-of the box!

```shell
docker run -it --gpus all -p 8000:8000 -p 8001:8001 -p 8002:8002 -p 8888:8888 -v /home/michal/dev/recsys/merlin-examples-data:/workspace/data/ --ipc=host nvcr.io/nvidia/merlin/merlin-tensorflow-inference:22.05 /bin/bash
```

## Installing proper libraries (inside container)

```shell
pip install jupyterlab
pip install tensorflow==2.9.2 "feast<0.20" faiss-gpu
pip install protobuf==3.19.6
pip install cupy-cuda116
pip uninstall cupy-cuda115
```

## Running infrastructure (inside container)

```shell
jupyter-lab --allow-root --ip='0.0.0.0' --NotebookApp.token='lolo' &
tritonserver --model-repository=/Merlin/examples/Building-and-deploying-multi-stage-RecSys/poc_ensemble/ --backend-config=tensorflow,version=2
```

# Using dedicated Dockerfile

Use `Build & attach recsys image` Intellij run configuration, this will prepare the correct Docker image and run & attach the container.

Then in attached console:

```shell
cd /
jupyter-lab --allow-root --ip='0.0.0.0' --NotebookApp.token='lolo' &
tritonserver --model-repository=/Merlin/examples/Building-and-deploying-multi-stage-RecSys/poc_ensemble/ --backend-config=tensorflow,version=2
```

# Backup

```shell
rsync -arvhp --progress --whole-file --no-compress /home/michal/dev/recsys michal@nas:BACKUPS/rsync/p620/
```

# Solved problems 

- to run notebooks `pip install cupy-cuda11x`
- but to run Triton had to uninstall it `pip uninstall cupy-cuda11x`


