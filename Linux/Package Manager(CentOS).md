Red hat package manager(rpm)

- `rpm -i telnet.rpm`  - install
- `rpm -e telnet.rpm` - delete
- `rpm -q telnet.rpm`  - query package
- `rpm -qa` - list all installation

Yum package manager install dependecies too

- `yum install ansible`
- `ls /etc/yum.repos.d/`
- `yum repolist` - listing packages
- `yum list ansible` - package name and version
- `yum remove ansible` - delele package
- `yum --showduplicates list ansible`
- `yum install ansible-2.4.2.0` - specify specific version