
To save time later in the DEMO we should populate this before configuring the ONPREM environment.
There are two VPN connections ... one between AWS and ONPREM ROUTER1 and one between AWS and ONPREM ROUTER2
For each of those there are two tunnels ... AWS Endpoint A -> ONPREMROUTER
and AWS endpointB -> ONPREMROUTER

Those are the details we will populate

# SHARED VALUES

ROUTER1_PRIVATE_IP                  = 192.168.12.31	
ROUTER2_PRIVATE_IP                  = 192.168.12.250
ONPREM BGP ASN                      = 65016
AWS BGP ASN                         = 64512

# CONNECTION1 - AWS => ON PREM ROUTER1

CONN1_TUNNEL1_PresharedKey          = QBTMl1fwgxkOXsrRDM7Wt9336MqQqbpA
CONN1_TUNNEL1_ONPREM_OUTSIDE_IP     = 54.144.208.197
CONN1_TUNNEL1_AWS_OUTSIDE_IP        = 75.2.94.33
CONN1_TUNNEL1_ONPREM_INSIDE_IP      = 169.254.57.230/30
CONN1_TUNNEL1_AWS_INSIDE_IP         = 169.254.57.229/30
CONN1_TUNNEL1_AWS_BGP_IP            = 169.254.57.229

CONN1_TUNNEL2_PresharedKey          = xm7L6x7FrCuPeSX9OZJ7jGpb4STJdk2p
CONN1_TUNNEL2_ONPREM_OUTSIDE_IP     = 54.144.208.197
CONN1_TUNNEL2_AWS_OUTSIDE_IP        = 76.223.40.80
CONN1_TUNNEL2_ONPREM_INSIDE_IP      = 169.254.100.78/30
CONN1_TUNNEL2_AWS_INSIDE_IP         = 169.254.100.77/30
CONN1_TUNNEL2_AWS_BGP_IP            = 169.254.100.77


# CONNECTION2 - AWS => ON PREM ROUTER2

CONN2_TUNNEL1_PresharedKey          = c8uRF9R_ARtGtkPjWBKd2nONfA5pOO3W
CONN2_TUNNEL1_ONPREM_OUTSIDE_IP     = 18.205.161.250
CONN2_TUNNEL1_AWS_OUTSIDE_IP        = 13.248.171.102
CONN2_TUNNEL1_ONPREM_INSIDE_IP      = 169.254.34.214/30
CONN2_TUNNEL1_AWS_INSIDE_IP         = 169.254.34.213/30
CONN2_TUNNEL1_AWS_BGP_IP            = 169.254.34.213

CONN2_TUNNEL2_PresharedKey          = ElAc50hJ7NGS7SzEJC4aourzA5t8Mhme
CONN2_TUNNEL2_ONPREM_OUTSIDE_IP     = 18.205.161.250
CONN2_TUNNEL2_AWS_OUTSIDE_IP        = 99.83.199.223
CONN2_TUNNEL2_ONPREM_INSIDE_IP      = 169.254.186.254/30
CONN2_TUNNEL2_AWS_INSIDE_IP         = 169.254.186.253/30
CONN2_TUNNEL2_AWS_BGP_IP            = 169.254.186.253



# INSTRUCTIONS ON GETTING THE VALUES

We will be locating values for a specific connection `CONN1` or `CONN2` and a specific tunnel .. `TUNNEL1` or `TUNNEL2`

For anything starting with CONN1 .. Look in the `CONNECTION1CONFIG.TXT` file
For anything starting with CONN2 .. Look in the `CONNECTION2CONFIG.TXT` file
In each of the above files, for anything showing TUNNEL1 fine the section `IPSec Tunnel #1` in the above files (THE TOP HALF)
In each of the above files, for anything showing TUNNEL2 fine the section `IPSec Tunnel #2` in the above files (THE BOTTOM HALF)

For `ROUTER1_PRIVATE_IP` its the 192.168.12.SOMETHING Private IPv4 Address for `ROUTER1` - Check the `Outputs` of the `ONPREM` CFN Stack for `Private IP of Router1`
For `ROUTER2_PRIVATE_IP` its the 192.168.12.SOMETHING Private IPv4 Address for `ROUTER2` - Check the `Outputs` of the `ONPREM` CFN Stack for `Private IP of Router2`

For `CONN1_TUNNEL1_PresharedKey` open `CONNECTION1CONFIG.TXT`, Locate `IPSec Tunnel #1`, Locate `- Pre-Shared Key` Your key is there
For `CONN1_TUNNEL2_PresharedKey` open `CONNECTION1CONFIG.TXT`, Locate `IPSec Tunnel #2`, Locate `- Pre-Shared Key` Your key is there
For `CONN2_TUNNEL1_PresharedKey` open `CONNECTION2CONFIG.TXT`, Locate `IPSec Tunnel #1`, Locate `- Pre-Shared Key` Your key is there
For `CONN2_TUNNEL2_PresharedKey` open `CONNECTION2CONFIG.TXT`, Locate `IPSec Tunnel #2`, Locate `- Pre-Shared Key` Your key is there

For `CONN1_TUNNEL1_ONPREM_OUTSIDE_IP` its the PublicIPv4 Address of `ROUTER1` 
    `CONN1_TUNNEL2_ONPREM_OUTSIDE_IP` its the PublicIPv4 Address of `ROUTER1` 
    `CONN2_TUNNEL1_ONPREM_OUTSIDE_IP` its the PublicIPv4 Address of `ROUTER2` 
    `CONN2_TUNNEL2_ONPREM_OUTSIDE_IP` its the PublicIPv4 Address of `ROUTER2` 

For `CONN1_TUNNEL1_AWS_OUTSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Outside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN1_TUNNEL2_AWS_OUTSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Outside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN2_TUNNEL1_AWS_OUTSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Outside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN2_TUNNEL2_AWS_OUTSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Outside IP Addresses:`, locate `- Virtual Private Gateway` the value is there

For `CONN1_TUNNEL1_ONPREM_INSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Customer Gateway` the value is there
For `CONN1_TUNNEL2_ONPREM_INSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Customer Gateway` the value is there
For `CONN2_TUNNEL1_ONPREM_INSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Customer Gateway` the value is there
For `CONN2_TUNNEL2_ONPREM_INSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Customer Gateway` the value is there

For `CONN1_TUNNEL1_AWS_INSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN1_TUNNEL2_AWS_INSIDE_IP` open `CONNECTION1CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN2_TUNNEL1_AWS_INSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #1`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Virtual Private Gateway` the value is there
For `CONN2_TUNNEL2_AWS_INSIDE_IP` open `CONNECTION2CONFIG.TXT`, locate `IPSec Tunnel #2`, locate `#3: Tunnel Interface Configuration`, locate `Inside IP Addresses:`, locate `- Virtual Private Gateway` the value is there

For `CONN1_TUNNEL1_AWS_BGP_IP` the value is the same as `CONN1_TUNNEL1_AWS_INSIDE_IP`
For `CONN1_TUNNEL2_AWS_BGP_IP` the value is the same as `CONN1_TUNNEL2_AWS_INSIDE_IP`
For `CONN2_TUNNEL1_AWS_BGP_IP` the value is the same as `CONN2_TUNNEL1_AWS_INSIDE_IP`
For `CONN2_TUNNEL2_AWS_BGP_IP` the value is the same as `CONN2_TUNNEL2_AWS_INSIDE_IP`


