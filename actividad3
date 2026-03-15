import tkinter as tk
import threading
import time
import random

semaforo = threading.Semaphore(2)
autos_creados = 0

def crear_auto():

    global autos_creados
    autos_creados += 1
    auto_id = autos_creados

    y = random.randint(60,200)

    auto = canvas.create_rectangle(10,y,50,y+20,fill="blue")

    hilo = threading.Thread(target=logica_auto,args=(auto,auto_id))
    hilo.start()


def logica_auto(auto,id_auto):

    escribir_log(f"Auto {id_auto} llegó al puente")

    semaforo.acquire()

    escribir_log(f"Auto {id_auto} entrando al puente")

    mover(auto,300)

    escribir_log(f"Auto {id_auto} cruzando")

    time.sleep(random.randint(1,3))

    mover(auto,600)

    escribir_log(f"Auto {id_auto} salió del puente")

    semaforo.release()


def mover(auto,destino):

    x_actual = canvas.coords(auto)[0]

    while x_actual < destino:

        ventana.after(0,canvas.move,auto,5,0)
        time.sleep(0.05)
        x_actual += 5


def escribir_log(texto):

    ventana.after(0,lambda: registro.insert(tk.END,texto+"\n"))
    ventana.after(0,registro.see,tk.END)


ventana = tk.Tk()
ventana.title("Simulación Concurrencia - Puente")
ventana.geometry("800x500")

titulo = tk.Label(
    ventana,
    text="Simulación de Hilos con Semáforo",
    font=("Arial",16)
)
titulo.pack(pady=10)

canvas = tk.Canvas(ventana,width=700,height=250,bg="lightgray")
canvas.pack()

canvas.create_rectangle(300,0,450,250,fill="brown")

boton = tk.Button(
    ventana,
    text="Agregar Auto",
    command=crear_auto,
    bg="green",
    fg="white",
    font=("Arial",12)
)
boton.pack(pady=10)

registro = tk.Text(ventana,width=80,height=10)
registro.pack()

ventana.mainloop()
