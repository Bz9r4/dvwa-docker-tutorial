# **How to Install DVWA Using Docker on Ubuntu**  

## **Requirements**  
- A Linux-based operating system (Ubuntu recommended)  
- Internet connection  

## **Step 1: Update the System**  
Before installing anything, it's a good practice to update the system:  
```bash
sudo apt update && sudo apt upgrade -y
```

## **Step 2: Install Dependencies**  
Install the necessary certificates to download and install Docker correctly:  
```bash
sudo apt-get install ca-certificates curl
```

## **Step 3: Add the Docker GPG Key**  
Create the required directory and download Docker's GPG key:  
```bash
sudo install -m 0755 -d /etc/apt/keyrings
```
```bash
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```
```bash
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

## **Step 4: Add the Docker Repository**  
Add Docker's official repository to the system's sources list:  
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

## **Step 5: Install Docker**  
Now install Docker and its components:  
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
During installation, press `Y` to confirm the download of the required packages.  

## **Step 6: Test the Docker Installation**  
To ensure Docker was installed correctly, run:  
```bash
sudo docker run hello-world
```
If everything is correct, you will see a message indicating that Docker is working.  

## **Step 7: Start and Enable Docker**  
Enable the Docker service to start automatically with the system:  
```bash
sudo systemctl start docker
```
```bash
sudo systemctl enable docker
```

## **Step 8: Allow Docker Usage Without `sudo`**  
Add your user to the `docker` group to avoid needing `sudo` for every command:  
```bash
sudo usermod -aG docker $USER
```
Restart your session to apply the new permissions.  

## **Step 9: Download and Run DVWA**  
Now that Docker is set up, download the DVWA image:  
```bash
docker pull vulnerables/web-dvwa
```
Run the DVWA container on port 80:  
```bash
docker run -d -p 80:80 vulnerables/web-dvwa
```

## **Step 10: Check if the Container is Running**  
Run the following command to verify that the container is running correctly:  
```bash
docker ps
```

## **Step 11: Access DVWA**  

1. Open your browser and go to `http://YOUR_IPV4`.  
2. On the login screen, simply click **Login** without filling in any fields.  
3. On the setup screen, scroll to the bottom and click **Create/Reset Database**.  
   This button is responsible for:  
   - Creating the initial database structure for DVWA.  
   - Creating the necessary tables to store users, settings, and vulnerability test logs.  
   - Ensuring the environment is ready for use by eliminating any inconsistencies or old data.  
4. The login screen will appear again. Use the following credentials:  
   - **Username:** `admin`  
   - **Password:** `password`  

Now, DVWA is ready to use! 🎉  

---

This guide should help you quickly set up a secure environment for security testing on Ubuntu. 🚀
