Grpc for Cisco IOS-XR in python
--
Author: Karthik Kumaravel

Contact: kkumara3@cisco.com

This is a small repo showing how to use GRPC in python for the IOS-XR end node.The repo is consisted of three main componenets, the compiled pb2 file from the IDL, a python client accessing the pb2 file, and an example python file. The example is a small python file showing how to set up the connection and use one of the rpc calls. Please look at the unit-testing and client page for more rpc calls. At the bottom of the repo, there is a walkthrough of how to create your own client. 

If you find any problems with this repo, please file a bug so I can fix it. If you need help, feel free to contact me. 


GRPC Calls
--
The file is called example_grpc.py. This file has an excamples of the different rpc calls. This configuration shows how to get things started with self signed certs.

- Download the repository
- Install grpc

```
pip install grpcio
```
(sudo may be required)
- ssh into the router and turn on grpc and tls on the router, below is an example configuration.

```
interface GigabitEthernet 0/0/0/0
 ipv4 address 192.168.1.2 255.255.255.0
 no shut

grpc
 tls
 port 57777
 !
!
```

- Copy the autogenerated .pem file to the 'keys' folder in the client directory.

```
scp cisco@192.168.1.2:/misc/config/grpc/ems.pem ./
```

(note if you don't want to use TLS, don't pass the cred and options)

- If you are using your own box, change the parameters in the example.py file to have the proper authentication credentials.
- Run the program

```
python grpc_example.py
```
For a more in-depth look, check out the wiki https://github.com/cisco-grpc-connection-libs/ios-xr-grpc-python/wiki

Getting here from the beginning
--
To create a client of your own there are a few steps to follow.

- Download the proto file for IOS-XR's grpc: https://github.com/CiscoDevNet/grpc-getting-started
- Follow the instructions to generate the client/server code in python using the grpc-getting-started's proto file: http://www.grpc.io/docs/tutorials/basic/python.html#generating-client-and-server-code
- From here create a client, an example can be found here: http://www.grpc.io/docs/tutorials/basic/python.html#creating-the-client
 -  At this point you should have a client similar to the one in this repo

Other Useful Links
--
If you would like to test this all out with IOS-XRv, use the following link to request access to the vagrant box.

https://xrdocs.github.io/

To be done
--
Here is a list of current work to be done
- Add example vagrant setup
- Examples of all the different tests
- More unit testing
- Documentation around MDT telemetry
