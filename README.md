# Code-Print

import os
from getpass import getuser
from datetime import datetime
import time
#import PyPDF2
import shutil
import win32print
import win32api

def main():
    previous_files = set()

    usuario = getuser()
    print(usuario)
    
    archivo='lo'

    while True:
        time.sleep(4)
        current_files = set(os.scandir('C:/Users/'+usuario+'/Downloads'))
        #print(os.path.expanduser('~')+'/Downloads')

        for file in current_files - previous_files:
            nombre=os.path.splitext(file.name)[0]         
            if nombre ==  archivo:
                fecha_fichero = os.path.getmtime(file.path)
                fecha_actual = datetime.now().timestamp()
                diferencia_tiempo = fecha_actual - fecha_fichero
                if diferencia_tiempo < 2000000000:
                    print(f"El archivo {file.name} cumple con el criterio de tiempo.")
                    #agregar_a_impresion(file.path)
                    win32api.ShellExecute( None, 'print', 'lo.pdf',  win32print.SetDefaultPrinter('Cannon 3000'), 'C:/Users/'+usuario+'/Downloads' , 0)
                    print(nombre)
                
                else:
                    print(f"El archivo {file.name} no cumple con el criterio de tiempo.")

        previous_files = current_files


 # Copiar el archivo a la cola de impresión
    #shutil.copy(ruta_archivo, win32print.GetDefaultPrinter())

if __name__ == "__main__": 
    main()
