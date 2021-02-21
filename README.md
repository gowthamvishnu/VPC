# VPC-virtual private cloud
1)create a vpc
  a) nametag:
  b)ICDR:10.200.0.0./16 then create.
  
2)Next thing we want to do is associate this vpc with the internet gateway then vpc can talk to the internet.
  a)create Intenetgateway
  b)attach thids IGW to the internet gateway.
  
3)Then create two subnets one private and one private.go to the subnet and create subnets under our VPC.one public and one private

  a)10.200.0.0/24 public subnet(we can select particular region)
    In order to make this public subnet.we would have to create route under our vpc and add this to the subnet association.
    * create a routetable.and then you want to add a route for the internet.
    * by default as we know routetable  would have an entry for this local VPC. that means to route the traffic with in VPC only.
    * we have to enable the traffic to and through internet and that where we edit this route table and add destination for the internet and will route it through IGW. 
       in routetable there is a option called routes
       10..200.0.0/16     local    active (default one)
       0.0.0.0/16         ourIGW   (we have to add this under routes to access to the internet)
    * make sure this route table associate with the subnet.
    * edit subnetassociation and add our subnet which we want to make it public.
    *This makes a subnet to a pulic subnet.  
    
  b)10.200.1.0/24 private subnet(create a subnet)
   * now similarly  create a route table for the privatesubnet.
   * if we see routes it routes with in the vpc only.we dont want to modify this because we want to make it private.
   * now add this route to the subnet under subnet associations.
   * this will make this subnet as a private subnet.

4)now create 2 ec2 instances,one is under public subnet with an auto assign publicis enabled.another ec2 instance under private subnet with auto assign public vpc Disabled.

5)public ec2 instance security group while creating 
  type        protocal             portrange          source
  ssh          TCP                  22                MY IP  
  
6)we connect to private ec2 instance throught public instance through via SSH(port 22 for that)
    type        protocal             portrange          source
     ssh          TCP                  22               custom 
     ICMP         ICMP               0.65535            custom
     
 7)lets try to login to public instance.and try ping command to check the internet connection.
 8)Now try to connect to private instance through public instance
  login in public instace and try ssh hostname@privateip  (it won't connect because we didn't provide pem key)
  now copy pem key in a file and give 400 permission to that file and now try 
  ssh -i examplekey.name hostanme@ipadress of private instance.
