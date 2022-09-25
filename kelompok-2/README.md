# Kelompok 2
**Anggota**
- Ade Muhammad Safari
- Angga Nugraha
- Ivanka Alan Muhammad

# Premptive Setup
- Reverse Proxy ke 3 port (3000[frontend], 5000[backend], 8080[jenkins])
- DNS Cloudflare ke studentdumbways.my.id (kelompok2.;api.kelompok2.;jenkins.kelompok2)
- SSL Certbot
- Installasi Docker via BASH

# Install Docker via BASH Script

`#sh/`

# Deploy Application on top Docker

## 1. Cloning Repository

Disini, kita menarik repo dari _Wayshub-Frontend_ dan _Wayshub-backend_
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Deploy%20frontend%20on%20top%20docker/git%20clone%20fe.png?raw=true)

## 2. Setup Dockerfile & App

Disini kita membuat `dockerfile` agar aplikasi dapat dibuild sebagai _Docker Image_
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Deploy%20frontend%20on%20top%20docker/docker%20make%20dockerfile.png?raw=true)

**DockerFile Front-End**
![image](https://user-images.githubusercontent.com/111945026/191699665-44094d9d-bca1-40e8-b166-17b5a531a6fb.png)

**DockerFile Back-End**
![image](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Deploy%20backend%20on%20top%20docker/media/docker1.png?raw=true)

> Untuk frontend, konfigurasi dengan backend harus dijalankan sebelum di build.
> Untuk backend, semua konfigurasi harus dijalankan sebelum di build.

**config.json**
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Deploy%20backend%20on%20top%20docker/media/be2.png?raw=true)

## 3. Setup Docker-compose

Agar kita dapat menjalankan semua aplikasi sekaligus dengan 1 command, kita bisa gunakan `docker-compose` untuk menjalankan semuanya
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Deploy%20backend%20on%20top%20docker/media/be3.png?raw=true)

> Frontend akan berjalan di port 3000 (- 3000:3000)
> Frontend + Backend berjalan dengan image yang sudah di push sebelumnya (ivankalan12/wayshub-*)
> Backend akan berjalan di port 5000
> Backend + database sudah di konfigurasi sebelumnya

## 4. Build Application as Image

Setelah dockerfile dibuat, kita bisa langsung build aplikasi sebagai image dan deploy image tersebut.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Deploy%20frontend%20on%20top%20docker/docker%20build%20dockerfile.png?raw=true)

Kita juga bisa build semua isi `docker-compose` menggunakan build.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Deploy%20backend%20on%20top%20docker/media/be4.png?raw=true)

Hasil build bisa kita check melalui `docker images`.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Deploy%20backend%20on%20top%20docker/media/be6.png?raw=true)

## 5. Push Docker ke Docker Hub

Sebelum kita bisa melakukan push ke Docker Hub, kita harus login ke akun Docker terlebih dahulu.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Deploy%20frontend%20on%20top%20docker/docker%20login.png?raw=true)

Lalu, kita gunakan command `docker push` untuk melakukan push ke repository
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Deploy%20frontend%20on%20top%20docker/docker%20push%20image%20to%20docker%20hub.png?raw=true)


# CI/CD Jenkins & Pipeline

## Install Jenkins

Sebelum kita bisa menggunakan CI/CD melalui pipeline, kita harus gunakan _Jenkins_ untuk semua konfigurasinya.
Pertama, kita pull image dari _Jenkins_ di _Docker Hub_.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/jenkins.png?raw=true)

Setelah itu, kita jalankan _Jenkins_ untuk melakukan konfigurasi awal.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/jenkins2.png?raw=true)

Jika sudah berjalan, kita butuh password yang digenerate oleh _Jenkins_ untuk melakukan login user "admin", password tersebut bisa kita cek di logs dari docker _Jenkins_ yang kita jalankan.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/jenkins3.png?raw=true)

Lalu kita akses Jenkins melalui `IP server:8080` untuk setup pertama.
Karena kita hanya ingin menggunakan plugin sshagent, kita pilih opsi _Select to Install Plugins_.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/jenkins4.png?raw=true)
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/jenkins5.png?raw=true)

Setelah itu, jika kita lanjut maka akan mulai berjalan instalasi _Jenkins_ disini.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/jenkins6.png?raw=true)

Pada saat instalasi selesai, kita akan diminta untuk mengisi "Admin User" selain user "admin". Disini bisa kita isi sesuai dengan keinginan kita.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/jenkins7.png?raw=true)

Setelah itu kita isi Jenkins URL dengan URL DNS Cloudflare yang sudah disediakan.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/jenkins8.png?raw=true)
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/jenkins9.png?raw=true)

Jika reverse proxy sudah benar, maka bisa diakses melalui URLnya langsung
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/rpjenkins3.png?raw=true)

## Config SSH untuk Pipeline

Jika kita ingin menjalankan _pipeline_ nanti, maka kita harus membuat credential baru sebagai identitas untuk menjalankan perintah _pipeline_ di appserver.

Kita masuk ke `Dashboard > Manage Jenkins` lalu masuk ke `Manage Credentials`
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/sshj.png?raw=true)

