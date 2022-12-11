- `service httpd start` - start the service
- `systemctl start httpd`
- `systemctl stop httpd`
- `systemctl status httpd`
- `system enable httpd` - configure httpd to start at startup
- `sytem disable httpd` - configure to not start at startup

Add service under this path:
`/etc/systemd/system`
create a file `{name}.service` and inside :
[Service]
ExecStart =/usr/bin/python3 /opt/code/my_app.py

`systemctl daemon-reload` - notify about changes
`systemctl start my_app` - start the service

configure to boot on startup add to the `{name}.service`
[Install]
WantedBy=multi-user.target 

Later run command `systemctl enable my_app`

Add metadata:
[Unit]
Description=My python web application

[Service]
ExecStart=
ExecStartPre=/opt/code/configure_db.sh
ExecStartPost=/opt/code/email_status.sh

automatically restart
Restart=always


`