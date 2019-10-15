# SISTEMA DE DETECCION DE CAIDA
Python.
import smtplib
import socket
sock = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)
address = ("192.168.1.13",5555) #direccion ip del pc y puerto de envio de datos
sock.bind(address)
data,address = sock.recvfrom(5555)

def datos():
    while True:
        data,address = sock.recvfrom(5555)
        a = float(data[17:23]) #ubicacion del dato x en el arreglo de datos del acelerometro
        b = float(data[25:31]) #ubicacion del dato y en el arreglo de datos del acelerometro
        c = float(data[32:39]) #ubicacion del dato z en el arreglo de datos del acelerometro
        #print (a,"    ",b,"    ",c) #imprime los datos pero no es necesario
        norma = (float(((a**2)+(b**2)+(c**2))**(1/2)))      
        print (norma)
        if norma > 50:
            print("la persona se cayó")
            def enviarmail():
                mensaje = "la persona se cayo!" # el cuerpo del mensaje
                subject = "ALERTA" # el asunto del mensaje
                mensaje = "Subject: {}\n\n{}".format(subject, mensaje) #el mensaje con asunto
                server = smtplib.SMTP_SSL('smtp.gmail.com', 465)
                server.login('correo de donde se envia', "clave respectiva")
                server.sendmail("correo de donde se envia", "correo a quien se envia", mensaje)
                server.quit()
                return
            enviarmail()
   
datos()  
