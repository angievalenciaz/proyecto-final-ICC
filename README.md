# proyecto-final-ICC
menu():
    print("=============================")
    print("==     1. Crear            ==")
    print("==     2. Buscar           ==")
    print("==     3. Editar           ==")
    print("==     4. Eliminar         ==")
    print("==     5. Mensaje          ==")
    print("==     6. Ver historial    ==")
    print("==     7. Salir            ==")
    print("=============================")
    print("Seleccione una opción del 1 al 7: ")
    opcion=int(input())

    return opcion



def Edit(posicion,pos2):
    Alumnos.seek(0)
    data=Alumnos.readlines()
    Alumnos.seek(0)
    for linea in data:
        if linea != "-+-".join(lista_de_alumnos[posicion])+"-+-\n":
            Alumnos.write(linea)
        else:
            nuevo_valor=input("Ingrese nuevo dato: ")
            lista_de_alumnos[posicion][pos2]=str(nuevo_valor)
            Alumnos.write("-+-".join(lista_de_alumnos[posicion])+"-+-\n")
    Alumnos.truncate()



def seguridad(dato):
    seguir=True
    while seguir==True:
        pregunta=int(input("¿El contenido ingresado es correcto?:\n [1]Sí\n [0]No\n"))
        if pregunta == 1:
            seguir=False
        elif pregunta==0:
            dato=input("Ingrese nuevo contenido: ")
        else:
            print("Solamente los valores 1 y 0")
    return dato


def ID(ID_Registro):
    for i in range(0,len(lista_de_alumnos)):
        if lista_de_alumnos[i][4] == str(ID_Registro):
            return i
    print("No se encontró el ID")


def crear(lista):

    #Agregar un algoritmo que permita crear una lista solicitando los siguientes datos:
    # 1. Nombres
    # 2. Apellido Paterno
    # 3. Edad
    # 4. Teléfono
    # 5. ID_Registro --> Este código se va a generar automáticamente de manera correlativa y será el identificador para manipular el registro en la lista.
    registro=[]
    print("Funcionalidad de crear")
    registro.append(input("1. Nombres: "))
    registro.append(input("2. Apellido Paterno: "))
    registro.append(input("3. Edad: "))
    registro.append(input("4. Teléfono: "))
    registro.append(str(contador))
    Alumnos.write("-+-".join(registro)+"-+-\n")
    lista.append(registro)
    print("5. ID_Registro: ",lista[len(lista)-1][4])
    print(lista[len(lista)-1])
    lista_modificada = lista
    return lista_modificada



def buscar(lista_donde_se_buscara_el_valor, valor_a_buscar):
    #Agregar un algoritmo que permita buscar los registros en la lista_donde_se_buscara_el_valor que cumplan con el valor_a_buscar.
    #Deberá mostrar los registros que coincidan.
    print("Funcionalidad de buscar")
    for i in range(0,len(lista_donde_se_buscara_el_valor)):
        for j in range(0,5):
            for busqueda in lista_donde_se_buscara_el_valor[i][j]:
                if valor_a_buscar in busqueda:
                    print(lista_donde_se_buscara_el_valor[i])
                    if i+1<=len(lista_donde_se_buscara_el_valor)-1:
                        i=i+1
                    else:
                        return
    print("No se encontró el valor solicitado")


    return



def editar(lista, ID_Registro):
    #Agregar un algoritmo que permita modificar el registro especifico de una lista
    #Los datos que se podrán modificar son:
    # 1. Nombres
    # 2. Apellido Paterno
    # 3. Edad
    # 4. Teléfono
    seguir=True
    pos=ID(ID_Registro)
    print(lista[pos])
    while seguir==True:
        valor_a_cambiar=int(input("¿Qué valor desea cambiar?\n [0]Nombre\n [1]Apellido\n [2]Edad\n [3]Teléfono\n [4]Salir\n"))
        while not -1 < valor_a_cambiar < 5:
            valor_a_cambiar=int(input("Solo los números mostrados\n ¿Qué valor desea cambiar?\n [0]Nombre\n [1]Apellido\n [2]Edad\n [3]Teléfono\n [4]Salir\n"))
        if valor_a_cambiar == 4:
            seguir=False
        elif int(input("¿Seguir?:\n [1]Sí\n [0]No\n")) == 0:
            seguir=False
        else:
            Edit(pos,valor_a_cambiar)
    lista_modificada=lista
    return lista_modificada



