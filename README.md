class Producto:
    def __init__(self, id_producto, nombre, categoria, cantidad, precio, proveedor):
        self.id_producto = id_producto
        self.nombre = nombre
        self.categoria = categoria
        self.cantidad = cantidad
        self.precio = precio
        self.proveedor = proveedor

class Inventario:
    def __init__(self):
        self.productos = {}

    def agregar_producto(self, producto):
        if producto.id_producto in self.productos:
            print(f"El producto con ID {producto.id_producto} ya existe.")
        else:
            self.productos[producto.id_producto] = producto
            print(f"Producto '{producto.nombre}' agregado correctamente.")

    def actualizar_producto(self, id_producto, cantidad):
        if id_producto in self.productos:
            self.productos[id_producto].cantidad += cantidad
            print(f"Cantidad actualizada. Nueva cantidad de '{self.productos[id_producto].nombre}': {self.productos[id_producto].cantidad}.")
        else:
            print(f"Producto con ID {id_producto} no encontrado.")

    def eliminar_producto(self, id_producto):
        if id_producto in self.productos:
            eliminado = self.productos.pop(id_producto)
            print(f"Producto '{eliminado.nombre}' eliminado del inventario.")
        else:
            print(f"Producto con ID {id_producto} no encontrado.")

    def mostrar_inventario(self):
        if not self.productos:
            print("El inventario está vacío.")
        else:
            print("Inventario actual:")
            for producto in self.productos.values():
                print(f"ID: {producto.id_producto}, Nombre: {producto.nombre}, Categoría: {producto.categoria}, Cantidad: {producto.cantidad}, Precio: ${producto.precio}, Proveedor: {producto.proveedor}")


# Ejemplo de uso
def menu():
    inventario = Inventario()

    while True:
        print("\n----- MENÚ DEL SISTEMA DE INVENTARIO -----")
        print("1. Agregar Producto")
        print("2. Actualizar Cantidad de Producto")
        print("3. Eliminar Producto")
        print("4. Mostrar Inventario")
        print("5. Salir")
        opcion = input("Selecciona una opción: ")

        if opcion == '1':
            id_producto = input("ID del producto: ")
            nombre = input("Nombre del producto: ")
            categoria = input("Categoría del producto: ")
            cantidad = int(input("Cantidad en stock: "))
            precio = float(input("Precio unitario: "))
            proveedor = input("Proveedor: ")
            producto = Producto(id_producto, nombre, categoria, cantidad, precio, proveedor)
            inventario.agregar_producto(producto)

        elif opcion == '2':
            id_producto = input("ID del producto a actualizar: ")
            cantidad = int(input("Cantidad a añadir o restar (usa valores negativos para restar): "))
            inventario.actualizar_producto(id_producto, cantidad)

        elif opcion == '3':
            id_producto = input("ID del producto a eliminar: ")
            inventario.eliminar_producto(id_producto)

        elif opcion == '4':
            inventario.mostrar_inventario()

        elif opcion == '5':
            print("Saliendo del sistema...")
            break

        else:
            print("Opción no válida, intenta nuevamente.")


if __name__ == "__main__":
    menu()
