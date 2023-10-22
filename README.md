![](FOTO.PNG)
# **Tecnológico Nacional de México**
# **Instituto Tecnológico de Tijuana**
# **Subdirección Académica**
# **Depto de Sistemas y Computación**
# **SEMESTRE: AGOSTO – DICIEMBRE 2023**
# **Ing. En Sistemas Computacionales**
# **SISTEMAS PROGRAMABLES 23a**
# **Estevez Ramirez Maria Teresa - 20211773**
## FECHA: 22 de octubre del 2023

# **ChatGTP**
## Código 
```python
# Alumno: Estevez Ramirez Maria Teresa
# No. control: 20211773

import machine
import ssd1306
import network
import urequests
import ujson

# Configuración de la pantalla OLED
i2c = machine.I2C(0, sda=machine.Pin(8), scl=machine.Pin(9), freq=400000)
oled = ssd1306.SSD1306_I2C(128, 64, i2c)

# Configuración de la red WiFi
wifi = network.WLAN(network.STA_IF)
wifi.active(True)
wifi.connect("OPPO A53", "f082dd9d35a2")  # Reemplaza "xxxx" con tu contraseña de WiFi
while not wifi.isconnected():
    pass

# Función para obtener respuesta de ChatGPT
def ask_chatgpt(texto_entrada):
    # Configuración de la API de ChatGPT (reemplaza con tus propias credenciales)
    api_url = 'https://api.openai.com/v1/engines/davinci/completions'
    api_key = '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'

    headers = {
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json",
    }
    data = {
        "prompt": texto_entrada,
        "max_tokens": 50,
    }

    response = urequests.post(api_url, json=data, headers=headers)
    response_data = ujson.loads(response.text)
    oled.fill(0)
    oled.text("Respuesta: ", 0, 0)

    if 'choices' in response_data:
        oled.text(response_data['choices'][0]['text'], 0, 16)
        response_text = response_data['choices'][0]['text']
    else:
        response_text = "No hay respuesta"
    
    oled.show()
    return response_text

# Bucle principal
while True:
    # Esperar a que se presione el botón (ajusta el pin y la configuración según tu hardware)
    boton = machine.Pin(17, machine.Pin.IN, machine.Pin.PULL_UP)
    if not boton.value():
        oled.fill(0)
        oled.text("Bienvenido", 0, 0)
        questions = "¿Cómo te ayudo?:"
        oled.text(questions, 0, 16)
        oled.show()
        texto_entrada = input("¿Cómo te ayudo?: ")  # Inicializa la entrada de texto
        oled.text(texto_entrada, 0, 32)
        oled.show()
        response = ask_chatgpt(texto_entrada)
        # Mostrar en OLED
        oled.text(response, 0, 48)
        oled.show()

```
## Simulación del circuito
![]()

## Curcuito
![]()

## ENCENDIDO
![]()
> Web

![]()
> Encendido

## Apagado
![]()
> Web

![]()
> Apagado
