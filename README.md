What worked?

1. Create virtual environment using packages available in HPC (I am using Stanford cluster which uses linux-64) and activate the environment.

$ python -m venv /home/groups/....
$ source /home/groups/.../pytorch-gpu/bin/activate

*Package examples:

pip install --upgrade pip
pip install numpy matplotlib tqdm ipykernel
pip install ipython
pip install jupyter
pip install pyzmq
pip install notebook

2. Load pytorch from the HPC itself. I tried using pytorch channel to install cuda-enabled pytorch, but it DID NOT work for my HPC.
   I also tried making my own conda environmen and installing pytorch with CUDA, but it did not work in the HPC. So I used pytorch available in the HPC.

# Load modules required for PyTorch
$ module purge
$ module load math
$ module load py-pytorch/2.4.1_py312

# Activate your venv (adjust path if needed)
$ source /home/groups/.../pytorch-gpu/bin/activate

# OPTIONAL: Set TMPDIR if you had issues before
$ export TMPDIR=/home/groups/.../tmp

3. Confirm if required pytorch is installed:

python -c "import torch; print(torch.__version__, torch.cuda.is_available())"

4. Register jupyter kernel (One-time)

$ python -m ipykernel install --user --name pytorch-gpu --display-name "PyTorch GPU (venv)"

5. Actiacte jupyter notebook in terminal and copy URL to the VS code text editor of HPC. Then use PyTorch GPU as the kernel.

$ jupyter notebook


** Extra tips:
1. If memory is exceeded, then you can do this to access memory of the group.
$ mkdir -p /home/groups/....
$ python -m venv /home/groups/....
$ source /home/groups/.../pytorch-gpu/bin/activate


2. You can also make a tmp folder, if your space is not enough even for the temporary installation files.

$ mkdir -p /home/groups/.../tmp
$ export TMPDIR=/home/groups/.../tmp

  * For permanently making it as tmp folder, do this:
$ echo 'export TMPDIR=/home/groups/.../tmp' >> ~/.bashrc
