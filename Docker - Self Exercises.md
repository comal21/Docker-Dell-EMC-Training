### **Scenario 1: Setting Up a Temporary Ubuntu Environment**  
📌 **Goal:** Run an Ubuntu container to test some Linux commands without affecting your system.  

#### **Steps:**  
1. Pull the Ubuntu image:  
   ```sh
   docker pull ubuntu
   ```  
2. Run the container in interactive mode:  
   ```sh
   docker run -it ubuntu bash
   ```  
3. Inside the container, try basic commands like:  
   ```sh
   apt update && apt install -y curl
   exit  # To leave the container
   ```
4. Check if the container is still there:  
   ```sh
   docker ps -a
   ```  
5. Remove the container:  
   ```sh
   docker rm <container_id>
   ```

---

### **Scenario 2: Running a Web Server Using Docker**  
📌 **Goal:** Deploy an **NGINX web server** in a container and access it via a browser.  

#### **Steps:**  
1. Run an NGINX container on port 8080:  
   ```sh
   docker run -d -p 8080:80 nginx
   ```  
2. Check running containers:  
   ```sh
   docker ps
   ```  
3. Open a web browser and visit:  
   ```
   http://localhost:8080
   ```
   You should see the **default NGINX welcome page**.  

4. Stop and remove the container:  
   ```sh
   docker stop <container_id>
   docker rm <container_id>
   ```

---



### **Scenario 3: Checking Logs for a Running Container**  
📌 **Goal:** View logs of an application running inside a container.  

#### **Steps:**  
1. Start an NGINX container:  
   ```sh
   docker run -d --name mywebserver nginx
   ```  
2. View logs:  
   ```sh
   docker logs mywebserver
   ```  
3. Stop and remove the container:  
   ```sh
   docker stop mywebserver
   docker rm mywebserver
   ```

---


