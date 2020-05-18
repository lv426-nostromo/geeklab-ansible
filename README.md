# geeklab-ansible
## Geek Lab: setup basic Centos 7 web server (nginx, php-fpm) with ansible

Пробный плейбук по базовой настройке web сервера на основе Centos 7

Как пользоваться:

1. Прописать хосты или группы хостов в файле hosts

```
    [web]
    192.168.1.110 ansible_connection=ssh ansible_ssh_user=root 
    192.168.1.111 ansible_connection=ssh ansible_ssh_user=root 
    [test]
    192.168.1.112 ansible_connection=ssh ansible_ssh_user=root ansible_password=your_root_password
```

2. При необходимости отредактировать ansible.cfg, полезно если использовать не глобальный ansible, а запускать его в virtualenv.

```
    #inventory = /etc/ansible/hosts  ; This points to the file that lists your hosts
    [defaults]
    inventory = /home/user/projects/ansible/geeklab-ansible/hosts  
    ansible_python_interpreter=/usr/bin/python
    log_path =  /home/user/projects/ansible/geeklab-ansible/ansible.log
    roles_path = /home/user/projects/ansible/geeklab-ansible/roles
```

3. Задать переменные в tasks/main.yml

```
    var_zabbix_server: <== ip zabbix server
    web_root: /hosts  <== /hosts/domain1.com 
    web_group: hosting <== группа для веб сервисов
    web_user: <== имя пользователя 
    user_password: <== хэш пароля пользователя
    mysql_root_password: <== пароль для рута mysql
    domains: <== список доменов для создания виртуальных хостов
    - domain1.com
    - domain2.com
    mysql_master_ip: <== ip адрес мастер хоста для репликации
    mysql_slave_ip: <== ip слейва для репликации
    mysql_replication_user: <== пользователь mysql для репликации
    mysql_repluser_pass: <== пароль пользователя для репликации
    mysql_db_user: <== пользователь базы данных проекта
    mysql_user_password: <== его пароль
    mysql_project_db: <== база данных проекта
```

4. Закомментировать импорты ненужных тасков или импортировать нужные.

5. Запустить исполнение плейбука () -v, -vv, -vvv  делает вывод короче/подробнее):

```
    ansible-playbook -vv tasks/main.yml
 ```

