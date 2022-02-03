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

![Capture12](https://user-images.githubusercontent.com/93419670/152276453-aedfa8bd-4cc4-4bfb-beb0-9219b8a751ef.PNG)


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
![Capture53](https://user-images.githubusercontent.com/93419670/152277671-ff32e8bb-3469-4562-9d43-4f7fe4c3100a.PNG)


This is the configuration for vm.local

```
sudo nano /etc/nginx/sites-available/vm.local
```

![Capture33](https://user-images.githubusercontent.com/93419670/152277150-e5b77045-a18a-40eb-bc7e-39b8f4f89475.PNG)

![Capture34](https://user-images.githubusercontent.com/93419670/152277163-94b9403d-0a24-4bcd-b164-b70610b9e40d.PNG)

This is the configuration for hosts in VM

```
nano /etc/hosts
```

![Capture51](https://user-images.githubusercontent.com/93419670/152276716-c28235be-c88e-4536-97ae-53b14f84b739.PNG)

After we add the ansible, then we run them using

```
ansible-playbook -i hosts install-''.yml -k
```

The first one is mariadb

![Capture41](https://user-images.githubusercontent.com/93419670/152274636-7d41d771-307c-419a-96b3-e0c20ecd2f1c.PNG)

Next is Laravel

![Capture40](https://user-images.githubusercontent.com/93419670/152274703-43d5b4c9-e096-4297-b798-0bfc1965d8e6.PNG)

![Capture39](https://user-images.githubusercontent.com/93419670/152274724-048d3bc6-b0cc-4059-9d03-566ddd803c25.PNG)


The next one is Code Igniter

![Capture52](https://user-images.githubusercontent.com/93419670/152276633-bf1b3ebc-944f-4def-b478-6f269f8f03f8.PNG)

And then Wordpress

![Capture38](https://user-images.githubusercontent.com/93419670/152275024-a749119c-a2bc-4943-a3d0-0d99a5ec70a7.PNG)

![Capture37](https://user-images.githubusercontent.com/93419670/152275037-22cdc899-4e62-4c5f-9525-dafd1dd1d38b.PNG)

Then YII2.0

![Capture36](https://user-images.githubusercontent.com/93419670/152274945-44a19f50-ee19-4908-a01b-fa72ada05542.PNG)

![Capture35](https://user-images.githubusercontent.com/93419670/152274963-b7647ff0-c969-475a-a4eb-3c52bb1c8208.PNG)

Hasil

![Screenshot (9)](https://user-images.githubusercontent.com/93419670/152276850-b58874a3-e187-479e-8d1b-1aee1566f38c.png)
![Screenshot (10)](https://user-images.githubusercontent.com/93419670/152276875-1669127a-d106-46d3-88e6-e849e0fb98c1.png)
![Screenshot (11)](https://user-images.githubusercontent.com/93419670/152276887-d96cc5ce-0cdd-4f7f-8482-e8892ab13c52.png)
![Screenshot (12)](https://user-images.githubusercontent.com/93419670/152276894-392b3253-8cf5-4060-a40e-ffa2f3d8595a.png)
![Screenshot (13)](https://user-images.githubusercontent.com/93419670/152276949-03a5462e-8ee0-47cb-974e-a62b89751f3a.png)
![Screenshot (14)](https://user-images.githubusercontent.com/93419670/152276962-b00c1aef-ff9d-4821-a910-c2eed4fda8ad.png)
![Screenshot (15)](https://user-images.githubusercontent.com/93419670/152276968-affaf7f3-085f-4940-b83b-770b99a7da5a.png)
![Screenshot (16)](https://user-images.githubusercontent.com/93419670/152276976-7e8f89b8-1808-4db5-bda7-d0d23e11109d.png)


