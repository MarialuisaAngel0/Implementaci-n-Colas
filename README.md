from collections import deque

# Clase para la Cola de Prioridad
class PriorityQueue:
    def __init__(self):
        self.queue = deque()
    
    def enqueue(self, item):
        """Agrega un elemento a la cola."""
        self.queue.append(item)
    
    def dequeue(self):
        """Elimina y retorna el primer elemento de la cola."""
        if not self.is_empty():
            return self.queue.popleft()
        return None
    
    def is_empty(self):
        """Verifica si la cola está vacía."""
        return len(self.queue) == 0
    
    def size(self):
        """Devuelve el número de elementos en la cola."""
        return len(self.queue)
    
    def show(self):
        """Muestra los elementos en la cola."""
        return list(self.queue)


# *Sistema de Gestión de Tareas*
class TaskManager:
    def __init__(self):
        self.task_queue = PriorityQueue()
    
    def add_task(self, task):
        self.task_queue.enqueue(task)
        print(f"Tarea '{task}' agregada correctamente.")
    
    def process_task(self):
        if not self.task_queue.is_empty():
            task = self.task_queue.dequeue()
            print(f"Tarea '{task}' procesada.")
        else:
            print("No hay tareas pendientes.")
    
    def show_pending_tasks(self):
        tasks = self.task_queue.show()
        if tasks:
            print("Tareas Pendientes:", tasks)
        else:
            print("No hay tareas en espera.")


# *Sistema de Atención al Cliente*
class CustomerService:
    def __init__(self):
        self.vip_queue = PriorityQueue()
        self.regular_queue = PriorityQueue()
    
    def add_customer(self, name, vip=False):
        """Agrega un cliente a la cola según su prioridad."""
        if vip:
            self.vip_queue.enqueue(name)
            print(f"Cliente VIP '{name}' agregado a la cola.")
        else:
            self.regular_queue.enqueue(name)
            print(f"Cliente Regular '{name}' agregado a la cola.")
    
    def attend_customer(self):
        """Atiende a un cliente según su prioridad."""
        if not self.vip_queue.is_empty():
            print(f"Atendiendo Cliente VIP: {self.vip_queue.dequeue()}")
        elif not self.regular_queue.is_empty():
            print(f"Atendiendo Cliente Regular: {self.regular_queue.dequeue()}")
        else:
            print("No hay clientes en espera.")
    
    def show_waiting_customers(self):
        """Muestra la cantidad de clientes en espera en cada cola."""
        print(f"Clientes en espera - VIP: {self.vip_queue.size()}, Regulares: {self.regular_queue.size()}")


# *Menú Principal*
def main():
    task_manager = TaskManager()
    customer_service = CustomerService()
    
    while True:
        print("\n--- MENÚ PRINCIPAL ---")
        print("1. Gestor de Tareas")
        print("2. Sistema de Atención al Cliente")
        print("3. Salir")
        opcion = input("Seleccione una opción: ")
        
        if opcion == "1":
            while True:
                print("\n--- GESTOR DE TAREAS ---")
                print("1. Agregar tarea")
                print("2. Procesar tarea")
                print("3. Ver tareas pendientes")
                print("4. Volver al menú principal")
                sub_opcion = input("Seleccione una opción: ")
                
                if sub_opcion == "1":
                    tarea = input("Ingrese la descripción de la tarea: ")
                    task_manager.add_task(tarea)
                elif sub_opcion == "2":
                    task_manager.process_task()
                elif sub_opcion == "3":
                    task_manager.show_pending_tasks()
                elif sub_opcion == "4":
                    break
                else:
                    print("Opción no válida. Intente de nuevo.")

        elif opcion == "2":
            while True:
                print("\n--- SISTEMA DE ATENCIÓN AL CLIENTE ---")
                print("1. Agregar cliente")
                print("2. Atender cliente")
                print("3. Ver clientes en espera")
                print("4. Volver al menú principal")
                sub_opcion = input("Seleccione una opción: ")
                
                if sub_opcion == "1":
                    nombre = input("Ingrese el nombre del cliente: ")
                    es_vip = input("¿Es VIP? (s/n): ").lower() == "s"
                    customer_service.add_customer(nombre, es_vip)
                elif sub_opcion == "2":
                    customer_service.attend_customer()
                elif sub_opcion == "3":
                    customer_service.show_waiting_customers()
                elif sub_opcion == "4":
                    break
                else:
                    print("Opción no válida. Intente de nuevo.")

        elif opcion == "3":
            print("Saliendo del programa...")
            break
        else:
            print("Opción no válida. Intente de nuevo.")


if __name__ == "__main__":
    main()
