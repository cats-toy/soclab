# soclab
SOC automation in a homelab
<h1 align='center'>Overview</h1>
<p> Integrating various applications together to make an automated Security Operations Center(SOC) in a homelab</p>


<table>
  <tr>
    <th>Tools</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <th>Shuffle</th>
    <th>Connects all the other software in one platform</th>
  </tr>
  <tr>
    <th>Wazuh</th>
    <th>SIEM and XDR platform</th>
  </tr>
  <tr>
    <th>TheHive</th>
    <th>Incident Response</th>
  </tr>
  <tr>
    <th>TheHive-Cortex</th>
    <th>Analysis</th>
  </tr>
</table>


<h1 align='center'>Installing docker </h1>
-
-
-


<h1 align='center'>Installing Shuffle</h1>

-Follow the instructions on the shuffle page in github
-
<p>Encountered issue while downloading using docker-compose,<img src='https://imgur.com/XRKDmRP.png'><br>
In order to fix this problem, I had to go into the Shuffle configuration page at <a href='https://shuffler.io/docs/configuration'>shuffle config</a> to find the strings to be inputted.<br>
Resulting in this,<br> <img src='https://imgur.com/ZyjDFch.png'><br>
</p>


Installing Wazuh
- Installed using curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh && sudo bash ./wazuh-install.sh -a 
- Had to kill several processes using ports :443 and :9200 to enable the wazuh installer helper to commence installation.
- Installed Wazuh central components, since UFW is present, i opened ports 1515/tcp and 1514/tcp. After logging in using <wazuh-dashboard-ip>:443, wazuh will check its API connection and other systems.
- Installed Wazuh agent on separate vm since the manager itself acts as an agent.


Installing TheHive and Cortex
-
-
-
-
