# DNS_Server
Use the below commands to run on docker and visual studio:
To create a network:
docker network create dcn_app

To build and run:
docker build -t fs .
docker run -p 9090:9090 --net=dcn_app fs
docker build -t us .
docker run -p 8080:8080 --net=dcn_app us
docker build -t as .
docker run --network dcn_app --name dns_server -p 53533:53533/udp -it as


Once the 3 servers are up and running send a PUT request:
https://reqbin.com/req/curl/xp8cw8vs/put-json-example

{
  "hostname": "fibonacci.com",
  "fs_ip": "172.19.0.2",
  "as_ip": "172.19.0.4",
  "as_port": 53533,
  "ttl": 100
}

Once the PUT request is sent we can verify that the servers are running by :
http://localhost:8080/fibonacci?hostname=%22fibonacci.com%22&fs_port=9090&number=9&as_ip=%22172.19.0.4%22&as_port=53533

Note: IP addresses to be verified in VStudio window and passed accordingly

