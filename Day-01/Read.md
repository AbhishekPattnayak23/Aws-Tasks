<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
    <img src="https://github.com/AbhishekPattnayak23/Aws-Tasks/blob/main/Assets/Understanding_IP_Addressing.jpg"  width="300" height="300">
    <h1>IP Explained</h1>
    <h2>Welcome to the Network Setup Guide! This guide will help you understand the basics of IP addresses, classes, public and private IPs, and how to configure them for different environments.</h2>
    <ul>
        <li>Understanding IP Addresses</li>
        <li> In any network setup, devices communicate with each other using IP addresses. There are two types of IP addresses:</li>
        <li>IPv4: Shorter addresses, like phone numbers for devices.</li>
        <li>IPv6: Longer addresses, similar to phone numbers but with more digits.</li>
        <li>IP Address Ranges:
            <p>IPv4 addresses range from 0.0.0.0 to 255.255.255.255. They are divided into five classes: A, B, C, D, and E.</p>
        </li>
    </ul>
        <ul>
        <li>Class A: 1.0.0.0 to 126.255.255.255</li>
        <li>Class B: 128.0.0.0 to 191.255.255.255</li>
        <li>Class B: 128.0.0.0 to 191.255.255.255</li>
        <li>Class C: 192.0.0.0 to 223.255.255.255</li>
        <li>Classes D and E are reserved for specific purposes and not commonly used.</li>    
    </ul>
    <h2>Loopback Address</h2>
    <hr>
    <p>You might wonder why 127 is skipped. 127.0.0.1 is reserved for loopback, meaning a device pings itself.</p>

    <h2>Public and Private IPs</h2>
    <hr>
    <p>As IP addresses are limited, there's a concept of public and private IPs.</p>

    <ul>
        <li>Public IPs: Used for communication over external networks.</li>
        <li>Private IPs: Used internally within closed infrastructures or office environments.</li>    
        <li>Private IP Ranges</li>   
        <li>Private IPs are reserved within specific ranges:</li>    
    </ul>

    <p>
        10.0.0.0 to 10.255.255.255 (10/8 prefix)
        172.16.0.0 to 172.31.255.255 (172.16/12 prefix)
        192.168.0.0 to 192.168.255.255 (192.168/16 prefix)
        These addresses are for internal use only and should not be accessible from outside the network.
    </p>

    <h2>Configuring IP Addresses</h2>
    <hr>
    <p>Example
        To demonstrate, you can open CMD and type ipconfig to view your IPv4 private address. 
        Then, by searching "my public IP" on Google, you can find your public IP address.</p>

    <h2>Network Setup</h2>  
    
    <p>In the diagram above, you can see how public and private IPs are used in different environments.

        Now you have a basic understanding of IP addresses, classes, and how to use public and private IPs effectively. Happy networking!
        </p>

    <h2>More about Networking: A deep dive</h2>    
    <hr>

    <p>There are two types of IP’s</p>
       <ol>
        <li>IPv4</li>
        <li>IPv6</li>
       </ol>

    <p>IP ranges from 0.0.0.0 to 255.255.255.255</p>   

    <h3>There are classes also in IP address:</h3>
    <ul>
        <li>Class A – Range: 1.0.0.0 To 126.255.255.255
            Used for large networks with many devices, the first 8 bits represent the network, and the remaining 24 bits represent host addresses. The default subnet mask is 255.0.0.0, and the first octet is 0–127.</li>
        <li>Class B – Range: 128.0.0.0 To 191.255.255.255
            Used for medium-sized networks, the first 16 bits represent the network, and the remaining 16 bits represent host addresses. The default subnet mask is 255.255.0.0, and the first octet is 128–191.</li>  
        <li>Class C – Range: 192.0.0.0 To 223.255.255.255
            Used for small networks, the first 24 bits represent the network, and the remaining 8 bits represent host addresses. The default subnet mask is 255.255.255.0, and the first octet is 192–223.</li> 
       <li>Class D
        Used for multicast addressing, which allows a single data packet to be transmitted to multiple devices simultaneously.</li>   
        <li>Class E
            Reserved for experimental purposes and future use. 
            IPv4 addresses are 32-bit numbers that are typically written as four octets separated by periods.</li>       
    </ul>

    <ul>
        <li>Class A – 1.0.0.0 TO 126.255.255.255</li>
        <li>Class B – 128.0.0.0 TO 191.255.255.255</li>    
        <li>Class C – 192.0.0.0 TO 223.255.255.255</li>
    </ul>

    <p>Here we can notice that 127.0.0.1 is left completely which is called as loopback address which pings its own devices only. 
        Public IP v/s Private IP:
        Using these IP’s can cause shortage in IP’s so <a href="https://datatracker.ietf.org/doc/html/rfc1918">RFC1918(org)</a> came out with an idea of Public IP and Private IP</p>

        <p>Private IP’s ranges from: should be connected internally 
            10.0.0.0        -   10.255.255.255  (10/8 prefix)
            172.16.0.0      -   172.31.255.255  (172.16/12 prefix)
            192.168.0.0     -   192.168.255.255 (192.168/16 prefix)
       So operating inside a close infra or office environment, then private IP’s are used only.
       Public IP’s are used while accessing the internet gateway so that the confidential packets generated by an employee is not shared with the outside world through public IP’s.</p>

       <img src="https://github.com/user-attachments/assets/b137a247-b46d-4f45-8a24-1c2d8bcb1d54">
  
</body>
</html>
