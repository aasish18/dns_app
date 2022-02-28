# dns_app
This is the DNS server application for DCN Lab 3. Below are some instructions to run this app.

# Project Description
The US, FS, and AS folders make up this program. A.py file with the source code and a Dockerfile to compile the source code into Docker are included in each folder.

The authoritative server is represented by AS. It processes DNS registration and DNS query requests from the fibonacci server and the user server, respectively. UDP Socket receives requests; for receiving and sending answers (port 53533 is recommended).

The Fibonacci server is represented by the letter FS. It's a basic HTTP web server that runs on port 9090 and has two paths: /register and /fibonacci. After receiving an HTTP PUT message, the path /register utilizes the message body to register DNS on the authoritative server. The path /fibonacci accepts a number in the form /fibonacci?number=some value> and returns the Fibonacci number F(some value).

The user server is represented by the letter US. It's a basic HTTP web server that runs on port 8080. Five parameters should be given under the route /fibonacci:

/fibonacci?hostname=<hName>&fs_port=<fsPort>&number=<some_value>&as_ip=<asIP>&as_port=<asPort>
  
hName and fsPort are the Fibonacci server's host name and port number, whereas asIP and asPort are the authoritative server's IP address and port. If the DNS query of hName on the authoritative server successfully retrieves the Fibonacci server's IP address, some value will be given to the route /fibonacci on Fibonacci server.

  
# How to build & deploy
  
Under each of the 3 folders US, AS, and FS, please use command:
  
docker build -t path .
 
please build a Docker network using:
  
docker network create someNetworkName
