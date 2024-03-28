**Context**

Sebuah perusahaan penyedia platform online untuk jual beli mobil bekas di UK yang dimana menyediakan wadah untuk mempertemukan pemilik mobil yang ingin menjual mobilnya dengan para calon pembeli potensial di Inggris.Untuk menjual mobilnya para calon penjual mobil diharuskan untuk login pada website, kemudian dapat langsung memasang mobil yang akan dijual dengan mengisi spesifikasi, foto, dan harganya.Harga yang diisi dibebaskan untuk masing-masing penjual mobil, namun dengan kebebasan ini tentunya akan ada banyak penjual terutama yang jarang ataupun baru pertama kali menjual mobil bekasnya kesulitan dalam menentukan harga yang tepat. Faktor terpenting dalam pembelian mobil bekas dimana calon pembeli cukup selektif adalah harga. Sebagaimana berlakunya hukum supply dan demand, jika harga terlalu tinggi dibandingkan harga mobil dengan spesifikasi yang hampir sama tentunya mobil tersebut akan sulit terjual, sebaliknya dengan harga yang terlalu rendah tentunya penjual mobil bekas tidak akan memperoleh profit yang seharusnya atau bahkan dibawah harga pasarnya, maka dari itu penetapan harga yang tepat merupakan hal yang sangat krusial.


**Problem Statement**

Platform yang disediakan perusahaan tentunya diharapkan dapat memudahkan para pemilik mobil untuk menjual mobilnya dengan profit yang diharapkan dan memudahkan pembeli mobil bekas untuk menemukan mobil bekas yang dinginkan dan tentunya dengan harga yang bagus.

Permintaan terhadap mobil bekas terus meningkat di Inggris pada beberapa quartal terakhir pada tahun 2023 Q1 - https://www.smmt.co.uk/2023/05/used-car-sales-q1-2023/ , Q2 - https://www.smmt.co.uk/2023/08/used-car-sales-q2-2023/ , Q3 - https://www.smmt.co.uk/2023/12/used-car-sales-q3-2023-2/ , Q4 - https://www.smmt.co.uk/2024/02/used-car-sales-q4-2023/ . Peningkatan ini disebabkan oleh beragamnya pilihan dan fleksibilitas yang ditawarkan oleh mobil bekas, ditambah dengan harga yang lebih terjangkau dibandingkan mobil baru, menjadikannya daya tarik tersendiri bagi konsumen dengan anggaran yang terbatas. Adanya mobil bekas akan memungkinkan konsumen untuk memilih kendaraan dengan model, ukuran, dan fitur yang diinginkan tanpa harus membayar harga penuh.

Dengan permintaan yang meningkat, tentunya akan semakin banyak juga mobil bekas yang beredar di pasaran. Untuk dapat tetap kompetitif di pasar, tentunya penentuan harga yang tepat merupakan suatu tantangan yang sangat penting yang harus diselesaikan.
Kemudian juga adanya kesulitan bagi penjual mobil bekas untuk menentukan harga mobil yang sesuai dan faktor apa saja yang menentukan harga nya.

**Goals**

Berdasarkan permasalahan tersebut, perusahaan ingin memiliki model Machine Learning prediktif yang nantinya dapat digunakan oleh calon penjual mobil untuk memprediksi harga pasar dari mobilnya berdasarkan spesifikasi mobilnya yang dapat membantu penjual mobil untuk menentukan harga yang sesuai dan kompetitif.
Dengan model ini tentunya perusahaan dapat menyediakan platform yang memudahkan dalam memberikan rekomendasi harga terbaik bagi calon penjual, dan tentunya pembeli juga menikmati dampak dari implementasi model ini dimana dengan model ini pembeli tidak perlu takut membeli mobil dengan harga mobil yang tidak wajar/terlalu mahal di platform kita, dengan demikian secara tidak langsung dapat berpengaruh positif pada brand perusahaan.Dengan memberikan pengalaman terbaik bagi kedua pihak, tentunya akan meningkatkan jumlah pengguna baik calon penjual maupun calon pembeli. Peningkatan pengguna ini tentunya akan memberikan keuntungan bagi perusahaan dimana traffic yang meningkat tentunya jumlah transaksi juga akan cenderung meningkat yang juga akan meningkatkan pendapatan perusahaan dari transaction/commission fee sebesar 1% dari nilai transaksi.Selain itu, sumber pendapatan yang juga akan meningkat adalah pendapatan dari additional service seperti iklan prioritas sebesar £10/bulan.


