## 6th sem big data (MongoDB Installation for Ubuntu OS)
### 1. **Download all the .deb Packages**:
* [MongoDB Community](https://repo.mongodb.org/apt/ubuntu/dists/jammy/mongodb-org/8.0/multiverse/binary-amd64/mongodb-org-server_8.0.4_amd64.deb) 
* [MongoDB Shell](https://downloads.mongodb.com/compass/mongodb-mongosh_2.3.8_amd64.deb)
* [MongoDB Compass](https://downloads.mongodb.com/compass/mongodb-compass_1.45.2_amd64.deb)

### 2. **Install MongoDB from the .deb Package**:

Open the terminal and navigate to the *Downloads* folder where the `.deb` file is stored:

```BASH
cd Downloads/
```
* **Use the following command to install the MongoDB Server `.deb` package:**
```BASH
sudo dpkg -i mongodb-org-server_8.0.4_amd64.deb
```
* **Start and Enable MongoDB**
```BASH
sudo systemctl start mongod
```
* **Confirm MongoDB is running by checking the service status:**
```BASH
sudo systemctl status mongod
```
* **Use the following command to install the MongoDB Shell `.deb` package:**
```BASH
sudo dpkg -i mongodb-mongosh_2.3.8_amd64.deb
```
* **You can verify by connecting to MongoDB in the shell:**
```BASH
mongosh
```
* **You can verify the connection to MongoDB in the (test)shell:**

```BASH
show dbs;
```
* **to exit from mongosh use exit command**
```BASH
exit
```
* **Use the following command to install the MongoDB Compass `.deb` package:**

```BASH
sudo dpkg -i mongodb-compass_1.45.2_amd64.deb
```

**Click on show application you will find a icon named MongoDB Compass.** <br>
**Installation process Completed...**
