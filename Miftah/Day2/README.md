<h1>Encoder untuk Motor</h1>
<p>
  <br>Encoder igunakan untuk mengetahui posisi robot berbasis putaran. Cara kerja encoder menggunakan gtembakan laser yang melewati sekat-sekat yagn bergerak sesuai rotasi motor. Ada juhga yang menggunakan medan magnet<br/>
  <br>Pada kali ini akan dijelaskan mengenai setting encoder pada motor</br>
  <br>1. Sesuaikan Timer yang digunakan pada encoder motor pada menu TIMERS ioc</br>
  <br>2. Pada menu combined channels di mode ubah menjadi encoder mode</br>
  <br>3. Setelah di setup semua generate code dengan menggunakan ctrl+s</br>
  <br>4. Deklarasikan variable dengan menggunakan tipe data short int</br>

  ```
  short int enc1;
  short int enc2;
  short int enc3;
  short int enc4;
  short int enc5;
  short int encA;
```
  
  <br>5. Deklarasikan juga pada user code begin untuk timer nya</br>

  ```
  HAL_TIM_Encoder_Start(&htim1, TIM_CHANNEL_ALL);
  HAL_TIM_Encoder_Start(&htim2, TIM_CHANNEL_ALL);
  HAL_TIM_Encoder_Start(&htim3, TIM_CHANNEL_ALL);
  HAL_TIM_Encoder_Start(&htim5, TIM_CHANNEL_ALL);
  HAL_TIM_Encoder_Start(&htim8, TIM_CHANNEL_ALL);
```
  
  <br>6. Pada while (1) buat program untuk dapat terdeteksi</br>

  ```
  enc1 = TIM1 -> CNT;
  enc2 = TIM2 -> CNT;
  enc3 = TIM3 -> CNT;
  enc4 = TIM5 -> CNT;
  enc5 = TIM8 -> CNT
  encA = TIM4 -> CNT;
```
`
    <br>7. Untuk mengujinya dapat menggunakan fitur debgguer (logo laba-laba) kemudian cek pada live expression masukkan variabel encoder yang akan di tes</br>
</p>
