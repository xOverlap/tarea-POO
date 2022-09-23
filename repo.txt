import math
aceleracion = 0 # Definimos la aceleracion inicial
pi = math.pi # Importamos pi de la libreria Math
latitud1 = 0
longitud1 = 0

def Distancia(lat1, log1, lat2, log2):
    # Radio de la tierra en kilometros
    radio = 6371
    # Convertimos las cordenadas en radianes
    lat = (lat2 - lat1) * (math.pi / 180)
    log = (log2 - log1) * (math.pi / 180)
    # Punto 1
    a = (math.sin(lat / 2) * math.sin(lat / 2)) + (math.cos(lat1 * (math.pi / 180)) * (math.cos(lat2 * (math.pi / 180)))) * (math.sin(log / 2) * math.sin(log / 2))
    # Punto 2
    c = 2 * math.atan2(math.sqrt(a), math.sqrt(1 - a))
    # Distancia total
    d = radio*c
    return d


# Pedimos los datos
print("Rellene los datos que se le piden a continuacion para completar su registro")
rut = input("Ingrese su rut:\n")
nombre = input("Ingrese su nombre:\n")
apellido = input("Ingrese su apellido:\n")
correo = input("Ingrese su correo:\n")
contraseña = input("Ingrese una contraseña:\n")
edad = int(input("Ingrese su edad:\n"))
matricula = input("Ingrese su matricula:\n")
# Verificamos si es mayor de edad
if edad < 18:
    print("No puede ingresar al sistema, usted es menor de edad\n")
elif edad >= 18:
    # Se muestran sus datos ingresados
    print("Su rut es: ", rut,", su nombre es: ", nombre,", su apellido es: ", apellido,", su correo es: ", correo,", su edad es: ", edad," y su matricula es: ", matricula)
    #  Se le da a escojer una opcion
    print("Presione 1 para iniciar sesion. ")
    print("Presione 2 para comenzar una carrera ")
    opc = input()
    # Si escoje 1 pasa a iniciar sesion
    if opc == "1":
        verficacionCorreo = input("Ingrese su correo:\n")
        verficacionContraseña = input("Ingrese su contraseña:\n")
        # Si el correo y la contraseña son correctos, se le da a escojer una opcion
        if verficacionCorreo == correo and verficacionContraseña == contraseña:
            print("Bienvenido", nombre, "matricula numero", matricula, "\n")
            opcion = ""
            encendido = False
            # Se le preguta si quiere comenzar una carrera
            carrera = input("Presione 1 para comenzar una carrera\nPresione 2 para salir\n")
            # Si escoje 1, se le da a escojer una opcion
            if carrera == "1":
                # Se genera un bucle para que el usuario pueda escojer alguna de las opciones hasta que desee salir
                while opcion != "8":
                    print("1. - Ingresar ubicación GPS Inicial, LATITUD")
                    print("2. - Ingresar ubicación GPS Inicial, LONGITUD")
                    print("3. - Encender el vehículo.")
                    print("4. - Acelerar vehículo")
                    print("5. - Descelerar vehículo")
                    print("6. - Apagar Vehículo")
                    print("7. - Girar Vehículo.")
                    print("8. - Finalizar carrera")
                    opcion = input()
                    # Si escoje 1, se le pide que ingrese la latitud
                    if opcion == "1":
                        latitud1 = float(input("Ingrese la latitud:\n"))
                        print("Latitud ingresada correctamente\n")
                    # Si escoje 2, se le pide que ingrese la longitud
                    elif opcion == "2":
                        longitud1 = float(input("Ingrese la longitud:\n"))
                        print("Longitud ingresada correctamente\n")
                    # Si escoje 3, se le informa que el vehiculo se encendio
                    elif opcion == "3":
                        print("Encendiendo vehículo...\n")
                        encendido = True
                    # Si escoje 4 y el auto esta encendido ( true ), se le informa que el vehiculo se acelero
                    elif opcion == "4" and encendido:
                        aceleracion += 10
                        print("Usted está viajando a", aceleracion, "Km/h\n")
                    # Si escoje 5 y el auto esta encendido ( true ), se le informa que el vehiculo se desacelero
                    elif opcion == "5" and encendido:
                        if aceleracion < 10:
                            print("Usted está detenido\n")
                        elif aceleracion >= 10:
                            if aceleracion == 10:
                                aceleracion = 0
                                print("Usted está detenido\n")
                            elif aceleracion > 10:
                                aceleracion -= 10
                                print("Usted está viajando a", aceleracion, "Km/h\n")
                    # Si escoje 6 y el auto esta encendido ( true ), se le informa que el vehiculo se apago
                    elif opcion == "6" and encendido:
                        print("Apagando vehículo...\n")
                        encendido = False
                    # Si escoje 7 y el auto esta encendido ( true ), se le informa que el vehiculo giro
                    elif opcion == "7" and encendido:
                        print("Girando vehículo...\n")
                    # Si escoje 8, se le informa que la carrera finalizo y tendra que ingresar la latitud y longitud del destino y le dira cuanto es el total a pagar
                    elif opcion == "8":
                        print("Finalizando carrera...\n")
                        latitud2 = float(input("Ingrese la latitud de destino:\n"))
                        longitud2 = float(input("Ingrese la longitud de destino:\n"))
                        distancia = Distancia(latitud1, longitud1, latitud2, longitud2)
                        print("Distancia recorrida: ", round(distancia, 2), "Km")
                        print("Total a pagar por el viaje: $", round(distancia*(220*1.8))) # Como no nos indica investigue y segun meganoticias uber en 2018 cobraba 220 pesos por km recorrido, no encontre informacion actualizada pero por el precio de la gasolina en 2018 que estaba a 737 vs hoy que esta a 1310 multiplicare por 1.8 aprox ese valor
                    else:
                        print("Puede que el motor este apagado o no haya ingresado una opción válida\n")
            # Si escoje 2 sale del programa
            elif carrera == "2":
                print("Saliendo del sistema...")
            else:
                print("Opción no válida\n")
        # Si el correo y la contraseña son incorrectos, se le informa que no puede ingresar al sistema
        else:
            print("Correo o contraseña incorrecto\n")
    elif opc == "2":
        print("Tiene que registrarse para poder comenzar una carrera\n")
    else:
        print("Opción no válida\n")