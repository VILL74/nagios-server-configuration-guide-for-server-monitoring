# nagios-server-configuration-guide-for-server-monitoring

### Authors (Autores)

| Author                | Origin                               |
| --------------------- | ------------------------------------ |
| Joshua Caffroni Pacheco       | UniBarranquilla - IUB                |
| Harry Lopez Garcia           | UniBarranquilla - IUB                |

### Abstract (Resumen)
In this document you can find how to configure a Nagios server to monitor servers, Nagios is an open source monitoring tool that is used to monitor IT (Information Technology) infrastructures, including servers, networks, applications and services, thanks to this Allows system administrators to actively detect and resolve problems before they affect end users. A real-world monitoring environment was set up using the Oracle VM VirtualBox application by creating virtual machines to monitor a server.

### Screenshots (Pantallazos)

- `Host List`
  
![2](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/91bde8bc-c5a9-4bcd-8ede-d46be35ecea1)

- `This panel shows the list of services that are being monitored with their statuses`
  
![1](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/aff2aae3-944b-41a6-a766-0e905e62ca58)




### TOOLS TIC'S (Herramientas TIC'S)
- `Virtual box`
- `Ubuntu Server`
- `WinScp`
- `Putty`


### Status (Estado del trabajo)

| Status            | Description                          |
| ----------------- | ------------------------------------ |
| <img src="https://img.shields.io/badge/Study%20Status-Design%20Finalized-brightgreen.svg" alt="Study Status: Design Finalized"> | The study was finished | 

### Keyworks (Palabras claves)

- `Server`
- `Nagios`
- `Ubuntu`
- `Monitoring`
- `Plugins`
- `Service`
- `Firewall`
- `Docker`
- `NGINX`

### Roadmap (Hoja de ruta)

	 Pre-requisitos (Pre-Requisites)
         - Linux: Basic knowledge of Linux command line operations and processes such as editing and creating configuration files and restarting services, Linux shell 
         scripts as well as its basic commands.
         - networks: basic knowledge such as IP addresses, ports, network protocols (TCP/IP, UDP) and firewall configuration.
         - docker: Basic knowledge such as installing and creating containers, killing and stopping processes in containers.

	 Instalación (Installation)
         - VirtualBox
         - Linux Ubuntu (Ubuntu server)
         - Docker
	 - Nginx + test page
		Servidor (Server)
                        - Nagios 
			- Plugins Nagios
		Clientes (Client)
                        - Sftp
			- Docker
                        - Nginx + test page
   
  
### How to install nagios

Disclaimer: before starting, keep in mind that two instances of Ubuntu Server were used to do this since this research was done for educational purposes.

- `Step 1 (this step must be done in both instances)`

Activation of ports and firewall: before starting with this you must make sure that port 80 and port 5666 are active, for this you can use the command

`sudo ufw status`

The command will show you the status of the firewall, whether activated or deactivated, and the ports that are activated at that moment.

`disabled`

![image](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/3c3e9229-1577-4609-9be4-f96e82807d80)

If your firewall is disabled, you can activate it with the command

`sudo uwf enable`

Enabled (no ports)

![image](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/cd7943a2-6275-41fe-84cc-a910ff676c40)

For activation of posts you can use the following commands to activate ports 22, 80, 5666

`Sudo ufw allow 22`

`Sudo ufw allow 80`

`Sudo ufw allow 5666`

![image](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/946b407a-598f-4a5f-8f8e-7f1d9c5a1594)

- `Step 2`

In the first instance, the installation of NAGIOS and the NRPE agent must be carried out on the server. For both cases, the following links are available.

NAGIOS installation

**Note:** the first two commands in step 1 can sometimes generate an error if you are sure that all package lists are up to date on your server or you are comfortable with a specific version or you just don't want to take the risk, ignore that step and continue from step 2

