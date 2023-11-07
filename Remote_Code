import board
from adafruit_motorkit import MotorKit
from adafruit_motor import stepper
from pynput import keyboard
import RPi.GPIO as GPIO

GPIO_PIN = 13

GPIO.setmode(GPIO.BCM)
GPIO.setup(GPIO_PIN, GPIO.OUT)

kit = MotorKit()

kit.stepper1.throttle = 1
kit.stepper2.throttle = 1

kit.stepper1._step_size = 15
kit.stepper2._step_size = 15

kit.stepper1.release_time = 0.001
kit.stepper2.release_time = 0.001

def on_press(key):
    try:
        if key.char == 'a':
            kit.stepper1.onestep()
            time.sleep(0.01)
        elif key.char == 'd':
            kit.stepper1.onestep(direction=stepper.BACKWARD)
            time.sleep(0.01)
        elif key.char == 'w':
            kit.stepper2.onestep()
            time.sleep(0.01)
        elif key.char == 's':
            kit.stepper2.onestep(direction=stepper.BACKWARD)
            time.sleep(0.01)
        elif key.char == 'c':
            GPIO.output(GPIO_PIN, GPIO.HIGH)
    except AttributeError:
        pass

def on_release(key):
    if key.char in ['a', 'd', 'w', 's']:
        kit.stepper1.throttle = 10.0
        kit.stepper2.throttle = 10.0
    elif key.char == 'c':
        GPIO.output(GPIO_PIN, GPIO.LOW)

with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()

GPIO.cleanup()
