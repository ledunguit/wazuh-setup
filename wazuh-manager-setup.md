## Wazuh Manager Installation
This process will go through the installation of the **Wazuh Manager** in a 1 GB RAM **Ubuntu Server 20.04** node.

**Note:** It is recommended to set Static IP address for this node rather than static one.

**Note:** Root user privileges are required to execute all the following commands.

### Adding the Wazuh repository
1. Install the necessary packages for the installation:
```shell
sudo apt install curl apt-transport-https lsb-release gnupg2
```
2. Install the GPG key:
```shell
sudo curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | apt-key add -
```
3. Add the repository:
```shell
sudo echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee -a /etc/apt/sources.list.d/wazuh.list
```
4. Update the package information:
```shell
sudo apt update
```

### Installing the Wazuh manager
1. Install the Wazuh Manager package:
```shell
sudo apt install wazuh-manager
```
2. Enable and start the Wazuh Manager service:
```shell
sudo systemctl daemon-reload
sudo systemctl enable wazuh-manager
sudo systemctl start wazuh-manager
```
3. Run the following command to check if the Wazuh Manager is active:
```shell
sudo systemctl status wazuh-manager
```

### Disabling Wazuh Repositories
It is recommended to disabling the Wazuh repository to prevent accidental upgrades. To do so, use the following command:
```shell
sudo sed -i "s/^deb/#deb/" /etc/apt/sources.list.d/wazuh.list
sudo apt update
```

### Miscellaneous
1. Allowing ports in firewall:
```shell
sudo ufw allow 1514
sudo ufw allow 1515
sudo ufw allow 55000
```
2. To check if the ports are listening:
```shell
ss -lntp
```
3. To check connected agents:
```shell
sudo /var/ossec/bin/manage_agents -l
```
4. To check agents status:
```shell
sudo /var/ossec/bin/agent_control -l
```
5. To check logs from agents:
```shell
sudo tail -f /var/ossec/logs/alerts/alerts.log
```

**NEXT:** [Elasticsearch Installation](./elasticsearch-setup.md)
