# you need to make sure that you have no process/service running on ports 67/udp, 69/udp and 8000/tcp

docker build -t dhcp dhcp
docker build -t tftp tftp
docker build -t simplehttpd httpd

docker run -p 67:67/udp --net=host -t dhcp &
docker run -p 69:69/udp --net=host -v /var/lib/tftpboot:/var/lib/tftpboot -t tftp &
docker run -p 8000:8000/tcp --net=host -t simplehttp &

# you need to change the IP of your network interface to 192.168.1.2
#   ip 192.168.1.2 netmask 255.255.255.0 gateway 192.168.1.1
# now you should boot your PXE target and ESXi should get installed automagically :)

# if something goes wrong you can use tcpdump to see any problems

