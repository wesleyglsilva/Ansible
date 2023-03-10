# Ansible for Windows

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
ansible_user=+++++++++ 
ansible_password=+++++++++ 
ansible_winrm_server_cert_validation=ignore

*** Criar os playbooks e subir para o github

*** Executar os playbooks a partir do github

ansible-pull -U https://github.com/wesleyglsilva/Ansible.git playbooks/install-htop.yml

*** Referencias
https://opensource.com/article/19/2/ansible-windows-admin
https://github.com/ansible/ansible/blob/devel/examples/scripts/ConfigureRemotingForAnsible.ps1
https://docs.ansible.com/ansible/latest/os_guide/windows_usage.html
https://4sysops.com/archives/automate-windows-updates-with-ansible/
https://www.youtube.com/watch?v=gIDywsGBqf4


