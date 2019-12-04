# AWS_Jupyter_Notebook
instructions to install jupyter notebook on an instance and manage different virtual environments

## step1: launch a EC2 instance
  - in your VPC, public Subnet
  - Launch instance (ubuntu server 18)
  	- Name: Jupyter_instance
	- Accessible through VPC
	
## step2: connect to instance
  - use ssh from windows command line
  - Check python
  ```
  sudo apt-get upgrade
  sudo apt-get update
  python3.6
  ```
  - dont install python if it is already installed!!!, (in case you need: ```sudo apt-get install python3.6```)
  - to test, you can run a simple python script
  - type a script in text file and save it with ".py" extension (for example: script_python.py)
  - load the script into your Jupyter_instance with WinSCP or scp line
  	```C:\Users\jeanm\Documents>scp -i "JM_Keypair.pem" "script_python.py" ubuntu@107.23.70.185:/home/ubuntu/script_python.py```
  -launch the script
    ```python3 "script_python.py"```

## step3: install Jupyter notebook
  - first: Install pip on the EC2 instance
  ```sudo apt install python3-pip```
  - if needed, you can look at: <https://linuxize.com/post/how-to-install-pip-on-ubuntu-18.04/> 
  - check the version of pip
  ```pip3 --version```
  - Install Jupyter
  ```Pip3 install jupyter```
  - note:this is not a good idea to install Jupyter into a virtual env. But in case your are interested, you can look at :<https://www.digitalocean.com/community/tutorials/how-to-set-up-jupyter-notebook-with-python-3-on-ubuntu-18-04> 

## step4: connect to Jupyter
  - launch Jupyter
  ```jupyter notebook --ip=0.0.0.0```
  - note: the "--ip=0.0.0.0" command allows that the jupyter server considers your local machine ip as the "localhost"
  - note2: if it does not work, disconnect from your EC2 instance and connect again (this will refresh recent installations)
  - Connect to jupyter from your physical local instance, in your internet browser
  ```<your_ip>:8888```
  - note: please ensure that in your security group instance, the TCP protocol at port 8888 from your IP is allowed (it can also be allowed from any IP)
  - the server will ask you for a token: please enter the token provided when launching the jupyter notebook on your EC2 instance (copy and paste)
  - once token is in, you are in your Jupyter notebook server! ENJOY!!!

A jupyter notebook server is a great tool to transfer files and you can continue working using the terminal console
  
## step6: How to keep the server alive when EC2 is shut down?
  -  "nohup" is the command line
  ```Nohup jupyter notebook ip=0.0.0.0 &```
  - to see what happens behind the scene (to get the token for example)
  ```Cat nohup.out```
  - To stop the nohup
  ```Kill <your process number>```
  - note: for more info about nohup: https://www.journaldev.com/27875/nohup-command-in-linux
  
## step7: manage environments in jupyter notebook
the interest of managing environments is to navigate around the 2 main defaults of python: the non compatibility of packages and the number of versions (2.6 3.6 3.7 etc...)

  - Use conda or pew or virtual env
  	- Conda: https://www.digitalocean.com/community/tutorials/how-to-install-anaconda-on-ubuntu-18-04-quickstart
	- Conda allows you to create env with different versions of python
	- Pew only allows you to create env with SAME version of python
	```Pip3 install pew```
	- Create a new env with pew (for example "genial_env_1")
	```Pew new genial_env_1```

- How to connect the virtual environment to your jupyter notebook: have ipykernel installed in your environment (here = genial_env_1)
	```Pip3 install ipykernel```
    	```python3 -m ipykernel install --user --name=genial_env_1```
- refresh the jupyter notebook with the refresh comman of your browser

- Install packages in your <genial_ev_1> environment (pandas for example):
```Pip3 install pandas```
	
- Copy the environment configuration into a txt
```Pip3 freeze > genial_env_1_config.txt```
	
- create another new environment and copy the existing saved configurations by running the hereunder command:
```Pip3 install -r genial_env_1_configt.txt```
    
You are now ready to enjoy distance working with jupyter notebook !!! HAVE great FUN!
