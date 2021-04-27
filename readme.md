To install software or manage Windows server 2016 through Ansible, the following steps need to be followed before we run a task against the remote server_name

Windows server_name

1.  Login to the windows server_name
2. Download the script "ConfigureRemotingforAnsible.ps1" from this repo
3. Open the powershell window with administrator privileges and execute the ScriptBlock

You should get the following reponse

Self-signed SSL certificate generated; thumbprint: 8828D42445BA957038D880C4458950CBACC0CFEC


wxf                 : http://schemas.xmlsoap.org/ws/2004/09/transfer
a                   : http://schemas.xmlsoap.org/ws/2004/08/addressing
w                   : http://schemas.dmtf.org/wbem/wsman/1/wsman.xsd
lang                : en-US
Address             : http://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous
ReferenceParameters : ReferenceParameters

Ok.

4. Verify winrm listener by running the winrm enumerate winrm/config/Listener

PS C:\Users\azureuser\Desktop> winrm enumerate winrm/config/Listener
Listener
    Address = *
    Transport = HTTP
    Port = 5985
    Hostname
    Enabled = true
    URLPrefix = wsman
    CertificateThumbprint
    ListeningOn = 10.0.2.4, 127.0.0.1, ::1, 2001:0:2851:782c:1c82:34c4:f5ff:fdfb, fe80::5efe:10.0.2.4%9, fe80::1968:73e5
:5e21:48ad%5, fe80::1c82:34c4:f5ff:fdfb%10

Listener
    Address = *
    Transport = HTTPS
    Port = 5986
    Hostname = windowsremoteho
    Enabled = true
    URLPrefix = wsman
    CertificateThumbprint = 8828D42445BA957038D880C4458950CBACC0CFEC
    ListeningOn = 10.0.2.4, 127.0.0.1, ::1, 2001:0:2851:782c:1c82:34c4:f5ff:fdfb, fe80::5efe:10.0.2.4%9, fe80::1968:73e5
:5e21:48ad%5, fe80::1c82:34c4:f5ff:fdfb%10

for more common winrm - ansible connection issue, refer https://docs.ansible.com/ansible/devel/user_guide/windows_setup.html#common-winrm-issues


5. winrm set winrm/config/service/auth @{Basic="true"}
6. winrm set winrm/config/service @{AllowUnecrypted="true"}