- [How to install Nagios on Ubuntu](https://tecnolitas.com/blog/como-instalar-nagios-en-ubuntu-20-04/)

**Installation of the NRPE agent on the server**

[Nagios - Install NRPE](https://www.youtube.com/watch?v=7qZv50kweys)

### Usage (Por qué es importante usarlo)

It's important to use Nagios because it provides real-time visibility into the status of important systems and services, helping to ensure the availability, reliability and optimal performance of the IT infrastructure, thanks to active monitoring of resources and detection of problems. Early on, Nagios helps prevent unplanned outages and helps minimize downtime, thereby improving productivity and user satisfaction.

- **In the second instance, a container was created with nginx in Docker**

- **step 1 docker installation**

1. Login with super user
   
`sudo su`

2. Download .sh to install Docker on the operating system

`curl -fsSL https://get.docker.com -o get-docker.sh`

![image](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/42ca7dae-9f34-469c-9ba8-23cae81738c2)

3. Install Docker on the operating system

`sh get-docker.sh`	

![image](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/fb3676d6-641d-4c76-8855-d1921e45b726)

4. View the installation version

`docker –v`

![image](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/18a6e740-1283-4cf8-875f-cee1e345c3e5)

5. Try Hello – World of Docker

`docker run hello-world`

![image](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/e67a573d-daa8-4a8c-a057-ad11db8e525e)

- **Step 2 NGIX installation**

To install NGIX we must have something to display and for this we will use a test page loaded into the server through sftp which was configured using the following link

- [Nginx server file and test page](https://howtoforge.es/como-instalar-y-utilizar-sftp-en-servidores-linux/)

- [How to install and use SFTP on Linux servers](https://howtoforge.es/como-instalar-y-utilizar-sftp-en-servidores-linux/)

Once this is done you can use different tools, in this case I used winscp
- [Install Winscp](https://winscp.net/eng/download.php)

Once this is done you can follow the following steps

- 1.Locate inside the Docker folder that was loaded by SMTP
- 2. Go to the nginx folder
- 3. Create the image via a DockerFile
  
`docker build -t img_dk_nginx .`

- 4. Run Nginx server in container without a volume
- 5. docker run -d -p 4200:80 -v $PWD/plantilla:/usr/share/nginx/html --name container_nginx_4200 img_dk_nginx

**Note:** if port 4200 is busy on your server, you only have to change it in the command which is in the part of the command that says “4200:80” you just have to change 4200 to the desired port.

Once this is done, you can verify its operation by entering the IP of your server followed by port 4200 in your trusted search engine.

**step 3 NRPE agent inhalation**

- [Nagios client configuration](https://rincondelsistema.home.blog/2019/03/17/configuracion-clientes-nagios/)

**Step 4 add host and services to NAGIOS monitoring**

- [Add Host and Services to Nagios monitoring](https://youtu.be/40nUAYv-zQs?si=5dY2NLeJb_zBZGw9)

### FAQ (Preguntas y respuestas)

- **Does a port have to be enabled for the Nagios server to serve?**
  
Yes, port 5666 must be enabled on the Nagios server and the client server. You should also keep in mind that if you use sftp to transfer files to a server, you must also enable port 22 and allow TCP traffic.

`step by step on how to enable a port on the ubuntu server firewall:`

`1.ufw status:`
  
This command shows you the current status of the firewall. It provides an overview of which rules are applied and which connections are allowed or blocked.

`2.ufw enable:`

This command activates the UFW (Uncomplicated Firewall) if it's not already enabled. UFW is a simplified user interface for managing iptables, the Linux firewall. Enabling UFW doesn't imply that it's already blocking or allowing any traffic; it simply enables the firewall functionality.

 `3.ufw allow 5666:`
 
This command adds a rule to the UFW firewall that allows traffic through port 5666. Nagios, a monitoring system, commonly uses port 5666 for communication between the Nagios server and clients. Allowing traffic on this port is essential for Nagios to work properly. The allow option indicates that the traffic is allowed and 5666 specifies the port, you must take into account enabling port 5666 on the client machine and on the nagios server so that they can communicate correctly


- **How to activate port 22 to use SFTP to transfer files?**

`step by step on how to enable port 22 in ubuntu server firewall:`

`1.ufw status:`
  
This command shows you the current status of the firewall. It provides an overview of which rules are applied and which connections are allowed or blocked.

`2.ufw enable:`

This command activates the UFW (Uncomplicated Firewall) if it's not already enabled. UFW is a simplified user interface for managing iptables, the Linux firewall. Enabling UFW doesn't imply that it's already blocking or allowing any traffic; it simply enables the firewall functionality.

`3.ufw allow 22:`

This command adds a rule to the UFW firewall that allows traffic through port 22. Port 22 is the default port for SSH (Secure Shell), which is a protocol for securely accessing a remote system. Allowing traffic on this port is useful if you need to access the system remotely via SSH. The allow option indicates that traffic is allowed, and 22 specifies the port.

`4.ufw allow 22/tcp:`

This command is similar to the previous one but explicitly specifies the TCP protocol. Although most applications using port 22 use TCP, this command ensures that only TCP traffic on port 22 is allowed and not any other protocol like UDP. TCP is a reliable, connection-oriented communication protocol commonly used for data transfers requiring delivery assurance, such as SSH.

- `photo result of activating ports`

![allow firewall](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/820df265-3c1b-48fd-a29d-704f4446badd)


- **How do I define a service to monitor?**

`1.locate us in the file to define the services to use:`

We must have administrator permissions to avoid problems and we enter the following path /usr/local/nagios/etc/servers using the following command:

`cd /usr/local/nagios/etc/servers`

`2. open configuration file to define nagios services`

once located we give ls to find the file called client.cfg and we use nano client.cfg to be able to edit the file

-`photo of how to apply the commands`

![1 definir servicio e](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/615308b3-41aa-44d7-bd35-ef4cd87fa404)

-`structure of how to define a service`

![2 definir servicio](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/b88ed09b-26da-4cb8-865c-759b4b54558e)

![3 definir servicio](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/d3bd5be6-9040-4043-9eb0-18c39e492f69)

`3. go and edit commands.cfg file`

- `It must be taken into account that the services that were defined are those that are by default in the commands.cfg file`

To locate ourselves in the commands.cfg file we go to the following path /usr/local/nagios/etc/objects with the command cd, then we give ls and finally nano commands.cfg

-`photo of how to apply the commands`

![1commands](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/430facc2-316d-4286-be08-78c238cd3c20)

-`structure of how it is defined in the commands file`

![2commands](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/6260d109-6222-41b4-b579-d7c28e81ed95)


- **How to connect the client server and the nagios server?**
  
`1.locate us in the file to define the services to use:`

We must have administrator permissions to avoid problems and we enter the following path /usr/local/nagios/etc/servers using the following command:

`cd /usr/local/nagios/etc/servers`

`2. open configuration file to define nagios services`

once located we give ls to find the file called client.cfg and we use nano client.cfg to be able to edit the file

-`photo of how to apply the commands`

![1 definir servicio e](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/615308b3-41aa-44d7-bd35-ef4cd87fa404)

-`structure of how to define a service`

In the first part of the file you see a defined service, this is the client server, the only thing we must change is the host name (it is the host name that we are going to assign), the alias (which is the description) and finally address (there they will place the IP of the client server)

![2 definir servicio](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/b88ed09b-26da-4cb8-865c-759b4b54558e)

`3. On the client server`

On the client server we go to the nrpe.cfg file, we open the file with the command nano /etc/nagios/nrpe.cfg

-`photo of how to apply the commands`

![1conectar servidor cliente](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/ede276de-12bc-4dae-8294-2dc252ebfc99)

-`In this line we place the IP of our Nagios server after the comma`

![conectar servidor cliente](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/cc57b7b3-3074-40fd-9bcd-c3f3111dfefd)

-`we can find port 5666 of Nagios already defined` 

![2 conectar servidor cliente](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/fe1ed57e-c550-4c1a-9ef0-15770b301748)


-`restart client server and nagios` 

`restart Nagios server`

 sudo service nagios restart

`restart client server`

sudo /etc/init.d/nagios-nrpe-server restart

Once this is done you must restart both servers.

- **How do I define the nrpe commands so I can use them?**

`1. go and edit commands.cfg file`

- `It must be taken into account that the services that were defined are those that are by default in the commands.cfg file`

To locate ourselves in the commands.cfg file we go to the following path /usr/local/nagios/etc/objects with the command cd, then we give ls and finally nano commands.cfg

-`photo of how to apply the commands`

![1commands](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/430facc2-316d-4286-be08-78c238cd3c20)

`2.edit file`

At the last part of the file you are going to place the following line

![definir nrpe comando solo](https://github.com/VILL74/nagios-server-configuration-guide-for-server-monitoring/assets/87573078/535a86eb-7c5d-4547-ba81-35ae2399220c)

### Contacts (Contactos)
- `Joshua Caffroni`

jcaffroni@unibarranquilla.edu.co

- `Harry Lopez`
  
harrydlopez@unibarranquilla.edu.co

### Acknowledgements (Agradecimientos)

`HowtoForge - Tutoriales de Linux`:
-[How to install and use SFTP on Linux servers](https://howtoforge.es/como-instalar-y-utilizar-sftp-en-servidores-linux/)

`Nazareno Anselmi`: 
- [Nagios - Install NRPE](https://www.youtube.com/watch?v=7qZv50kweys)
  
`Tecnolitas`: 
- [How to install Nagios on Ubuntu](https://tecnolitas.com/blog/como-instalar-nagios-en-ubuntu-20-04/)
  
`Damiandiazrios82`:  
- [Nagios client configuration](https://rincondelsistema.home.blog/2019/03/17/configuracion-clientes-nagios/)

`Pavel Saavedra`:  
-[Add Host and Services to Nagios monitoring](https://youtu.be/40nUAYv-zQs?si=5dY2NLeJb_zBZGw9)




