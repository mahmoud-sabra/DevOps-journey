### **Create a Custom VPC In us-east-1 Region** 

- CIDR: `10.0.0.0/16`
### **Create an Internet Gateway (IGW)**

- Attach it to the VPC
### **Create a Public Subnet**

- CIDR: `10.0.1.0/24`
### **Create a Route Table & Configure Routing**

- Add a route for `0.0.0.0/0` → IGW
- Associate it with the **public subnet**
### **Create a Security Group (SG) for the Web App**

- Allow **SSH (22)** from  from **anywhere**
- Allow **HTTP (80, 443)** from **anywhere**
- Allow **Port 3000 (custom web app port) from anywhere**
### **Launch an EC2 Instance**

- Use the **public subnet**
- Select **Amazon Linux 2 AMI**
- Assign the **security group**
- Attach a **key pair** for SSH access
- Assign ElasticIP to the Instance

### **Deploy a Simple Web App**
1. **SSH into the instance:**
2. Install **Node.js & GIT**
3. clone the [mahmoud-sabra/test_node](https://github.com/mahmoud-sabra/test_node)
4. Install dependencies and run the app
-----
