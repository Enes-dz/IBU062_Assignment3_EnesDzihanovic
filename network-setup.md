Devices FROM Project:
1. Router(Full Name: Router2) Model: 1941
2. Switch(Switch4) Model: 2960-24TT
3. Switch(Switch5) Model: 2960-24TT
4. PC(PC3) PC-PT - 168.90.0.2
5. PC(PC4) PC-PT - 168.90.0.3
6. Laptop(Laptop1) Laptop-PT - 168.90.0.4
7. Server(Server3) Server-PT - 168.90.0.5
8. Server(Server4) Server-PT - 210.3.14.13
9. Server(Server5) Server-PT - 210.3.14.12
10. PC(PC5) PC-PT - 210.3.14.11
11. PC(PC6) PC-PT - 168.90.0.6
12. PC(PC7) PC-PT - 210.3.14.14

**Explonation** {*Additional Explonation of code*} [*Format of the code*]

1. First step was to setup dhcp Pool for router port "GigabitEthernet 0/0". I did this in following steps.
    a) When entering in CLI I started with following commands:
        -- Router>enable
        -- Router#configure terminal
    
    b) Next is naming DHCP pool which in my case was MYPOOL with command:
        -- Router(config)#ip dhcp pool MYPOOL
    
    c) After that I needed to give this pool network address, router gateway, subnet mask, and I added additional DNS server(from Labs because I didn't know if it would work without it.):
        --Router(dhcp-config)#network 168.90.0.0 255.255.0.0 {[Network Address] [Subnet Mask]}
        --Router(dhcp-config)#default-router 168.90.0.1
        --Router(dhcp-config)#dns-server 8.8.8.8
        --Router(dhcp-config)#exit {"Exiting dhcp-config"}
    
    d) Then it was time for connecting my "GigabitEthernet 0/0" to this DHCP pool with "Default Gateway" IP:
        --Router(config)#interface gigabitethernet0/0 {"Entering this port settings"}
        --Router(config-if)#ip address 168.90.0.1 255.255.0.0 {[Default Gateway] [Subnet Mask]}

    e) Additionally while I was in this port I made sure to that it was ON. This can also be changed in config tab:
        --Router(config-if)#no shutdown

    i) One more addition is that I excluded Dafault Gateway Address and Network address to avoid assigning Router addresses:
        --Router(config)#ip dhcp excluded-address 168.90.0.0 168.90.0.1
    
2. Second step is creating dhcp Pool for router port "GigabitEthernet 0/1" and it's pretty the same as for the first Port - of course with different values that were provided in the assignment.



**IMPORTANT NOTE**

In router there is additional DHCP Pool called "GlobalDHCP" that is not connected to anything. I used this pool for testing purposes and I hope that it isn't a big Problem.