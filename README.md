**Model Prediksi Mobil Bekas United Kingdom**

Dikarenakan model berukuran lebih besar dari 25MB, final model bisa diakses di link ini: https://drive.google.com/file/d/1iWBCjYL3_g5VZM70cstx9fF_yPty04xV/view?usp=sharing

Project ini dibuat dalam rangka Final Project  Purwadhika, sebagai syarat kelulusan program Data Science Online.

**Content**
* File project berupa ipynb, memuat proses data understanding, data cleaning, exploratory data analysis, preprocessing, baseline model, hyperparameter tuning serta data prediction.
* Dataset diunduh melalui Google Drive yang disediakan Purwadhika, yang bersumber dari Kaggle adityadesai13 (https://www.kaggle.com/datasets/adityadesai13/used-car-dataset-ford-and-mercedes)

**Library**
***Basic:***
* Pandas -> Data Manipulation and Handling
* Numpy -> Math operations
* Matplotlib, Seaborn -> Data visualization

***Uji Statistik:***
* Normaltest -> Uji normalitas
* Kruskal -> F-test nonparametrik

***Preprocessing:***
* CategoryEncoder, OneHotEncoder -> Encoding kategorikal
* RobustScaler -> Scaling numerik
* ColumnTransformer -> merangkai transformasi kolom secara paralel
* Pipeline (sklearn) -> mernagkai model dan transformer secara berurutan
* TrainTestSplit -> Membagi dataset menjadi gugus Training dan Testing

***Regression Models:***
* KNeighborsRegressor
* DecisionTreeRegressor
* Ridge
* XGBRegressor
* LGBMRegressor

***Evaluation Metrics:***
* Median Absolute Error
* R2_score
* Cross_val_score

**Data Dictionary**
* **model**: nama jenis mobil
* **year**: tahun registrasi mobil 
* **price**: harga jual yang terpampang pada listing (dalam Poundsterling)
* **transmission**: jenis transmisi mobil
* **mileage**: jarak (dalam mil) tempuh penggunaan mobil
* **fuelType**: jenis bahan bakar
* **tax**: pajak kendaraan bermotor tahunan (dalam poundsterling)
* **mpg**: mil yang dapat ditempuh untuk setiap gallon bahan bakar
* **engineSize**: volume mesin (liter)
* **brand**: merek mobil

**Use Case**

* Model ini nantinya akan digunakan oleh calon penjual mobil yang hendak memasang listing pada platform kita.
* Calon penjual mobil hanya perlu memasukkan informasi spesifikasi mobil yang dibutuhkan (model,year,transmission,mileage,fueltype,mpg,enginesize(liter),brand) dan model akan memberikan rekomendasi harganya.


**Analytic Approach**

Karena tujuan kita adalah memprediksi harga, yang perlu dilakukan adalah melakukan analisis data untuk mengetahui faktor apa saja yang mempengaruhi harga jual mobil bekas, kemudian akan dilanjutkan dengan membangun sebuah model regresi yang dapat digunakan sebagai alat untuk membantu penjual mobil bekas pada platform perusahaan untuk memprediksi harga yang dapat membantu dalam menentukan harga jual mobil agar memiliki harga yang kompetitif di pasar.


**Metric**

Pada umumnya untuk regresi, kita bisa menggunakan metric seperti MAE,RMSE,R2,MAPE,dan MedAE.Pemilihan metric ini berdasarkan karakteristik datanya.Evaluasi metrik yang dapat digunakan jika memiliki banyak outlier adalah MedAE karena berdasarkan https://scikit-learn.org/stable/modules/model_evaluation.html#median-absolute-error:~:text=3.3.4.6.-,Median%20absolute%20error,-%C2%B6 metric ini robust terhadap outlier,RMSE(jika tidak ada outlier). Penggunaan MedAE ini robust terhadap outliers, dan untuk MedAE hasil errornya didapat dari median absolut errornya.Untuk mempermudah interpretasi MedAE berdasarkan https://help.pecan.ai/en/articles/6456388-model-performance-metrics-for-regression-models#:~:text=Percentage%20Error%20(RMSPE)-,Median%20Absolute%20Percentage%20Error%20(MdAPE),-Median%20Absolute%20Percentage kita dapat membuat custom metric yaitu MdAPE yang merupakan persentase MedAE, RMSE adalah nilai rata-rata error kuadrat yang setelah itu di akarkan agar lebih mudah untuk dipahami. Selain itu kita juga akan menggunakan R2 score yang dapat mengukur kemampuan model dalam menjelaskan target variabel menggunakan variabel dependennya.Semakin kecil nilai RMSE, dan MedAE yang dihasilkan, berarti model semakin akurat dalam memprediksi harga sewa sesuai dengan limitasi fitur yang digunakan. Sebaliknya semakin besar nilai R-Squared yang memiliki nilai antara 0-1, maka semakin baik model tersebut.

**Models**
* XGBoost: https://xgboost.readthedocs.io/en/stable/get_started.html
* K-Neighbors Regression: https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html
* Ridge: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Ridge.html
* LightGBM: https://lightgbm.readthedocs.io/en/stable/
* Decision Tree Regression: https://scikit-learn.org/stable/modules/tree.htm



**Limitation**

- Model dilatih menggunakan dataset harga listing (belum terjual) yang ditentukan oleh tiap pemilik mobil, sehingga harga dari hasil prediksi cenderung akan mengikuti pasaran harga menurut penjual.
- Model kemungkinan besar masih dapat meleset kurang lebih 5%
- Terkadang model masih dapat memprediksi harga yang jauh dari harga sebenarnya meskipun kasus ini jarang terjadi.
- Model dapat lebih dipercaya jika:
    * Tahun registrasi di antara tahun 2010-2020
    * Mobil berbahan bakar Petrol/Diesel
    * Mobil dengan rentang nilai pasaran 450-159999 poundsterling
 
**Conclusion**

Berdasarkan modeling yang sudah kita lakukan, faktor yang paling berpengaruh terhadap price adalah jenis transmisi, engine size, dan year.Jika dilihat dari MdAPE pada model akhir, apabila nantinya model ini digunakan untuk memprediksi harga mobil bekas, model ini diperkirakan akan meleset kurang lebih 5% dari harga seharusnya.Perkiraan 5% ini tidak mutlak sehingga masih ada kemungkinan untuk meleset lebih atau justru kurang dari 5% ini.

**Tableau Dashboard**
https://public.tableau.com/app/profile/steven.gordianus/viz/FinalProject_17116248960980/Dashboard1
 