def eliminar(lista, ID_Registro):
    pos=ID(ID_Registro)
    Alumnos.seek(0)
    data=Alumnos.readlines()
    Alumnos.seek(0)
    for linea in data:
        if linea != "-+-".join(lista_de_alumnos[pos])+"-+-\n":
            Alumnos.write(linea)
    Alumnos.truncate()
    lista.remove(lista[pos])
    lista_modificada = lista

    print("Funcionalidad de eliminar")

    return lista_modificada



def mensaje(emisor, receptor, mensaje, lista_de_mensajes):

    #Agregar un algoritmo que permita agregar mensajes a una lista_de_mensajes con la siguiente estructura:
    # ID_Registro_del_emisor
    # ID_Registro_del_receptor
    # Contenido del Mensaje
    # Fecha y hora del mensaje --> Este valor debe generarse automáticamente

    msn=[]
    FH="Fecha: "+time.strftime("%d/%m/%y")+" / Hora: "+time.strftime("%H:%M:%S")
    print("ID_Emisor: "+str(emisor)+"\nID_Receptor: "+str(receptor)+"\nMensaje: "+mensaje+"\n"+FH)

    pos=ID(emisor)
    msn.append("Emisor: "+lista_de_alumnos[pos][0]+" "+lista_de_alumnos[pos][1])
    pos2=ID(receptor)
    msn.append("Receptor: "+lista_de_alumnos[pos2][0]+" "+lista_de_alumnos[pos2][1])
    msn.append(FH)
    msn.append("Mensaje: "+mensaje)
    Mensajes.write("-+-".join(msn)+"-+-\n")
    lista_de_mensajes.append(msn)

    print("Funcionalidad de mensaje")
    return lista_de_mensajes



def ver_historial(lista_de_mensaje):
    #Agregar un algoritmo para mostrar el historial de los mensajes en orden cronológico con la siguient estructura:
    # Nombres y apellido del emisor |  Nombres y apellido del receptor  |  Fecha y hora del mensaje  |  Contenido del Mensaje
    # El historial debe mostrarse ordenado por Emisor , Receptor y Fecha y hora del mensaje

    for p in range(len(lista_de_mensaje)-1,-1,-1):
        print(lista_de_mensaje[p])

    print("Funcionalidad de ver historial")

    return


import time
Alumnos=open("Alumnos.txt","r+")
Mensajes=open("Mensajes.txt","r+")
lista_de_alumnos = []
lista_de_mensajes = []
for i,line in enumerate(Alumnos):
    lista_de_alumnos.append(line.split("-+-"))
    lista_de_alumnos[i].pop()
for i,line in enumerate(Mensajes):
    lista_de_mensajes.append(line.split("-+-"))
    lista_de_mensajes[i].pop()
if len(lista_de_alumnos) > 0:
    contador=int(lista_de_alumnos[len(lista_de_alumnos)-1][4])
else:
    contador=0
opcion=0



while not(opcion == 7):

    opcion = menu()

    if opcion == 1:
        print("Seleccionó la opción Crear")
        contador=contador+1
        lista_de_alumnos = crear(lista_de_alumnos)

    elif opcion == 2:
        print("Seleccionó la opción Buscar")
        valor_a_buscar = input("Ingrese el valor a buscar: ")
        buscar(lista_de_alumnos, valor_a_buscar)

    elif opcion == 3:
        print("Seleccionó la opción Editar")
        codigo_de_alumno = int(seguridad(input("Ingrese el ID de registro de alumno a MODIFICAR: ")))
        lista_de_alumnos = editar(lista_de_alumnos, codigo_de_alumno)

    elif opcion == 4:
        print("Seleccionó la opción Eliminar")
        codigo_de_alumno = int(seguridad(input("Ingrese el ID de registro de alumno a ELIMINAR: ")))
        lista_de_alumnos = eliminar(lista_de_alumnos, codigo_de_alumno)

    elif opcion == 5:
        print("Seleccionó la opción Mensaje")
        ID_registro_EMISOR=int(seguridad(input("Ingrese el ID de registro del EMISOR: ")))
        ID_registro_RECEPTOR = int(seguridad(input("Ingrese el ID de registro del RECEPTOR: ")))
        contenido_del_mensaje = seguridad(input("Ingrese el mensaje: "))
        lista_de_mensajes = mensaje(ID_registro_EMISOR, ID_registro_RECEPTOR, contenido_del_mensaje, lista_de_mensajes)

    elif opcion == 6:
        print("Seleccionó la opción Ver Historial")
        ver_historial(lista_de_mensajes)

    elif opcion == 7:
        print("Finalizó el programa")
