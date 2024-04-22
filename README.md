# nagios-server-configuration-guide-for-server-monitoring

### Authors (Autores)

| Author                | Origin                               |
| --------------------- | ------------------------------------ |
| Joshua Caffroni       | UniBarranquilla - IUB                |
| Harry Lopez           | UniBarranquilla - IUB                |

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
| <img src="https://img.shields.io/badge/Study%20Status-Design%20Finalized-brightgreen.svg" alt="Study Status: Design Finalized"> | The ongoing study | 

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
	 Instalación (Installation)

		Servidor (Server)
			Item1
			Item2
			Item3 - plugins 
		Clientes (Client)

### Usage (Por qué es importante usarlo)

It's important to use Nagios because it provides real-time visibility into the status of important systems and services, helping to ensure the availability, reliability and optimal performance of the IT infrastructure, thanks to active monitoring of resources and detection of problems. Early on, Nagios helps prevent unplanned outages and helps minimize downtime, thereby improving productivity and user satisfaction.

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
- 
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



- **How do I define the nrpe commands so I can use them?**



5 preguntas y respuestas

### Contacts (Contactos)
- `Joshua Caffroni`
jcaffroni@unibarranquilla.edu.co
- `Harry Lopez`
harrydlopez@unibarranquilla.edu.co

### Acknowledgements (Agradecimientos)
`Nazareno Anselmi`: 
- [Nagios - Install NRPE](https://www.youtube.com/watch?v=7qZv50kweys)
  
`Tecnolitas`: 
- [How to install Nagios on Ubuntu](https://tecnolitas.com/blog/como-instalar-nagios-en-ubuntu-20-04/)
  
`Damiandiazrios82`:  
- [Nagios client configuration](https://rincondelsistema.home.blog/2019/03/17/configuracion-clientes-nagios/)

`Pavel Saavedra`:  
-[Add Host and Services to Nagios monitoring](https://youtu.be/40nUAYv-zQs?si=5dY2NLeJb_zBZGw9)




