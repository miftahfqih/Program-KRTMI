# BACA ENCODER
Jadi pada day 2 kemarin kita mulai belajar membaca encoder

total ada 6 encoder (4 encoder roda, 1 encoder cahaya, 1 encoder lain)

permasalah kemarin ada pada pembacaan encoder cahaya, dimana pada IOC pin TIM2 nya belom disetting ke pullup semua
PIN PA15 & PB9

Jadi secara teori pada datasheet encoder E6B2 jika pada datasheet pembacaan encoder nya ditulis Open collector maka semua pin
pembacaan encoder harus di set PULL UP agar encoder dapat terbaca

yang dimana encoder ini nanti dapat membantu robot untuk membaca posisi