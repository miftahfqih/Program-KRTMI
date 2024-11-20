<h1>SETUP STM32 UNTUK MENGGERAKKAN MOTOR</h1>

<p>
  <br>1. Buat new project STM323<br/>
  <br>2. Masuk ke board selector kemudian sesuaikan board yang akan kita pakai, misalnya STM32F446RETX<br/>
  <br>3. Setelah digenerate akan masuk ke ioc nya<br/>
  <br>4. Untuk setup clock masuk ke RCC (System Core) di Mode HSE pilih Crystal/Ceramic Resonator<br/>
  <br>4. Atur Clock Configuration sesuai dengan frekuensi yang diinginkan : pilih HSE dan setup PLLCLK lalu sesuaikan frekuensi maksimumnya nya misalnya 180Mhz<br/>
  <br>5. Setelah setup Clock Configuration, kemudian pilih atur pin-pin yang digunakan pada GPIO (System Core)<br/>
  <br>6. Sesuaikan dengan kebutuhan seperti output, pwm, encoder, dll<br/>
  <br>7. Untuk motor sesuaikan pin outputnya, terdapat 2 pin direksi dan 1 pin PWM. Pin direksi menggunakan GPIO_Output dan pin PWM menggunakan Timer yang diseuiakan channelnya<br/>
  <br>8. Setelah memilih timer atur prescaler dengan melakukan perhitungan frekuensi maksimum/clock*timer<br/>
  <br>9. Jika selesai setup maka generate code dengan menggunakan ctrl+s<br/>
  <br>10. Dalam codingan deklarasikan pin dengan menggunakan HAL_TIM_PWM_Start(&htim14(pintimer), TIM_CHANNEL_1(timerchannel);<br/>
  <br>11. Untuk menggerakan motor masukkan ke dalam fungsi seperti contoh berikut :<br/>
  <br>    void jalanMotor(int motor, int speed){
  
		if (motor == 1){
			if (speed >= 0){
				HAL_GPIO_WritePin(GPIOA, GPIO_PIN_12, 0);
				HAL_GPIO_WritePin(GPIOA, GPIO_PIN_6, 1);
			}
			else{
				HAL_GPIO_WritePin(GPIOA, GPIO_PIN_12, 1);
				HAL_GPIO_WritePin(GPIOA, GPIO_PIN_6, 0);
			}

			TIM14->CCR1=abs(speed);
		}
		if (motor == 2){
			if (speed >= 0){
				HAL_GPIO_WritePin(GPIOC, GPIO_PIN_9, 1);
				HAL_GPIO_WritePin(GPIOC, GPIO_PIN_8, 0);
			}
			else{
				HAL_GPIO_WritePin(GPIOC, GPIO_PIN_9, 0);
				HAL_GPIO_WritePin(GPIOC, GPIO_PIN_8, 1);
			}



			TIM10->CCR1=abs(speed);
		}
		if (motor == 3){
			if (speed >= 0){
				HAL_GPIO_WritePin(GPIOB, GPIO_PIN_2, 1);
				HAL_GPIO_WritePin(GPIOB, GPIO_PIN_1, 0);
			}
			else{
				HAL_GPIO_WritePin(GPIOB, GPIO_PIN_2, 0);
				HAL_GPIO_WritePin(GPIOB, GPIO_PIN_1, 1);
			}

			TIM12->CCR2=abs(speed);
		}
		if (motor == 4){
			if (speed >= 0){
				HAL_GPIO_WritePin(GPIOC, GPIO_PIN_4, 0);
				HAL_GPIO_WritePin(GPIOB, GPIO_PIN_13, 1);
			}
			else{
				HAL_GPIO_WritePin(GPIOC, GPIO_PIN_4, 1);
				HAL_GPIO_WritePin(GPIOB, GPIO_PIN_13, 0);
			}

			TIM12->CCR1=abs(speed);
		}
	}
 <br>12. Untuk menentukan arah motor sesuai dengan yang kita inginkan dapat dimasukkan ke fungsi<br/>
 ```
	int kinematikRoda(int motor, int x, int y, int w){
		if (motor == 1){
			return x-y-w;
		}
		if (motor == 2){
			return x+y+w;
		}
		if (motor == 3){
			return x+y-w;
		}
		if (motor == 4){
			return x-y+w;
		}
		return 0;

	}
```
<br>13. Untuk menjalankan motor dapat dimasukkan ke dalam fungsi juga<br/>
```
	int robotJalan(int motor, int x, int y, int w){
						  motor=kinematikRoda(1, 0, 0, 200);
						  motor=kinematikRoda(2, 0, 0, 200);
						  motor=kinematikRoda(3, 0, 0, 200);
						  motor=kinematikRoda(4, 0, 0, 200);

						  jalanMotor(1,motor);
						  jalanMotor(2,motor);
						  jalanMotor(3,motor);
						  jalanMotor(4,motor);

	}
```
<br>14. Agar program dapat berjalan maka fungsi untuk menjalankan dapat dipanggil di while(1)<br/>
```
while (1){
     robotJalan(1, 0, 0, 200);
{
```
</p>
