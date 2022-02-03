# TUGAS BESAR

**RACHMAD SAFLYI & ALIFIA**

------

## Step by Step

------

SKEMA :
![00_scheme](https://user-images.githubusercontent.com/93419670/152255035-888125d0-5738-484c-97c8-9e1bb98aa345.png)

------

Make new lxc and configure the IP of each lxc

![Capture1](https://user-images.githubusercontent.com/93419670/152255278-09469dc9-9888-47eb-91ac-17934951a558.PNG)

install open ssh server in all of the lxc above, after that we go to ansible

```
apt install openssh-server
```

Go to

```
cd ~/ansible/TUBES
```

And then go to 'nano hosts' to classified each lxc just like the scheme above

![Capture2](https://user-images.githubusercontent.com/93419670/152255603-580ac68d-a6f6-4493-b606-34b79006f1d1.PNG)

And then

```
nano install-ci.yml //for code igniter
nano install-laravel.yml //for laravel
nano install-wp.yml //for wordpress
nano install-yii.yml //for yii2.0
nano install-mariadb.yml //for phpmyadmin
```

![Capture3](https://user-images.githubusercontent.com/93419670/152255641-b10b9daf-fd17-41e3-9650-d33ce3727992.PNG)
![Capture4](https://user-images.githubusercontent.com/93419670/152255645-f4b44094-32fb-460c-98da-f6eb754b16e0.PNG)
![Capture5](https://user-images.githubusercontent.com/93419670/152255633-af5d8e78-5488-4467-b559-2e5a5083121d.PNG)
![Capture6](https://user-images.githubusercontent.com/93419670/152255635-f7ebe1ba-7d36-4278-ba47-09687edd1bb4.PNG)
![Capture7](https://user-images.githubusercontent.com/93419670/152255638-1a8b45ee-a2c8-443f-a47d-318764a6c617.PNG)

After all done we go to

```
cd /roles/ci/tasks
nano main.yml
```

![Capture11](https://user-images.githubusercontent.com/93419670/152260524-70209b5a-7386-4361-8a34-c4cb0f5eb556.PNG)

After all done we go to

```
cd ../templates
nano app.conf
```

![Capture12](https://user-images.githubusercontent.com/93419670/152260406-ee17890f-f9a1-4ee1-8038-eb621534aace.PNG)


After all done we go to

```
cd ../handlers
nano main.yml
```

![02_6_app_ci_handlers_main_yml](assets/02_6_app_ci_handlers_main_yml.PNG)

The ansible for Code Igniter is done, the we go to

```
cd ../../
cd php/tasks
nano main.yml
```

![02_7_php_tasks_main_yml](assets/02_7_php_tasks_main_yml.PNG)

![02_8_php_tasks_main_yml](assets/02_8_php_tasks_main_yml.PNG)

Then go to

```
cd ../handlers
nano main.yml
```

![02_9_php_handlers_main_yml](assets/02_9_php_handlers_main_yml.PNG)

The ansible for php is done, next one is Laravel, we need to go to

```
cd ../../
cd lv/tasks
nano main.yml
```

![02_10_lv_tasks_main_yml](assets/02_10_lv_tasks_main_yml.PNG)

![02_11_lv_tasks_main_yml](assets/02_11_lv_tasks_main_yml.PNG)

![02_12_lv_tasks_main_yml](assets/02_12_lv_tasks_main_yml.PNG)

After that we go to

```
cd ../templates
nano env.template
```

![02_13_lv_templates_env_template](assets/02_13_lv_templates_env_template.PNG)

![02_14_lv_templates_env_template](assets/02_14_lv_templates_env_template.PNG)

Then go to

```
nano lv.conf
```

![02_15_lv_templates_lv_conf](assets/02_15_lv_templates_lv_conf.PNG)

After configuring in templates, we go to handlers

```
cd ../handlers
nano main.yml
```

![02_16_lv_handlers_main.yml](assets/02_16_lv_handlers_main.yml.PNG)

The ansible for Laravel is done, the next one is mariadb, first we go to

```
cd ../../../
cd db/tasks
nano main.yml
```

![02_17_db_tasks_main.yml](assets/02_17_db_tasks_main.yml.PNG)

Then go to templates

```
cd ../templates
nano my.cnf
```

![02_18_db_templates_my_cnf](assets/02_18_db_templates_my_cnf.PNG)

Next go to handlers

```
cd ../handlers
nano main.yml
```

![02_19_db_handlers_main_yml](assets/02_19_db_handlers_main_yml.PNG)

The ansible for database is done, the next one is for PHP My Admin, just like before we need to go to

```
cd ../../
cd pma/tasks
nano main.yml
```

![02_20_pma_tasks_main_yml](assets/02_20_pma_tasks_main_yml.PNG)

![02_21_pma_tasks_main_yml](assets/02_21_pma_tasks_main_yml.PNG)

![02_23_pma_tasks_main_yml](assets/02_23_pma_tasks_main_yml.PNG)

Then go to

```
cd ../templates
nano lxc_mariadb.conf
```

![02_24_pma_templates_lxcmariadb_conf](assets/02_24_pma_templates_lxcmariadb_conf.PNG)

Then go to handlers

```
cd ../handlers
nano main.yml
```

![02_25_pma_handlers_main_yml](assets/02_25_pma_handlers_main_yml.PNG)

Yay the ansible for PHP My Admin is done, next one is YII2.0

```
cd ../../
cd yii/tasks
nano main.yml
```

![02_26_yii_tasks_main_yml](assets/02_26_yii_tasks_main_yml.PNG)

![02_27_yii_tasks_main_yml](assets/02_27_yii_tasks_main_yml.PNG)

![02_28_yii_tasks_main_yml](assets/02_28_yii_tasks_main_yml.PNG)

The next one we go to templates

```
cd ../templates
nano yii.conf
```

![02_29_yii_templates_yii_conf](assets/02_29_yii_templates_yii_conf.PNG)

![02_30_yii_templates_yii_conf](assets/02_30_yii_templates_yii_conf.PNG)

Then we go to handlers

```
cd ../handlers
nano main.yml
```

![02_31_yii_handlers_main_yml](assets/02_31_yii_handlers_main_yml.PNG)

The ansible for YII2.0 is done, so the next one is Wordpress

```
cd ../../
cd wp/tasks
nano main.yml
```

![02_32_wp_tasks_main_yml](assets/02_32_wp_tasks_main_yml.PNG)

Then go to templates

```
cd ../templates
nano wp.conf
```

![02_33_wp_templates_wp_conf](assets/02_33_wp_templates_wp_conf.PNG)

Then

```
nano wp.local
```

![02_34_wp_templates_wp_local](assets/02_34_wp_templates_wp_local.PNG)

Don't forget to go to handlers

```
cd ../handlers
nano main.yml
```

![02_35_wp_handlers_main_yml](assets/02_35_wp_handlers_main_yml.PNG)

This is the configuration for vm.local

```
sudo nano /etc/nginx/sites-available/vm.local
```

![02_36_etc_sites_availabe_vmlocal](assets/02_36_etc_sites_availabe_vmlocal.PNG)

![02_37_etc_sites_availabe_vmlocal](assets/02_37_etc_sites_availabe_vmlocal.PNG)

![02_38_etc_sites_availabe_vmlocal](assets/02_38_etc_sites_availabe_vmlocal.PNG)

This is the configuration for hosts in VM

```
nano /etc/hosts
```

![02_39_etc_hosts_vm](assets/02_39_etc_hosts_vm.PNG)

![03_1_ansibleplaybook_pma_mariadb](assets/03_1_ansibleplaybook_pma_mariadb.PNG)

After we add the ansible, then we run them using

```
ansible-playbook -i hosts install-''.yml -k
```

The first one is mariadb

![03_2_ansibleplaybook_pma_mariadb](assets/03_2_ansibleplaybook_pma_mariadb.PNG)

![03_3_ansibleplaybook_pma_mariadb](assets/03_3_ansibleplaybook_pma_mariadb.PNG)

Next is Laravel

![03_4_ansibleplaybook_laravel](assets/03_4_ansibleplaybook_laravel.PNG)

![03_5_ansibleplaybook_laravel](assets/03_5_ansibleplaybook_laravel.PNG)

The next one is Code Igniter

![03_8_ansibleplaybook_ci](assets/03_8_ansibleplaybook_ci.PNG)

![03_9_ansibleplaybook_ci](assets/03_9_ansibleplaybook_ci.PNG)

And then Wordpress

![03_10_ansibleplaybook_wp](assets/03_10_ansibleplaybook_wp.PNG)

![03_11_ansibleplaybook_wp](assets/03_11_ansibleplaybook_wp.PNG)

Then YII2.0

![03_12_ansibleplaybook_yii](assets/03_12_ansibleplaybook_yii.PNG)

![03_13_ansibleplaybook_yii](assets/03_13_ansibleplaybook_yii.PNG)
