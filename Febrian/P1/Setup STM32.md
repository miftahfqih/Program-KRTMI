# Setup STM32
### 1. pilih board STM32 yang akan digunakan (Nucleo/Bluepill/Blackpill/dll)
### 2. RCC -> HSE pilih crystal/ceramic resonator, terus RCC global interrupt di enable
### 3. di clock configuration pilih HSE, lalu PLL/CLK, lalu sesuaikan Clock dengan frekuensi max clock
### 4. pilih pin-pin yang akan digunakan untuk output, PWM, dan encoder
### 5. untuk memilih pin output, langsunng dipilih pin nya lalu state nya diubah menjadi GPIO_Output
### 6. untuk timer atau PWM, pertama kita memilih timer yang akan digunakan lalu memilih channel nya, dan memlih mode PWM Generation CH1 
### 7. Setelah memilih channel untuk timer kita harus mengatur prescaler dan counter period nya agar supaya clock nya sesuai dengan apa yang kita inginkan 
### 8. untuk mengatur prescaler dan counter period kita dapat menggunakan perhitungan ....., sehingga kita mendapatkan clock yang kita inginkan
### 9. jika ingin menggunakan timer sebagai encoder, maka untuk channel nya kita memilih combined channel lalu Encoder Mode
### 10. setelah selesai setup pin dan clock nya maka untuk generate code nya dapat menggunakan ctrl+s atau dapat memilih logo seperti gerigi diatas
