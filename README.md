# Bank Telemarketing Campaign
-----------

## Business Understanding
Sebuah lembaga keuangan di Portugal sedang berupaya meningkatkan strategi pemasarannya untuk produk deposito berjangka. Mereka telah menjalankan beberapa kampanye pemasaran sebelumnya, namun tingkat keberhasilannya masih belum optimal.

Term deposito merupakan bentuk investasi yang memiliki jangka waktu dan *return* tertentu dalam penyimpanannya. *Return* merupakan bunga dari hasil lama dan besaran penyimpanan yang dilakukan, bunga ini yang disebut sebagai penghasilan bagi mereka yang menanamkan modal. Sebagai pihak yang berperan penting atas jalannya roda perekenomian, savings merupakan salah satu aspek penting yang berpengaruh dalam pergerakan ekonomi dan finansial suatu negara. Deposito/simpanan digunakan bank sebagai sumber dana/modal yang akan disalurkan kepada pihak/nasabah lain, dengan hal ini dapat membantu nasabah lain dalam mendorong perekonomian mereka yang juga bisa berdampak pada kesejahteraan negara.

Bagi pihak bank sendiri, adanya modal dari sistem deposito membantu mereka dalam menjalankan operasional seharinya dan juga memberikan keuntungan dari *return* bunga oleh peminjam. Selain itu, keuntungan lainnya dapat meningkatkan liquiditas serta kestabilan bank itu sendiri. Hal ini berarti semakin banyak modal dari *savings* yang masuk maka akses untuk mengabulkan permintaan pencairan dari nasabah semakin mudah. Oleh karena itu, untuk mencapai tujuan yang diharapkan pihak bank melakukan *campaign* guna meningkatkan jumlah nasabah yang melakukan *savings* dengan pembukaan deposito.

## Problem
Berdasarkan hasil analisis dataset yang diberikan, bisa dikatakan *campaign* manual yang dilakukan dengan cara menghubungi *client*/nasabah satu per satu kurang efisien. Hal ini karena selain memakan banyak waktu dan *cost*, hasil yang diharapkan mungkin bisa dikatakan tidak sebanding dengan usaha yang dikeluarkan untuk biaya *campaign* itu sendiri (seperti yang dianalisis hanya 11% mereka yang menerima).

**Asumsikan**:
  - Biaya tiap 1 menit panggilan: 0.19 euro<sup>1</sup>, rata-rata durasi panggilan berdasarkan analisis 180 detik atau 3 menit, maka <u>biaya 1 panggilan: 0.57 euro</u>. Jika sebagian besar *client* dipanggil sebanyak 2x dalam 1 periode per tahun *campaign* (median rata panggilan), <u>maka total biaya yang dikeluarkan untuk 1 *client*: 1.14 euro</u>.
  - Apabila 11% dari total *client* bank (41.176) adalah 4639 yang menerima penawaran maka <u>minimum profit yang didapat sebesar (5.32 * 4639 = 24.679 euro)</u>, <u>sedangkan total biaya yang dikeluarkan untuk menghubungi keseluruhan client (1.14 * 41176 = 46.940 euro)</u>.

Terlihat bahwa rasio biaya *campaign* yang dikeluarkan 2x lebih besar dibandingkan income yang masuk. Oleh karena itu, **apabila persentase penerimaan *campaign* bisa ditingkatkan, maka profit yang masuk lebih besar dan dapat menutupi biaya yang dikeluarkan.**

## Goals and Strategy
Berdasarkan masalah yang telah dipaparkan, agar *possibility* persentase penerimaan *campaign* meningkat, beberapa hal yang perlu dilakukan:
1. Mengetahui dan menganalisis ciri/pola berdasarkan informasi *client*, informasi *campaign* sebelumnya, dan infomasi kondisi ekonomi saat itu terhadap penerimaan penawaran.
2. Membangun model *machine learning* klasifikasi untuk mengetahui besaran persentase (probabilitas) setiap *client* dalam menerima penawaran.
3. Melakukan analisis segmentasi *client*/nasabah berdasarkan probabilitas setiap *client* dan penerapan strategi yang tepat pada setiap *segment* *client*.
- Contoh strategi promo berdasarkan segmentasi *client*:
    - Segmen *medium*: program yang memberikan insentif tambahan bagi *client* yang membuka deposito.
    - Segment *low*: Perusahaan dapat mengadakan program seperti bundling package (produk *non-banking*) yang bisa diarahkan kepada tiap karakteristik dari *low-segmented client* dengan rincian sebagai berikut**:
      - Melakukan bundling promo liburan/potongan tiket pesawat (tentunya disesuaikan dengan besaran dan lama jangka waktu pembukaan deposito) atau melakukan kolaborasi program *credit*, dengan mendapatkan tambahan limit *credit*.
      - Mendapatkan potongan/bebas premi asuransi untuk penyimpanan dalam jangka waktu dan besaran tertentu.

