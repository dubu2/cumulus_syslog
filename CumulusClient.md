# Activate Remote Logging on Cumulus Linux Switch

## Create variable for Syslog Server IP address

 [USING VARIABLES](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#defining-variables-in-a-playbook)

    vars:  
        SYSLOGSERVER: 10.160.75.165

## Create file with action script to enable remote logging via mgmt vrf

 [WRITE TO SYSLOG WITH MANAGEMENT VRF ENABLED](https://docs.cumulusnetworks.com/version/cumulus-linux-37/Monitoring-and-Troubleshooting/#write-to-syslog-with-management-vrf-enabled)

 [CREATING LOCAL QUEUE FOR LOG MESSAGES](https://www.golinuxhub.com/2018/05/how-to-remote-logging-using-rsyslog-omfwd-redhat.html)

    sudo echo 'action(type="omfwd" target="{{ SYSLOGSERVER }}" device="mgmt" port="514" protocol="udp")' > /etc/rsyslog.d/11-remotesyslog.conf

## Restart the Remote Syslog service and reload the daemons

    sudo systemctl restart rsyslog.service

    sudo systemctl daemon-reload
