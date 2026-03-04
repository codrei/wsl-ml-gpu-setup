# 🚀 The Ultimate Windows Deep Learning Setup: WSL + VS Code + GPU

Welcome! If you want to build Machine Learning and Deep Learning models, Linux is the industry standard. However, you don't need to wipe your Windows PC to do it.

This guide will teach you how to set up Windows Subsystem for Linux (WSL), connect it to Visual Studio Code, and build a bulletproof, GPU-accelerated Python environment that just works. We will use the modern tensorflow[and-cuda] method to completely bypass the nightmare of manually installing NVIDIA drivers.

-------------------------------------------------------------------------------------------------------------------------------

🛠️ Phase 1: Installing Linux on Windows (WSL)

First, we need to put a full Ubuntu Linux engine inside your Windows machine.

 Open Windows Terminal (or PowerShell) as Administrator.
    - Click your Windows Start menu, type PowerShell, right-click it, and select "Run as administrator".

 Install WSL.
    - Paste this command and press Enter:
      ''' Powershell
      wsl --install
      '''
    - This automatically downloads the necessary Windows features and the latest Ubuntu distribution.

 Restart your Computer.
    - Once it finishes, reboot your PC to lock in the changes.

 Get Ubuntu App on microsoft store
    - Once it finishes, open your Ubuntu app and it will direct you to its terminal.

 Create your Linux User.
    - After installing, a black terminal window will pop up asking you to create a UNIX username and password.
    - Note: When you type your password, nothing will show on the screen. This is a normal Linux security feature. Just type it and hit Enter.

💻 Phase 2: Connecting VS Code to Linux

Now we need to make VS Code act as our window into the Linux engine.

 Download VS Code. (If you haven't already, get it for Windows).

 Install the WSL Extension.
    - Open VS Code, go to the Extensions tab (the squares icon on the left).
    - Search for "WSL" (published by Microsoft) and install it.

 Boot up your Linux Terminal.
    - Open your normal Windows Start Menu, search for Ubuntu, and open it.

 Launch VS Code from Linux.
    - Inside that Ubuntu terminal, make a new project folder, go into it, and open it in VS Code using these three commands, (do it one at a time):
    ''' Bash
    mkdir my_ml_project
    cd my_ml_project
    code .
    ...
    - VS Code will open. Look at the bottom-left corner; it should proudly say WSL: Ubuntu.

🐍 Phase 3: Installing Miniconda (The Environment Manager)
We need a way to build isolated Python "sandboxes" so our libraries don't fight each other. Miniconda is the best tool for this.

 Open the VS Code Terminal.
    - Inside VS Code, press Ctrl + ` (the backtick key) to open the terminal. It should say bash or ubuntu on the right side.

 Download Miniconda.
    - Run this command to download the Linux installer:
    ```Bash
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    ...

 Install Miniconda.
    - Run the installer:
    ```Bash
    bash Miniconda3-latest-Linux-x86_64.sh
    ...
    - Press Enter to scroll through the terms, type yes to accept, and hit Enter to confirm the default installation location.
    - Crucial Step: When it asks if you want to initialize Miniconda, type yes.

 Refresh your Terminal.
    - Close the terminal (click the Trash Can icon) and open a new one (Ctrl + \``). You should now see (base)` at the start of your command line.

🏗️ Phase 4: Building the Ultimate ML Sandbox
This is the secret sauce. Instead of fighting with manual NVIDIA drivers (cuDNN, CUDA toolkits), we use a specific, modern setup that downloads everything automatically.

 Create the Python 3.12 Environment.
    - Why 3.12? It is fast, highly stable, and perfectly compatible with the modern ML ecosystem.
    ```Bash
    conda create -n tf_modern python=3.12 -y
    ...

 Activate the Environment.
    ```Bash
    conda activate tf_modern
    ...

 The "All-In-One" Installation Command.
    - This command installs TensorFlow (along with its built-in NVIDIA GPU bridge), standard data science tools (Pandas, Numpy), advanced tree models (XGBoost, LightGBM), explainability tools (SHAP), and the Jupyter kernel so VS Code can see it.
    ```Bash
    pip install tensorflow[and-cuda] numpy pandas matplotlib seaborn scikit-learn xgboost lightgbm catboost shap lime joblib ipykernel
    ...
    - Grab a coffee, this will take a few minutes!

🧪 Phase 5: Hooking up Jupyter and Verifying the GPU
Let's make sure VS Code is using your new environment and that TensorFlow actually sees your graphics card.

 Install the Jupyter Extension.
    - Go to the VS Code Extensions tab, search for "Jupyter" (published by Microsoft), and install it.

 Create a Notebook.
    - Create a new file in your project called test_gpu.ipynb.

 Select the Kernel.
    - Open the notebook. In the very top-right corner, click Select Kernel -> Python Environments -> select your tf_modern environment.
    - (If you don't see it, press F1, type Developer: Reload Window, and try again).

 Run the Ultimate Test.
    - Paste this exact code into the first cell and click the Play button:
    ```Python
    import tensorflow as tf
    print("Num GPUs Available: ", len(tf.config.list_physical_devices('GPU')))
    print(tf.config.list_physical_devices())
    ...

 Success!
    - If it prints Num GPUs Available: 1, you are completely finished!
    - (Note: If you see red text complaining about a NUMA node, ignore it! That just means you are using a normal desktop processor instead of a server motherboard).

*You are now ready to build world-class AI models on your own PC!* ^^