Kita pilih store `Jenkins` lalu kita akan masuk ke Systemnya, disini kita pilih lagi `Global Credentials`
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/sshj2.png?raw=true)
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/sshj3.png?raw=true)

Disini kita akan masuk ke menu Credentials yang ada, karena saat ini belum ada apa-apa, kita bisa tambahkan credentials dengan memilih `Add Credentials`
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/sshj4.png?raw=true)

Kita isi formnya sesuai dengan kebutuhan kita.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/sshj5.png?raw=true)

> ID kita isi _appserver_ karena credential ini akan digunakan untuk appserver
> Username diisi sesuai dengan 'user'@appserver
> PrivateKey diisi keygen ssh yang sudah di generate di appserver
> Lightweight Reload dimatikan agar jenkins reload lebih dalam

Jika sudah, berhasil terbuat credential yang sudah jadi.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Git%20config%20Jenkins/media/sshj6.png?raw=true)

## Scripting Pipeline

- Membuat Jenkinsfile didalam repo masing-masing.
- Integrasi webhook repo kedalam jenkins.
- Jika sudah, bisa di push ke repo agar Jenkins dapat di trigger.

**Implementasi JenkinsFile**
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/SCRIPT%20CI-CD%20Jenkinsfile/15.png?raw=true)
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/SCRIPT%20CI-CD%20Jenkinsfile/16.png?raw=true)

**Hasil Pipeline**
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/SCRIPT%20CI-CD%20Jenkinsfile/19.png?raw=true)
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/SCRIPT%20CI-CD%20Jenkinsfile/21.png?raw=true)

**Script CI/CD Backend**

```
def branch = "main"
def rname = "origin"
def dir = "~/wayshub-backend/"
def credential = 'appserver'
def server = 'kel2@103.183.74.32'
def img = 'ivankalan12/wayshub-be'
def cont = 'wayshub-be'

pipeline {
    agent any

    stages {
        stage('Repository Pull') {
            steps {
                sshagent([credential]){
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    echo "Pulling Wayshub Backend Repository"
                    cd ${dir}
                    docker container stop ${cont}
                    docker image prune
                    git pull ${rname} ${branch}
                    exit
                    EOF"""
                }
            }
        }

        stage('Building Docker Image') {
            steps {
                sshagent([credential]){
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    echo "Building Image"
                    cd ${dir}
                    docker build -t ${img}:${env.BUILD_ID} .
                    exit
                    EOF"""
                }
            }
        }

        stage('Image Deployment') {
            steps {
                sshagent([credential]){
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${dir}
                    docker tag ${img}:${env.BUILD_ID} ${img}:${env.BUILD_ID}-latest
                    docker container run -d ${cont}
                    exit
                    EOF"""
                }
            }
        }

        stage('Pushing to Docker Hub (ivankalan12)') {
            steps {
                sshagent([credential]){
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${dir}
                    docker image push ${img}:${env.BUILD_ID}-latest
                    exit
                    EOF"""
                }
            }
        }
        stage('Push Notification Discord') {
           steps {
                sshagent([credential]){
                    discordSend description: "wayshub-backend:" + BUILD_ID, footer: "Kelompok 2 - Dumbways.id Devops Batch 13", link: BUILD_URL, result: currentBuild.currentResult, scmWebUrl: '', title: 'Wayshub-backend', webhookURL: 'https://discord.com/api/webhooks/1019867961349132379/f5XTPLZWgUBN3-QZ0E-OkFQPXOJrGdj0LOjHMsQA8jfYC9mL5W1bt60mc_UbpLi88ceM'
                }
            }
        }
    }
}
```

## Notifikasi via Discord

**Notifikasi Repository Github**

1. Mengambil Webhook dari text-channel yang diinginkan.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20github%20discord/1.png?raw=true)
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20github%20discord/2.png?raw=true)

2. Masuk kedalam web repo github yang diinginkan lalu akses `Settings > Webhooks`
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20github%20discord/3.png?raw=true)

3. Lalu pilih `Add Webhook` lalu tambahkan URL Webhook discord tadi dan menambahkan '/github'
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20github%20discord/4.png?raw=true)
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20github%20discord/5.png?raw=true)

Hasil Notifikasi
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20github%20discord/6.png?raw=true)

**Notifikasi Job Jenkins**

1. Di _Jenkins_, kita install plugin `discordNotifier` dan `Post build task`.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20jenkins%20discord/1.png?raw=true)
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20jenkins%20discord/2.png?raw=true)

2. Aktifkan plugin dan restart _Jenkins_ agar plugin dapat berjalan.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20jenkins%20discord/3.png?raw=true)

3. Lalu buat project baru dengan Freestyle Project.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20jenkins%20discord/4.png?raw=true)

4. Tambahkan gitSSH repo yang diinginkan, lalu save projectnya.
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20jenkins%20discord/5.png?raw=true)
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20jenkins%20discord/6.png?raw=true)
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20jenkins%20discord/7.png?raw=true)

Hasil Notifikasi
![](https://github.com/ademuh/devops13-dumbways-ade/blob/main/Stage-2/kelompok-2/Webhook%20jenkins%20discord/8.png?raw=true)
