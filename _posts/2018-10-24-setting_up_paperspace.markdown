---
layout: single
title:  "Setting up Paperspace for FAST.AI"
date:   2018-10-24
---

### 1. Installed Ubuntu 16 as OS 
> You can install fast.ai template as well which will save you from step 2

- I chose P4000 as the machine, 50GB storage and public IP.

### 2. To install fast.ai setup

- After you start the remote machine, you will be provided with the open terminal.

> The recommended setup using <br/>`curl http://files.fast.ai/setup/paperspace | bash`<br/> in the terminal didn't
work for me and was showing error in line `rm /etc/apt/apt.conf.d/` and so I had to follow the below 3 steps.<br/>
If it works for you, then you can ignore the below points under this section.


- Download the below setup script from that terminal

        curl http://files.fast.ai/setup/paperspace  > fastai-setup.sh

> If you `ls`, you will see it in the current directory

- Edit the file ***fastai-setup.sh*** and remove line ***“sudo rm /etc/apt/apt.conf.d/.”***

- Save the file and run the below commands one by one:

        chmod +x fastai-setup.sh
        ./fastai-setup.sh

> It'll take 30-40 minutes to download the fast.ai resources and programs for the course.<br/>
After that you can see all the folders using the command `ls`. It'll show folders such as <br/>
anaconda3/     &emsp;&emsp; data/&emsp;&emsp;    downloads/&emsp;&emsp;    fastai/ 

### 3. To change Paperspace password

- In remote terminal type:

        passwd
- To change sudo password type:

        sudo passwd

### 4. Update repo (time to time)

        cd fastai
        git pull

### 5. Update conda (time to time)
        conda env update

### 6. Run jupyter notebook

- The updated jupyter notebook breaks if you normally run ‘jupyter notebook’ in a terminal. To fix this, overwrite the file using the below command
        
        jupyter notebook --generate-config

> Type `y` to overwrite

- Run the below command from your remote terminal:

        jupyter notebook --no-browser --port=8889 --NotebookApp.allow_remote_access=True

- Now, go to your ***LOCAL TERMINAL*** and run 

        ssh -N -L localhost:8888:localhost:8889 paperspace@your.public.ip.here

> You'll have to provide your paperspace password after which you can copy paste the notebook URL in your browser and change the port from 8889 to 8888 which should load the notebook correctly.

### 7. Permanent solution to run notebook from local terminal and without paperspace password

> In order to save time in paperspace authentication (every time you start the machine) and using step 6 to open notebook from local browser, you can run the below commands in your ***LOCAL TERMINAL***.

- Run the below three commands one by one:

        brew install ssh-copy-id
        cd ~/.ssh
        ssh-copy-id -i ~/.ssh/id_rsa.pub paperspace@your.public.ip.here

- Create a config file:
        
        nano config

> Make sure you are in ssh directory when you create a config file

- Add below contents (replace `your.public.ip.here` with actual IP from paperspace) to the config file:

        Host paperspace
            HostName your.public.ip.here
            IdentityFile ~/.ssh/id_rsa
            # StrictHostKeyChecking no  
            User paperspace
            LocalForward 8888 localhost:8888

- Save nano file
        
        ctrl o
        Enter

- Exit nano file

        ctrl x

- SSH into paperspace from your local terminal
        
        ssh paperspace

- Run jupyter notebook

        cd fastai
        jupyter notebook

> Copy paster the URL and voila!!<br/>
Next time you just need to turn on your remote server in Paperspace and then go to your local terminal and type `ssh paperspace`, and use your `jupyter notebook` from there.













