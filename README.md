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

Then, for each of the three images, docker run is used to run them in containers. To run these images on your Docker network, use the —network someNetworkName option in the run command. Furthermore, for user server, Fibonacci server, and authoritative server, use ports 8080:8080, 9090:9090, and 53533:53533, respectively.
  
After that, please first register the DNS of your Fibonacci server. You can use some HTTP tools (e.g., Postman on Google Chrome) to send an HTTP PUT message to http://localhost:9090. In this PUT message, please provide JSON object in the right format as below:
  
{
    "hostname": your hostname,
    "ip": your FS IP,
    "as_ip": your AS IP,
    "as_port": "53533"
}
  
In this JSON format, both ip and as ip should represent the IP address of each container within the Docker network you've constructed. To inspect these two IP addresses directly, run docker inspect someNetworkName.
  
Your registration details will then be returned in the HTTP response 201 if the DNS registration was successful. Then, on the user server, test DNS queries and fibonacci number retrieval by going to localhost:8080/fibonacci. Hostname must be appropriately registered on the authoritative server, fs port must be 9090, and as ip and as port must be the IP and port number of the authoritative server in your Docker network. The return message on your page if the URL is right is: (for example, number=11)
  
  
