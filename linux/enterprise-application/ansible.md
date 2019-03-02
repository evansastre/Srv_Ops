# Ansible

## Command

```text
yum install ansible -y
sed -i '/Ex 1/i\[local]' /etc/ansible/hosts
sed -i '/Ex 1/i\127.0.0.1' /etc/ansible/hosts
sed -i '/Ex 1/i\[remote]' /etc/ansible/hosts
sed -i '/Ex 1/i\192.168.1.1' /etc/ansible/hosts

#run local
ansible -i ./hosts --connection=local local -m ping
#run remote
ansible -i ./hosts remote -m ping
#-i ./hosts is default setting
#run remote with specific key
ansible -i ./hosts remote -v -m ping -u root --private-key=~/.ssh/id_rsa
#-m ping means use ping module

# Run against a local server
ansible -i ./hosts local --connection=local -b --become-user=root \
    -m shell -a 'yum install nginx'
# Run against a remote server
ansible -i ./hosts remote -b --become-user=root all \
    -m shell -a 'yum install nginx'
#-b --become-user=root  runas
#-a "some command"  means add command to shell module

-u USERNAME --user=USERNAME 指定移动端的执行用户
-U SUDO_USERNAME --sudo-user=USERNAME
-s --sudo -u指定用户的时候，使用sudo获得root权限
-k --ask-pass  提示输入ssh的密码，而不是使用基于ssh的密钥认证
-K --ask-sudo-pass 提示输入sudo密码，与--sudo一起使用

ansible remote -m shell -a "ifconfig | grep 192." -u UserName -k

```

## Playbooks

```text
ansible-playbook -i ./hosts nginx.yml

```



