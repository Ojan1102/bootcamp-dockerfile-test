Pertama saya akses vm root@192.168.100.113

![image](https://user-images.githubusercontent.com/71244380/217472841-5069a34c-3510-430f-820d-efe02c4175eb.png)

kemudian install docker sebelumnya mengedit file dengan menggunakan "vim /etc/selinux/config" pada bagian SELINUX=permissive,
setelah di save saya membuat repository docker-ce, lalu install docker-ce kemudian jalankan service dockernya, lalu setting firewald agar port 2375/tcp dibuka.

Edit file /lib/systemd/system/docker.service tambahkan -H tcp://0.0.0.0:2375

![image](https://user-images.githubusercontent.com/71244380/217477455-178d15a2-f4b0-4c6e-98d4-fe32fe21218e.png)

setelah disave maka saya reload daemonnya dengan command "systemctl daemon-reload" lalu restart service dockernya dengan command "systemctl restart docker.service".
kemudian, saya membuat configure connectionnya pertama membuat folder /etc/docker/ lalu menambahkan file didalam folder tersebut dengan nama daemon.json yang isinya

![image](https://user-images.githubusercontent.com/71244380/217478925-169ebe87-85f4-4fb1-9b78-21381276417e.png)

setelah itu, saya restart dockernya dengan command "systemctl restart docker.service" sebelum melakukan pull saya login docker dengan command
"docker login 192.168.100.250:8086" untuk pull request,dan login untuk pushnya juga dengan command "docker login 192.168.100.250:8087".
Tahap selanjutnya, saya membuat pull req dengan command "docker pull 192.168.100.250:8086/httpd:latest" 
ketika sudah di pull maka saya cek docker imagenya. 
Ketika sudah ada image nya, saya lanjutkan dengan membuat container dengan command "docker run --name testfauzan -p 8081:80 -d 192.168.100.250:8086/httpd:latest"
cek containernya lalu curl localhost:8081 bila ingin mengecek pada browser localhost maka dengan link http://192.168.100.113:8081/
