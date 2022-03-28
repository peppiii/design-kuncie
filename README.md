
## Table of contents
<!--ts-->
   * [Solutions Architecture](#architecture)
   * [Cost Estimation](#cost)
   * [architecture consideration](#architecture_considideration) 
<!--te-->
 
 ## architecture
Solutions Architecture In this part, we require you to explain the architecture of your solutions. Please provide an architecture diagram (we recommend using Dr aw.io). We also require you to explain every services that you use in the solutions and how do you use them.

<a href="https://github.com/peppiii/design-kuncie/blob/main/images/images1.png"><img src="https://github.com/peppiii/design-kuncie/blob/main/images/images1.png" width= 100% alt="architecture"></a>

## cost
In this part, we require you to estimate the cost for first 12 month. Please put a table that itemize services that you use along with the
estimated cost for the first month. Feel free to put assumptions or notes for each services.

Untuk cost estimation saya memakai google cloud calculator berikut linknya :
https://cloud.google.com/products/calculator#id=e1182b3a-5a58-41b6-b849-e335711e8a17

Untuk penjelasannya sebagai berikut :

Di dalam table tersebut ada beberapa services yang saya gunakan, yaitu 
-	GKE : disini untuk menaruh semua service yang kita siapkan, yaitu service mymentor dan mymentee.
Disini saya mengansumsikan bahwa service mymentor dan mymentte ini menggunakan aplikasi react dan dibelakang service tersebut ada API yang bertugas untuk melakukan komunikasi ke backend

Region: Singapore
1,460 total hours per month
Machine Class: REGULAR
Instance type: n1-standard-2
Sustained Use Discount applied
USD 119.77
Operating System / Software: Free
Sustained Use Discount: 30% 
Effective Hourly Rate: USD 0.082
Estimated Component Cost: USD 119.77 per 1 month

-	CloudSql : disini untuk menyimpan data yang berhubungan transanksional

instances: 1
Instance type: db-standard-2
Location: Singapore
730.0 total hours per month
SSD Storage: 20.0 GiB
Backup: 0.0 GiB
USD 142.80

-	MemoryStore : disini untuk menyimpan activity session

Service Tier: basic
Instance Capacity: 1 GiB
Capacity Tier: M1
Location: asia-southeast1
USD 47.45

-	PubSub : disini untuk menstore live activity dimana nanti akan di consume ke beberapa service yang ada di gke

Volume: 50 GiB
Subscriptions: 10
Base cost: 644.141
Topic retention cost: 94.5
USD 738.64

biasanya setelah 1 bulan berjalan, team cloud akan mereview lagi arsitektur design service yang telah dibuat, apakah harus di downgrade atau di scale lebih besar lagi

## architecture consideration 
Architecture Consideration In this part we require you to explain your architecture based on several criterias below

- Operational Excellence 
How can your design help us to develop faster and operate easier? 

Untuk melakukan develop faster biasanya kita membuat script terraform or gcloud. 

- Security 
How does your design have ability to protect our assets from unwanted use? 

Untuk level security untuk menjaga assets dalam hal ini saya menggunakan service account dan disesuaikan dengan ACL yang dibuat

 
- Reliability 
How can your design run correctly and consistently in time of failure?

Untuk design ini biasanya kita sudah ada template di terraform atau di gcloud yang kita simpen di repo kita. Jadi jika terjadi insident failure kita bisa menggunakan template ini lagi untuk membuat lebih cepet. 

- Performance Efficiency 
How are your design able to use the computing resources efficiently?

Untuk performance ini saya biasanya melihat dari 2 sisi yaitu aplikasi dan server. Biasanya saya menggunakan Prometheus dari sisi cpu, memory, dan load. Dari sisi aplikasi saya menggunakan APM dari elasticsearch. Setelah dapat dari 2 sisi baru saya bisa menganalisa apakah design topologi yang kita buat sudah efficient atau belum

- Cost Optimization 
How are your design able to give us the lowest price point available while serving the requirements?

Untuk lowest price bisa cuman dari sisi kita biasanya tidak merekomendasi. Soalnya kalao untuk lowest price biasanya hanya digunakan di sisi development dan juga staging 
