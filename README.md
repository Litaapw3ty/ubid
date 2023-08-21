import RPi.GPIO as GPIO
import time

# Atur mode pin GPIO
GPIO.setmode(GPIO.BCM)

# Tentukan nomor pin GPIO yang digunakan
servo_pin = 27

# Konfigurasi pin sebagai output
GPIO.setup(servo_pin, GPIO.OUT)

# Buat objek PWM untuk mengendalikan servo
pwm = GPIO.PWM(servo_pin, 50)  # 50Hz (siklus kerja 20 ms)

# Mulai PWM dengan siklus kerja 0 (posisi awal servo)
pwm.start(0)

try:
    while True:
        # Posisi servo pada sudut 0 derajat
        pwm.ChangeDutyCycle(2.5)  # Perubahan nilai duty cycle untuk mengubah posisi servo
        time.sleep(1)  # Tunggu selama 1 detik

        # Posisi servo pada sudut 90 derajat
        pwm.ChangeDutyCycle(12.5)
        time.sleep(1)

        # Posisi servo pada sudut 180 derajat
        pwm.ChangeDutyCycle(12.5)
        time.sleep(1)

except KeyboardInterrupt:
    # Jika pengguna menekan Ctrl+C, hentikan PWM dan bersihkan pin GPIO
    pwm.stop()
    GPIO.cleanup()

