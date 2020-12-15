# ansible-install
# Установка Ansible
Добавляем репозиторий EPEL и устанавливаем Ansible
```
#yum install epel-release
#yum install ansible
```

На сервере Ansible генерируем RSA-ключ
```
#ssh-keygen -t rsa
```
На удаленном сервере включаем аутентификацию по ключам
```
#vi /etc/ssh/sshd_config
PubkeyAuthentication yes 
AuthorizedKeysFile .ssh/authorized_keys

#systemctl restart shd
```
На сервере Ansible копируем публичный ключ id_pub.pub на удаленный сервер
```
#ssh-copy-id -i ~/.ssh/id_rsa.pub root@IP_ADDR
```
Тестируем подключение
```
#ssh IP_ADDR
```
Добавляем удаленный сервер в файл hosts
```
#vi /etc/ansible/hosts
[server]
centos ansible_ssh_host=IP_ADDR
```
Проверяем работу Ansible
```
#ansible server -m ping
centos | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```
