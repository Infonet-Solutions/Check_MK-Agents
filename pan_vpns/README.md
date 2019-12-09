# PAN_VPNS
This check is used in Check_MK to check the status of all VPN IPSec tunnels
This is done by query the appliance via XML API requests

## REQUIREMENTS
- python-requests needs to be present on the Check_MK system

## PREREQUISITES
- Create a user in the PaloAlto appliance with XML API privileges
- Get the XML API Key for the newly created user
```bash
curl -X GET 'https://firewall/api/?type=keygen&user={USERNAME}&password={PASSWORD}'
```
A successful response should contain your XML API Key
```html
<response status="success">
    <result>
        <key>gJlQWE56987nBxIqyfa62sZeRtYuIo2BgzEA9UOnlZBhU</key>
    </result>
</response>
```
- Place the agent and the check files in their respective folders
```bash
/opt/omd/sites/{SITENAME}/local/share/check_mk/checks

/opt/omd/sites/{SITENAME}/local/share/check_mk/agents/special
```

- in "WATO -> Host & Service Parameters -> Datasource Programs -> Individual program call instead of agent access" create a rule to call the check
```
/omd/sites/{SITENAME}/local/share/check_mk/agents/special/pan_vpns -k {XMLAPI KEY} $HOSTADDRESS$
```

- Apply the rule to every Appliance for which you want to monitor IPSec Tunnels
