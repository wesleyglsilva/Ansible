Ansible for Windows

*** Preparar o Windows para aceitar/executar playbooks ansible

[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)

powershell.exe -ExecutionPolicy ByPass -File $file -Verbose

winrm enumerate winrm/config/Listener

*** Executar o script ConfigureRemotingForAnsible.ps1 no powershell 

*** Popular o inventario (/etc/ansible/hosts)

[win]
192.168.0.119
[win:vars]
ansible_connection=winrm 
ansible_user=solides 
ansible_password=solides 
ansible_winrm_server_cert_validation=ignore

*** Referencias
https://opensource.com/article/19/2/ansible-windows-admin
https://github.com/ansible/ansible/blob/devel/examples/scripts/ConfigureRemotingForAnsible.ps1