## Data Overview 
Dataset diambil dari UCI Machine Learning Repository, yang merupakan *real data* dari salah satu Portugal Retail Bank oleh S'ergio Moro, Paulo Cortez, dan Paulo Rita (tahun 2014).

Data ini berisi *record direct marketing campaign* dari sebuah institusi bank melalui panggilan telephone (May 2008 to November 2010), dengan nama '**bank-additional-full.csv**'

Terdapat 20 fitur dengan 41.188 data *client*. Beberapa informasi fitur yang diberikan sebagai berikut:
- *Client Profile* : Berisi informasi *client*/nasabah.
- *Campaign* : Berisi informasi mengenai *campaign* sekarang maupun *campaign *sebelumnya.
- *Social & Economic Situation* : Berisi informasi mengenai kondisi ekonomi saat itu.

[Link Dataset](https://archive.ics.uci.edu/dataset/222/bank+marketing)

## Data Preprocessing
Sekarang kita masuk kedalam process data cleaning dan data preprocessing, tahap ini adalah tahap membersihkan data, memilih kolom yang digunakan dan mempersiapkan data untuk keperluan prediksi. berikut process cleaning dan preprocessing nya:

1. Handling Unknown -> Pada tahap analisis, dilakukan penyebaran pada nilai unknown kesetiap karakteristik kategorinya, dikarenakan persentase pengaruh unknown tidak terlalu besar sedangkan pada penerapan ke mesin,unknown dianggap sebagai kategori terpisah, hal ini mencegah bias mesin dalam mempelajari ciri client.<br>
2. Check & remove Duplicate -> terdapat 12 duplikasi data -> Drop, karena dapat menyebabkan mesin mempelajari data yang sama berulang kali dan dapat menyebabkan overfit dan bias penentuan mesin terhadap bobot/signifikansi ciri client.
3. Check Anomaly -> Semua nilai data dianggap relevan. 
4. Handling outliers -> Tidak dilakukan treatment apapun, karena karena menurut kami pada dataset ini outlier nya dapat memberikan insight yang baik bukan mengganggu analysis.
5. Rename Column & Value -> Tujuan mempermudah dalam pembacaan dan penginterpretasian data.

## Analysis Result
[Dashboard Link](#https://public.tableau.com/app/profile/gian.habli.maulana/viz/BankMarketingCampaignDashboard_17273603145210/Dashboard)

<img src="https://github.com/user-attachments/assets/3cbcd883-5888-4429-8505-16e5a566f8f1" width=880/>

<br>

**External Factor that gives impact to the decision of client will accept the offering or not**

- Kondisi ekonomi mengindikasikan adanya inflasi.
- Nasabah yang termasuk dalam rentang usia tua (kategori pensiun) > 65 memiliki acceptance rate terhadap penerimaan pembukaan deposito lebih besar serta nasabah yang berstatus 'student' masih berpotensi untuk menerima penawaran pembukaan tabungan/deposito.
- Penawaran pembukaan tabungan/deposito bisa lebih diprioritaskan kepada mereka yang masih berstatus single dan mereka yang belum pernah memiliki riwayat pembayaran pinjaman gagal (artinya, nasabah tidak pernah mengalami kesulitan pemenuhan kebutuhan seharinya sehingga memiliki potensi besar untuk melakukan savings).
- Menghubungi kembali nasabah yang pernah menerima campaign sebelumnya.
- Banyak melakukan campaign diawal dan diakhir bulan, karena tingkat acceptance rate dikedua bulan besar dibandingkan pertengahan bulan.
<br>

## Business Prediction Sytem
Tahap pembangunan sistem dengan penerapan model *Machine Learning*. Sistem yang dibangun merupakan sistem yang dapat memprediksi probabilitas setiap client dalam persentase. Persentase probabilitas ini yang dapat digunakan perusahaan dalam membantu keputusan perusahaan untuk melakukan penawaran terhadap client tersebut atau diperlukan penerapan strategi yang tepat. 

## Feature Selection
Berikut fitur yang dianggap dapat membantu model dalam mengenali ciri dari client:<br>

| Attribute | Data Type | Description |
| --- | --- | --- |
| age | Integer | Usia client |
| job | String | Pekerjaan client |
| marital | String | Status pernikahan client |
| education | String | Status pendidikan client |
| default | String | Apakah client pernah gagal bayar/macet ? |
| housing | String | Apakah client mempunyai pinjaman untuk pembayaran rumah ? |
| loan | String | Apakah client mempunyai pinjaman pribadi ? |
| contact | String | Jenis komunikasi yang digunakan |
| month | String | Bulan terakhir kali melakukan panggilan dengan client pada campaign tahun ini  |
| day_of_week | String | Hari terakhir kali melakukan panggilan dengan client |
| emp.var.rate | Float | Employment Variation Rate : Indikator rate tenaga kerja (%) (indikator quarter) |
| cons.price.idx | Float | Consumer Price Index : Indikator rata-rata perubahan harga barang & jasa. Semakin tinggi CPI, indikasi *Higher Inflation*. (indikator bulanan)|
| cons.conf.idx | Float | Consumer Confidence Index : Indikator tingkat kepercayaan customer mengenai kondisi perekonomian saat ini. Berpengaruh pada tingkat konsumsi rakyat. (indikator bulanan)|
| euribor3m | Float | Euribor 3 Month Rate : Tingkat suku bunga 3 bulan terakhir (indikator harian) |
| nr.employed | Float | Jumlah tenaga kerja (indikator quarter)  |
| y | String | Apakah client menerima penawaran "Term Deposito" ? |


## Metric Evaluation
Dalam penerapan *Machine Learning* memiliki kemungkinan *error* atas prediksi yang dirincikan seperti berikut:
<br>
<br>

|  | Tidak Menerima Tawaran (0) | Menerima Tawaran (1) |
| --- | --- | --- |
| **Tidak Menerima Tawaran (0)** | **True Negative (TN)** | **False Positif (FP)** |
|  | Model memprediksi *client* tidak menerima tawaran deposito, | Model memprediksi *client* menerima tawaran deposito,
|  | dan *client* tidak menerima tawaran. | tetapi *client* tidak menerima tawaran deposito.
| **Menerima Tawaran (1)** | **False Negatif (FN)** | **True Positif (TP)** |
|  | Model memprediksi *client* tidak menerima tawaran deposito, | Model memprediksi *client* menerima tawaran deposito,
|  | tetapi *client* menerima tawaran. | dan *client* menerima tawaran deposito.



---



| **Tipe error** | **Konsekuensi** |
| --- | --- |
| False Positive | Kehilangan biaya *marketing* dan pemborosan waktu. |
| False Negative | Kehilangan *potensial revenue* |

<br>

- Biaya *marketing cost* (False Positive) :
  - Biaya tiap 1 menit panggilan: 0.19 euro[<sup>1</sup>](https://digital-strategy.ec.europa.eu/en/policies/intra-eu-calls#:~:text=Europeans%20pay%20lower%20and%20limited,06%20per%20SMS%20(%2B%20VAT)), rata-rata durasi panggilan berdasarkan analisis 180 detik atau 3 menit, maka <u>biaya 1 panggilan: 0.57 euro</u>. Jika sebagian besar client dipanggil sebanyak 2x dalam 1 periode per tahun campaign (median rata panggilan), <u>maka total biaya yang dikeluarkan untuk 1 client: 1.14 euro</u>.

- Kehilangan *potential profit* (False Negative)
  - Apabila saat itu (2014) rata rate deposito: 0.2%[<sup>2</sup>](https://tradingeconomics.com/portugal/interest-rate), rata rate pinjaman: 5.52%[<sup>3</sup>](https://tradingeconomics.com/portugal/bank-lending-rate) dalam 1 tahun.
  - Jika diasumsikan client mengambil paling sedikit minimum deposito: 100 euro[<sup>4</sup>](https://withportugal.com/en/immigration/depositos-portugal) dalam 1 tahun, maka <u>profit minimum yang bisa dihasilkan 1 client: 5.32 euro**</u>
  <br>
  >**<b>Profit : ( lending rate - deposito rate ) * minimum deposito</b>

<br>

Dikarenakan ciri data mayoritas berpusat pada *client* yang menolak tawaran, maka untuk model melakukan prediksi terhadap *client* yang menerima, kemungkinan besar akan sulit, artinya potensi kemungkinan model salah memprediksi *client* yang sebenarnya memiliki sebagian ciri untuk menerima tawaran, besar.

Oleh karena itu, diperlukan minimalisir *error False Negative* terhadap prediksi model, untuk meminimalisir nilai tersebut artinya model memerlukan hasil prediksi dengan *Recall* besar.

<img src="https://cdn-images-1.medium.com/v2/resize:fit:800/1*BiB0AmdCN_O5Gi8d6j2ixg.png" width=120/>

<br>

Hasil prediksi tersebut akan diketahui seberapa besar keuntungan yang dapat diperoleh dari penerapan ML. `Namun, recall besar yang berhasil diperoleh tidak menjamin yang diperoleh menghasilkan profit`. Oleh karena itu,diperlukan *metrics* tambahan sebagai *metrics* tolak ukur atas %*Recall* yang dihasilkan.

**Profit Metrics**, merupakan *metrics* yang akan dipakai sebagai tolak ukur profit yang dihasilkan dengan interpretasi hasil *metrics* merupakan rata peningkatan profit minimum per *client*.

<img src="https://github.com/user-attachments/assets/e6c822ac-1407-4d73-b350-9b6b192acf93
" width=450/>

---------
<sup>1</sup>https://digital-strategy.ec.europa.eu/en/policies/intra-eu-calls#:~:text=Europeans%20pay%20lower%20and%20limited,06%20per%20SMS%20(%2B%20VAT).<br>
<sup>2</sup>https://tradingeconomics.com/portugal/interest-rate<br>
<sup>3</sup>https://tradingeconomics.com/portugal/bank-lending-rate<br>
<sup>4</sup>https://withportugal.com/en/immigration/depositos-portugal


## Model Limitation

Informasi *client* terkait sudah pernah dihubungi atau belum. Apakah *client* menerima penawaran sebelumnya atau tidak, tidak menjadi pengaruh bagi sistem dalam mengambil keputusan.

Model hanya mempelajari ciri *client* berdasarkan karakteristik dari: <br>
- *Profile client*</u>  ('age', 'job', 'marital', 'education'),<br>
- *Financial situation client*</u> ('default', 'housing', 'loan'),<br>
- *Economic stability*</u> ('emp_var_rate', 'cons_price_idx', 'cons_conf_idx', 'euribor3m', 'number_employed'),
- dan beberapa informasi kampanye sebelumnya ('contact', 'month', 'day_of_week').

<br>

Model yang sudah dibangun dapat digunakan ketika perusahaan memerlukan sistem yang dapat memprediksi kemungkinan penerimaan setiap client terhadap campaignnya sebelum campaign telemarketing dilakukan, <u>karena hasil model berupa persentase probability terhadap penerimaan campaign.</u>

Namun, **kelemahan dalam model ketika persentase prediksi berada pada range > 50%.** Pada range ini ada kemungkinan model akan memprediksi client menerima terhadap client yang sebenarnya berpotensi menolak. <br>

Oleh karena itu <u>untuk mengatasi kelemahan model, perusahaan dapat melakukan penawaran untuk meningkatkan kemungkinan client menerima</u> (*jika diasumsikan terjadi kesalahan pada prediksi > 50% artinya client tersebut merupakan client berpotensi menolak*)<br>

Untuk perusahaan dapat meningkatkan kemungkinan penerimaan client, maka perusahaan perlu melakukan beberapa strategi marketing yang tepat, <u>guna mempermudah perusahaan dalam menerapkan strategi tersebut kepada client yang tepat, client dibagi menjadi segment low dan medium</u>, dengan rincian:<br>

- *Low-segmented client*: client dengan persentase < 80%
- *Medium-segmented client*: client dengan persentase >= 80%

<br>

Beberapa kemungkinan kesalahan prediksi lainnya seperti:
- Pekerjaan *blue-collar* kecenderungan besar akan <u>diprediksi sebagai client berpotensi menolak penawaran</u> (yang kenyataan masih ada client dengan pekerjaan sama yang menerima penawaran).
- Maret, Oktober, dan Desember <u>berpotensi diprediksi sebagai client yang akan menerima</u> (yang kenyataan dibulan tersebut masih ada beberapa client yang menolak penawaran).
- Apabila tingkat suku bunga mendekati 0 (semakin mendekati 0) maka <u>kemungkinan model memprediksi sebagai client menerima</u> (*dikarenakan kondisi ekonomi dengan indikasi rendah merupakan indikasi sebagian besar client menerima*).
- Apabila tingkat tenaga kerja berada pada rentang < -1.5, <u>kemungkinan model memprediksi sebagai client yang kecenderungan akan menerima</u> (*dikarenakan kondisi ekonomi dengan indikasi rendah merupakan indikasi sebagian besar client menerima*)

----