**Analytic Approach**

Karena tujuan kita adalah memprediksi harga, yang perlu dilakukan adalah melakukan analisis data untuk mengetahui faktor apa saja yang mempengaruhi harga jual mobil bekas, kemudian akan dilanjutkan dengan membangun sebuah model regresi yang dapat digunakan sebagai alat untuk membantu penjual mobil bekas pada platform perusahaan untuk memprediksi harga yang dapat membantu dalam menentukan harga jual mobil agar memiliki harga yang kompetitif di pasar.

**Metric**

Pada umumnya untuk regresi, kita bisa menggunakan metric seperti MAE,RMSE,R2,MAPE,dan MedAE.Pemilihan metric ini berdasarkan karakteristik datanya.Evaluasi metrik yang dapat digunakan jika memiliki banyak outlier adalah MedAE karena berdasarkan https://scikit-learn.org/stable/modules/model_evaluation.html#median-absolute-error:~:text=3.3.4.6.-,Median%20absolute%20error,-%C2%B6 metric ini robust terhadap outlier,RMSE(jika tidak ada outlier). Penggunaan MedAE ini robust terhadap outliers, dan untuk MedAE hasil errornya didapat dari median absolut errornya.Untuk mempermudah interpretasi MedAE berdasarkan https://help.pecan.ai/en/articles/6456388-model-performance-metrics-for-regression-models#:~:text=Percentage%20Error%20(RMSPE)-,Median%20Absolute%20Percentage%20Error%20(MdAPE),-Median%20Absolute%20Percentage kita dapat membuat custom metric yaitu MdAPE yang merupakan persentase MedAE, RMSE adalah nilai rata-rata error kuadrat yang setelah itu di akarkan agar lebih mudah untuk dipahami. Selain itu kita juga akan menggunakan R2 score yang dapat mengukur kemampuan model dalam menjelaskan target variabel menggunakan variabel dependennya.Semakin kecil nilai RMSE, dan MedAE yang dihasilkan, berarti model semakin akurat dalam memprediksi harga sewa sesuai dengan limitasi fitur yang digunakan. Sebaliknya semakin besar nilai R-Squared yang memiliki nilai antara 0-1, maka semakin baik model tersebut.
Rumus:
- MedAE
$$\text{MedAE}(y, \hat{y}) = \text{median}(\mid y_1 - \hat{y}_1 \mid, \ldots, \mid y_n - \hat{y}_n \mid).$$
- RMSE
$$\text{RMSE}(y, \hat{y}) = \sqrt{\frac{\sum_{i=0}^{N - 1} (y_i - \hat{y}_i)^2}{N}}$$
- R2
$$R^2(y, \hat{y}) = 1 - \frac{\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y})^2}$$


** Limitation **

