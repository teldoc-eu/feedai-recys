FROM nvcr.io/nvidia/merlin/merlin-tensorflow-inference:22.05

RUN pip install tensorflow==2.9.2 protobuf==3.19.6 jupyterlab "feast<0.20" faiss-gpu
RUN pip install cupy-cuda116
RUN pip uninstall -y cupy-cuda115