# soclab
SOC automation in a homelab
<h1 align='center'>Overview</h1>
<p> Integrating various applications together to make an automated Security Operations Center(SOC) in a homelab</p>

![SOC_chart](https://github.com/cats-toy/soclab/blob/main/SOC.drawio.svg)
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


<h1 align='center'>Wazuh manager</h1>
<p>Installed using curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh && sudo bash ./wazuh-install.sh -a  </p>
<p> Had to kill several processes using ports :443 and :9200 to enable the wazuh installer helper to commence installation. I had nginx(using port :443) and docker(docker-proxy using port :9200) installed prior to this project, simply stopping the processes for this instance will allow for installation. I found the processes using this ports with 'sudo ss -lptn "sport = :<port>'.</p>
<p> Installed Wazuh central components, since UFW is present, i opened ports 1515/tcp and 1514/tcp, however for convenience I stopped UFW. After logging in using <wazuh-dashboard-ip>:443, wazuh will check its API connection and other systems.</p>
<p>Encountered an issue where the wazuh dashboard was not "ready". To remedy this, I started the wazuh-manager, wazuh-indexer and wazuh-dashboard on my Ubuntu VM. I also changed the configuration files for the dashboard in /etc/wazuh-dashboard/opensearch_dashboards.yml and /usr/share/wazuh-dashboard/data/wazuh/config/wazuh.yml, specifically the host port/url as it is 127:0:0:1 by default,I restarted wazuh-dashboard to apply the changes.</p> <img src='https://imgur.com/kxMU7sT.png' alt=wazuh dashboard config> <img src='https://imgur.com/rT0xLKr.png' alt=wazuh dashboard opensearch>

<h1 align='center'>Wazuh Agent</h1>
<p>Installed Wazuh agent on separate vm since the manager itself acts as an agent. </p>
<p> Using the wazuh manager, I made a new agent pack using the dashboard and filled out the form for my ubuntu agent(amd64). <br> <img src='https://imgur.com/63wVfFI.png'> Following the form, I eventually got the command to install my wazuh agent. I started up a new ubuntu VM by cloning a clean baseline snapshot of my current ubuntu VM, renamed its hostname to ubuntuagentvm, and installed the wazuh agent. </p>

<p> However, when checking my wazuh manager for my agent, it wasn't appearing. I checked the status for the wazuh agent and it was still running and active. I then check the configuration files for the agent in /var/ossec/etc/ossec.conf and changed the manager's IP address to the static address of my VM. After restarting the agent, it showed up on my manager. <br> <img src='https://imgur.com/p5T7q0k.png'> </p>

<p></p>

Installing TheHive and Cortex
-
-
-
-