- Model dilatih menggunakan dataset harga listing (belum terjual) yang ditentukan oleh tiap pemilik mobil, dimana hanya berdasarkan pertimbangan dan bias pada sisi penjual saja.Sehingga harga dari hasil prediksi cenderung akan mengikuti pasaran harga menurut penjual.
- Model kemungkinan besar masih dapat meleset kurang lebih 5%
- Model kurang dapat dipercaya dalam memprediksi harga mobil di sekitar tahun 2010 ke bawah dan di atas tahun 2020 karena sedikitnya data untuk mobil di sekitar tahun 2010 ke bawah, dan dataset yang tersedia hanya sampai tahun 2020.
- Model kurang dapat dipercaya untuk memprediksi mobil elektrik, karena data yang digunakan untuk melatih model sangat sedikit yang berjenis mobil elektrik.
- Model ini dilatih menggunakan data mobil dengan rentang nilai 450-159999 poundsterling, sehingga mobil dengan harga seharusnya yang diluar range tersebut kurang dapat dipercaya prediksinya.
- Terkadang model masih dapat memprediksi harga yang jauh dari harga sebenarnya meskipun kasus ini jarang terjadi.
- Model dapat lebih dipercaya jika:
    * Tahun registrasi di antara tahun 2010-2020
    * Mobil berbahan bakar Petrol/Diesel
    * Mobil dengan rentang nilai pasaran 450-159999 poundsterling

 ** Conclusion **
 Berdasarkan modeling yang sudah kita lakukan, faktor yang paling berpengaruh terhadap price adalah jenis transmisi, engine size, dan year.Jika dilihat dari MdAPE pada model akhir, apabila nantinya model ini digunakan untuk memprediksi harga mobil bekas, model ini diperkirakan akan meleset kurang lebih 5% dari harga seharusnya.Perkiraan 5% ini tidak mutlak sehingga masih ada kemungkinan untuk meleset lebih atau justru kurang dari 5% ini.
* Implikasi Model:
  - Model ini dapat memudahkan penjual mobil dalam menentukan harga jual mobilnya tentunya dengan memperhitungan 5% error tadi, dan meminimalisir risiko seperti menjual mobil dengan harga terlalu rendah dari pasaran atau menetapkan harga yang overpriced sehingga mobil tidak kunjung terjual.Katakanlah sebuah mobil yang akan dilisting harga seharusnya adalah 20000 jika pada umumnya tanpa model ini pemilik mobil cenderung menetapkan harga meleset 15% dari harga seharusnya.Maka perhitungannya:
      * 5% x 20000 = 1000
      * 15% x 20000 = 3000
      * Selisih : 3000 - 1000 = 2000  
  Di sini bisa kita lihat penjual yang menggunakan model kita dapat unggul dari segi harga hingga 2000 poundsterling dibandingkan yang tidak menggunakan.Jarak ini tentunya semakin besar seiring meningkatnya harga.
  Dengan harga yang fair, tentunya pembeli juga dapat menikmati pengalaman yang baik dalam membeli mobil bekas pada platform kita.Dengan memberikan pengalaman terbaik bagi users, tentunya jumlah user akan meningkat.

  - Dengan user yang meningkat tentunya perusahaan akan diuntungkan dari transaction fee dan servis iklan premiumnya.Jika seandainya setelah penerapan model ini jumlah user meningkat sebanyak 100 orang dalam 1 bulan dan katakanlah 10% saja dari jumlah user ini yang berhasil melakukan transaksi jual beli atau yang mengklik ads atau juga yang tertarik untuk berlangganan iklan premium, kemudian transaction fee yang dikenakan 1% dari harga transaksi, dan katakanlah harga transaksi yang terjadi rata-rata 20000 poundsterling maka untuk perhitungan profit berdasarkan transaksi saja kira-kira seperti ini:
    * Transaction:
        - Transaction Fee => 20000 x 1% = 200
        - Transaction Done => 100 x 10% = 10
        - Total => 200 x 10 = 2000
  - Untuk perhitungan profit berdasarkan iklan premium dengan harga 10 poundsterling/bln saja kira-kira seperti ini:
    * Iklan Premium:
        - Premium fee => 10
        - Premium subs => 100 x 10% = 10
        - Total => 10 x 10 = 100
    * Total profit:
        - 2000 + 100 = 2100 poundsterling
  Berdasarkan contoh di atas, dengan menggunakan model ini perusahaan mampu memperoleh profit mencapai 2100 poundsterling/bln.Perlu ditekankan, perhitungan ini hanya memperhitungkan user baru dalam bulan itu saja.

