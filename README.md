<img src="logo.png" alt="logo" width="750" height="150">

# Sensor IR Receiver

El sensor IR Receiver: Este módulo consta de un receptor IR 1838, una resistencia de 1kΩ y un LED. Funciona junto con el módulo transmisor IR KY-005 . Compatible con plataformas electrónicas populares como Arduino. Sirve muy bien para controles remoto universales, marco de fotos digital, iluminación equipada y otras aplicaciones.


| Características                       |                                          |                                       |  
|---------------------------------------|------------------------------------------|---------------------------------------|
| Dimensión: 6.4 x 7.4 x 51 mm          | Frecuencia: 37.9KHz                      | Ángulo de recepción: 90° (± 45°)      |   
| Ángulo de recepción: 90 °             | Alcance de recepción: 18m                | Filtro de luz ambiental: hasta 500LUX |   
| Voltaje de funcionamiento: 2.7 ~ 5.5V | Corriente de funcionamiento: 0.4 a 1.5mA |                                       |    


<img src="Sensor IR.jpg" alt="Sensor IR" width="500" height="600">


# Sensor IR Remote:
Un control remoto infrarrojo (IR) envía señales de luz infrarroja. Una luz infrarroja no puede verse a simple vista, pero puede ser visible con el uso de una cámara digital, la cámara del teléfono celular o videocámara.

| Características                             |                                          |  
|---------------------------------------------|------------------------------------------|
| Modulación a 38kHz                          | Temperatura: -25 a 85ºC                  |   
| 21 teclas de función para el control remoto | Distancia de Operación: 8-10 mts         |  
| Angulo de Operación: 60º                    | Compatible con la librería IR de Arduino |    

<img src="remoto.jpg" alt="remoto" width="500" height="600">


Codigo
import board
import pulseio
import adafruit_irremote

IR_PIN = board.D2  # Pin connected to IR receiver.

# Expected pulse, pasted in from previous recording REPL session:
pulse = [9144, 4480, 602, 535, 600, 540, 595, 536, 599, 537, 600, 536,
         596, 540, 595, 544, 591, 539, 596, 1668, 592, 1676, 593, 1667,
         593, 1674, 596, 1670, 590, 1674, 595, 535, 590, 1673, 597, 541,
         595, 536, 597, 538, 597, 538, 597, 1666, 594, 541, 594, 541, 594,
         540, 595, 1668, 596, 1673, 592, 1668, 592, 1672, 601, 540, 592,
         1669, 590, 1672, 598, 1667, 593]

print('IR listener')
# Fuzzy pulse comparison function:
def fuzzy_pulse_compare(pulse1, pulse2, fuzzyness=0.2):
    if len(pulse1) != len(pulse2):
        return False
    for i in range(len(pulse1)):
        threshold = int(pulse1[i] * fuzzyness)
        if abs(pulse1[i] - pulse2[i]) > threshold:
            return False
    return True

# Create pulse input and IR decoder.
pulses = pulseio.PulseIn(IR_PIN, maxlen=200, idle_state=True)
decoder = adafruit_irremote.GenericDecode()
pulses.clear()
pulses.resume()
# Loop waiting to receive pulses.
while True:
    # Wait for a pulse to be detected.
    detected = decoder.read_pulses(pulses)
    print('got a pulse...')
    # Got a pulse, now compare.
    if fuzzy_pulse_compare(pulse, detected):
        print('Received correct remote control press!')
















Uso
Los sensores infrarrojos ofrecen una solución para ciertos procedimientos de reconocimiento, por ejemplo, la de músculos. Otra aplicación médica para los sensores infrarrojos es la medición instantánea de la temperatura del cuerpo, es decir, como un termómetro remoto o infrarrojo.




