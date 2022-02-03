# TUGAS BESAR

**RACHMAD SAFLYI & ALIFIA**

------

## Step by Step

------

SKEMA :
![00_scheme](https://user-images.githubusercontent.com/93419670/152255035-888125d0-5738-484c-97c8-9e1bb98aa345.png)

------

membuat  lxc dan konfigurasi IP of setiap

![Capture1](https://user-images.githubusercontent.com/93419670/152255278-09469dc9-9888-47eb-91ac-17934951a558.PNG)

install open ssh server dalam semua lxc diatas, lalu masuk ansible

```
apt install openssh-server
```

Go to

```
cd ~/ansible/TUBES
```

masuk ke 'nano hosts' untuk mengklasifikasi setiap lxc

![Capture2](https://user-images.githubusercontent.com/93419670/152255603-580ac68d-a6f6-4493-b606-34b79006f1d1.PNG)

lalu

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

setelah itu lakukan

```
cd /roles/ci/tasks
nano main.yml
```

![Capture11](https://user-images.githubusercontent.com/93419670/152260524-70209b5a-7386-4361-8a34-c4cb0f5eb556.PNG)

masuk dalam app.conf

```
cd ../templates
nano app.conf
```

![Capture12](https://user-images.githubusercontent.com/93419670/152276453-aedfa8bd-4cc4-4bfb-beb0-9219b8a751ef.PNG)


setelah selesai lakukan..

```
cd ../handlers
nano main.yml
```

![Capture53](https://user-images.githubusercontent.com/93419670/152278090-464ed572-6bc3-4b84-8362-42bb7708ceeb.PNG)

ansible Code Igniter selesai, lalu

```
cd ../../
cd php/tasks
nano main.yml
```

![Capture20](https://user-images.githubusercontent.com/93419670/152278297-4e25b5b6-a93e-450b-bdb7-19b04b016366.PNG)


```
cd ../handlers
nano main.yml
```

![Capture54](https://user-images.githubusercontent.com/93419670/152278470-2811b69f-f287-4d33-83be-03718b71602b.PNG)

ansible php selesai, lanjutkan ke Laravel

```
cd ../../
cd lv/tasks
nano main.yml
```

![Capture15](https://user-images.githubusercontent.com/93419670/152278814-84725d21-b51d-428e-b346-1b94a73931b4.PNG)

```
cd ../templates
nano env.template
```
![Capture16](https://user-images.githubusercontent.com/93419670/152288789-d152a0bb-1391-41a4-af4f-32c1c9e6cb85.PNG)
![Capture17](https://user-images.githubusercontent.com/93419670/152288799-66ac6163-7760-4fe8-8f15-1853b29c18f5.PNG)

Then go to

```
nano lv.conf
```

![Capture18](https://user-images.githubusercontent.com/93419670/152288974-3b156395-8aa4-41d7-8b5c-cd05e891b743.PNG)

After configuring in templates, we go to handlers

```
cd ../handlers
nano main.yml
```

![Capture53](https://user-images.githubusercontent.com/93419670/152289122-ceaffffe-1e4f-4592-81a7-af5f22c438fb.PNG)

The ansible for Laravel is done, the next one is mariadb, first we go to

```
cd ../../../
cd db/tasks
nano main.yml
```
![Capture13](https://user-images.githubusercontent.com/93419670/152289301-fc4f5c9e-71de-41af-9d4d-41c145fba184.PNG)

Then go to templates

```
cd ../templates
nano my.cnf
```

![Capture14](https://user-images.githubusercontent.com/93419670/152289361-133744d1-81d8-4b43-b0b4-0f9f3872cbeb.PNG)

Next go to handlers

```
cd ../handlers
nano main.yml
```

![Capture54](https://user-images.githubusercontent.com/93419670/152289400-4e9755f1-11cf-4bf2-a6ad-d42f0151780c.PNG)

The ansible for database is done, the next one is for PHP My Admin, just like before we need to go to

```
cd ../../
cd pma/tasks
nano main.yml
```

![Capture21](https://user-images.githubusercontent.com/93419670/152289486-bd0dde16-b0bf-4b35-9119-b23d10bdf497.PNG)


Then go to

```
cd ../templates
nano lxc_mariadb.conf
```
![Capture22](https://user-images.githubusercontent.com/93419670/152289562-52478608-a382-41ef-9a60-78f258c10e29.PNG)

Then go to handlers

```
cd ../handlers
nano main.yml
```

![image](https://user-images.githubusercontent.com/93419670/152289759-2d885d79-42e2-4c03-997c-9c6be2180540.png)


Yay the ansible for PHP My Admin is done, next one is YII2.0

```
cd ../../
cd yii/tasks
nano main.yml
```

![Capture25](https://user-images.githubusercontent.com/93419670/152289913-17174975-f795-4ea6-b201-780142be586a.PNG)

The next one we go to templates

```
cd ../templates
nano yii.conf
```

![Capture30](https://user-images.githubusercontent.com/93419670/152290023-80d83670-62ae-45c1-9a7d-3aa242041852.PNG)

Then we go to handlers

```
cd ../handlers
nano main.yml
```

![image](https://user-images.githubusercontent.com/93419670/152290164-7add95c6-3cd6-4c92-85a8-804adf8e7d4f.png)


The ansible for YII2.0 is done, so the next one is Wordpress

```
cd ../../
cd wp/tasks
nano main.yml
```

![image](https://user-images.githubusercontent.com/93419670/152290339-8937e1e5-c32f-4a29-ad51-2b01387684f8.png)


Then go to templates

```
cd ../templates
nano wp.conf
```

![Capture31](https://user-images.githubusercontent.com/93419670/152290374-55ff1a7e-fb67-43a9-937b-c91e9bdd54ef.PNG)


Then

```
nano wp.local
```

![Capture27](https://user-images.githubusercontent.com/93419670/152290420-c8f4aa22-6005-4184-9e62-f7bedb3a399b.PNG)

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


