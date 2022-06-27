# Liquid-Filling-Machine-with-STM32F103XX

Amatör bir çalışmadır. Başarılıdır.
<h2>Makina İşlevi Nedir? </h2>
<h4>
Makinamız dolum makınasıdır. İşlevi belli bir litre dolum yapmak ve dolum yaparken istenilen miktar geçtikten sonra durmasıdır.

Bu işlem şu şekilde gerçekleşiyor.  Stm32 ile kesme işlemi saymayı hedefliyoruz . Bu kesmeler ise akış sensörümüzün darbe sayısını ölçmesi sayesinde her darbede bir kesme üretimi sağlıyoruz. Bu kesmeleri daha sonra yorumluyoruz. İlk işlemde bu yorumu gerçekleştirmek içim miktarını bildiğimiz bir miktar suyu sabitlenmiş akış sensörüne işaret alanının gösterdiği taraftan aktarımını sağlıyoruz. Aktarım sonucu sabit akış sensörümüzün ürettiği kesme sayısını yorumluyoruz. Bu yorum şu şekilde 
Akış sensöründen geçen miktar bölü üretilen kesme sayısı . Bu bize her bir kesmede ne kadar sıvı geçtiğini söyleyecektir.

<h3>Örnek bir hesaplama </h3>

1 Litre su geçirdiğimizde olursak üretilen kesme miktarı 200 çıktığını varsayarsak .</hr>
<h3>1000 ml /200 = 5 ml</h3>   Her kesmede üretilen miktar (Kalibrasyon ayarı). Bu miktarı kesme komutlarında bulunan "milim+=  " bölmesine "5" yazıyoruz.


Bu hesaplamadna sonra gireceğmiz miktarı tuşlar ile yazıp "*" tuşuna basıyoruz. Daha sonra Röle aktif hale geliyor ve Pompamızın elektrik geçisine izin veriyor.
Daha sonra pompa çalışırken , dolum yapılırken akış sensörü  istenilen miktarın fazlasını ölçünce röleyi kapatma komutu gönderiyoruz. </h4>
</br>
<h4>"A" tuşu durdurma , "B" tuşu miktarsız çalıştırma , "*" girilen miktara göre ölçer , "C" ekranı ve tutulan bilgileri temizleme tuşu</h4>

 
<h2>Kullandığımız parçalar.</h2>

<h4>Stm32F103C6T6</h4>

![image](https://user-images.githubusercontent.com/90522945/176002398-ebf7630c-4a41-48c2-8541-213581f4b890.png)


<h4>ST-LINK V2 Programlayıcı </h4>

![image](https://user-images.githubusercontent.com/90522945/176002517-a0c3aede-b2bb-4f80-8bc0-c830b10ba8ec.png)


<h4>LCD Ekran 2x8 </h4>

![resim_2022-06-27_212818913](https://user-images.githubusercontent.com/90522945/176010613-c3a8ecfa-a24b-4ee1-a785-9a0786db93c9.png)


<h4>Röle (5V İle tetikleme) </h4>

![image](https://user-images.githubusercontent.com/90522945/176002977-da145cd2-dd74-4610-a5ae-976a6b058cd8.png)

<h4>4x4 Tuş Takımı</h4>

![image](https://user-images.githubusercontent.com/90522945/176003195-d8685d8f-8a28-4a8e-b7be-ba17b20c2488.png)

<h4>12 Bilge Pumps Sıvı Pompası 750 Gph Sintine Pompa</h4>

![image](https://user-images.githubusercontent.com/90522945/176003348-e7d33656-7597-4ad7-acec-c4ee5cf53bd0.png)

<h4>Su Akış ve Hidrolik Basınç Sensörü (Flowmetter)</h4>

![image](https://user-images.githubusercontent.com/90522945/176004388-cdf1f034-6b7e-4756-9f72-cb1267751f08.png)






<h2>Kullandığımız Uygulamalar</h2>

<h4> STM32CubeIDE </h4>

![image](https://user-images.githubusercontent.com/90522945/176003704-9a360c83-844e-4d7f-9ba9-5047b59e9de4.png)


<h4>Şekil 4.6 STM32 ST-LINK Utility</h4>

![image](https://user-images.githubusercontent.com/90522945/176002606-626e16f6-2d1e-4b55-ba18-158886036ba4.png)


<h4>STM32CUBEIDE Değişikler</h4>

<h4>Rcc Ayarı </h4>

![image](https://user-images.githubusercontent.com/90522945/176004244-5b43ceef-7114-481f-bace-800413967b9b.png)



<h4>Sys Ayarı</h4>

![image](https://user-images.githubusercontent.com/90522945/176004261-ceccdfa1-fb51-4e18-be4e-1e185546a5c6.png)



<h2>Program Kodları </h2>

LCD ve tuş takımı için yazdığım kodlar kütüphane haline getirilmiştir. Daha sonra main.c belgemizden bu dosyalar çağırılarak projede kullanılmıştır. Şekil 5.10’da kütüphanelerin nereye yazılacağı gösterilmiştir.

![image](https://user-images.githubusercontent.com/90522945/176004710-c9aea9a1-92d3-430c-afb9-d283a73a1327.png)


![image](https://user-images.githubusercontent.com/90522945/176004757-b2ea29b0-451c-4c82-a65e-b45cc9ed32fb.png)


![image](https://user-images.githubusercontent.com/90522945/176004783-98a0384f-8b9f-4ca4-a40f-bb907a57d558.png)

![image](https://user-images.githubusercontent.com/90522945/176004815-0a62d9fa-3db2-477e-a218-31a423eea74e.png)


![image](https://user-images.githubusercontent.com/90522945/176004835-515b3055-36fe-4a5e-953a-5d1f74b36cd6.png)



Bu bir kesme işlemidir. Kesme işlemlerini stm32f1xx_it.c uzantılı belgenin içine yazılır. Extern yazıp ana fonksiyondaki (main) tanımladığımız değişkeni burda da kullanarak değişen değer aynen aktarılır. İlgili kesme kodunu Şekil 5.15’deki gibi ilgili fonksiyonun içine yazılmıştır.
<h4>stm32f1xx_it.c içindeki değişiklikler .</h4>

![image](https://user-images.githubusercontent.com/90522945/176004937-6f684a45-c422-45af-8de9-4753b4b20a34.png)



<h2>Prototipin Geliştirilmesi  Ve Şema    </h2>                                                                                                                                    

![desing 2](https://user-images.githubusercontent.com/90522945/176005132-6c88d1f5-c826-4782-b217-15a564b0ccd3.jpeg)


![image](https://user-images.githubusercontent.com/90522945/176005197-813cf761-c5d2-44b3-949f-de30669b5c76.png)

![image](https://user-images.githubusercontent.com/90522945/176005208-da80c3fb-1fa0-4195-92ea-aa5209ccd72a.png)



