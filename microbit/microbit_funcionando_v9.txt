from microbit import *

# Configura el puerto serial
uart.init(baudrate=115200)

debounce_delay = None

while debounce_delay == None:
    if uart.any():  # Verifica si hay datos disponibles
        received_data = uart.readline()  # Lee los datos
        if received_data:  # Verifica que haya datos
            #display.scroll(received_data.decode('utf-8'))  # Decodifica y muestra los datos
            letra = chr(received_data[0])
            if letra == 's':
                debounce_delay = 50
                display.scroll(chr(received_data[0]))
            elif letra == 'd':
                debounce_delay = 300
                display.scroll(chr(received_data[0]))
            
    
display.scroll (debounce_delay)

if debounce_delay == 300:
    imagenes_botones = [1, 2, 3, 4]
    umbral = 50

    def mostrar_boton(imagen, mensaje):
        """Muestra la imagen en la pantalla y envía el mensaje por UART."""
        display.show(imagen)
        uart.write(mensaje)
        sleep(debounce_delay)  # Evita que el botón se registre varias veces rápidamente

    while True:
        # Leer los valores de los botones
        if button_b.was_pressed():
            display.show(Image.SAD)
            sleep (200)
            reset()
            
        valor_boton1 = pin0.read_analog()
        valor_boton2 = pin1.read_analog()
        valor_boton3 = pin2.read_analog()
        valor_boton4 = pin5.read_digital()
    
        # Detectar cuál botón se ha presionado con anti-rebote
        if valor_boton1 < umbral:
            mostrar_boton(imagenes_botones[0], '1')
            while pin0.read_analog() < umbral:  # Espera a que se libere el botón
                pass  # No hacer nada hasta que el botón sea liberado
        elif valor_boton2 < umbral:
            mostrar_boton(imagenes_botones[1], '2')
            while pin1.read_analog() < umbral:
                pass
        elif valor_boton3 < umbral:
            mostrar_boton(imagenes_botones[2], '3')
            while pin2.read_analog() < umbral:
                pass
        elif valor_boton4 == 1:
            mostrar_boton(imagenes_botones[3], '4')
            while pin5.read_digital() == 1:
                pass
        else:
            display.clear()
    
        sleep(300)  # Para "Simón dice" sleep es de 300ms

if debounce_delay == 50:

    # Defino las imágenes para cada botón
    imagenes_botones = [1, 2, 3, 4]
    umbral = 50

    def mostrar_boton(imagen, mensaje):
        """Muestra la imagen en la pantalla y envía el mensaje por UART."""
        display.show(imagen)
        uart.write(mensaje)

    while True:
        # Leer los valores de los botones
        if button_b.was_pressed():
            display.show(Image.SAD)
            sleep (200)
            reset()
        valor_boton1 = pin0.read_analog()
        valor_boton2 = pin1.read_analog()
        valor_boton3 = pin2.read_analog()
        valor_boton4 = pin5.read_digital()

        # Detectar cuál botón se ha presionado
        if valor_boton1 < umbral:
            mostrar_boton(imagenes_botones[0], '1')
        elif valor_boton2 < umbral:
            mostrar_boton(imagenes_botones[1], '2')
        elif valor_boton3 < umbral:
            mostrar_boton(imagenes_botones[2], '3')
        elif valor_boton4 == 1:
            mostrar_boton(imagenes_botones[3], '4')
        else:
            display.clear()
    
        # Controlar el tiempo de espera según el juego
        sleep(50)  # Para "Simón Dice" sleep es de 300, para "Snake" puede ser 50.

    
        sleep(300)  # Para "Simón dice" sleep es de 300ms

if debounce_delay == 50:

    # Defino las imágenes para cada botón
    imagenes_botones = [1, 2, 3, 4]
    umbral = 50

    def mostrar_boton(imagen, mensaje):
        """Muestra la imagen en la pantalla y envía el mensaje por UART."""
        display.show(imagen)
        uart.write(mensaje)

    while True:
        # Leer los valores de los botones
        valor_boton1 = pin0.read_analog()
        valor_boton2 = pin1.read_analog()
        valor_boton3 = pin2.read_analog()
        valor_boton4 = pin5.read_digital()

        # Detectar cuál botón se ha presionado
        if valor_boton1 < umbral:
            mostrar_boton(imagenes_botones[0], '1')
        elif valor_boton2 < umbral:
            mostrar_boton(imagenes_botones[1], '2')
        elif valor_boton3 < umbral:
            mostrar_boton(imagenes_botones[2], '3')
        elif valor_boton4 == 1:
            mostrar_boton(imagenes_botones[3], '4')
        else:
            display.clear()
    
        # Controlar el tiempo de espera según el juego
        sleep(50)  # Para "Simón Dice" sleep es de 300, para "Snake" puede ser 50.




#--------------------------------------------------------------------------------------------------
#el microbit se resetea con el boton b
