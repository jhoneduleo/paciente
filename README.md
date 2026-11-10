 [paciente.py](https://github.com/user-attachments/files/34652202/paciente.py)
class Paciente:
    """Representa un paciente y guarda cada instancia en Paciente.txt."""

    ARCHIVO = "Paciente.txt"

    def __init__(self, identificacion, nombre, edad, motivo_consulta):
        self.identificacion = str(identificacion)
        self.nombre = nombre.strip()
        self.edad = int(edad)
        self.motivo_consulta = motivo_consulta.strip()
        self.guardar_en_archivo()

    def guardar_en_archivo(self):
        """Agrega los datos del paciente al archivo de texto."""
        with open(self.ARCHIVO, "a", encoding="utf-8") as archivo:
            archivo.write(
                f"{self.identificacion}|{self.nombre}|{self.edad}|"
                f"{self.motivo_consulta}\n"
            )

    @classmethod
    def listar_pacientes(cls):
        """Devuelve los registros guardados; si no existe, retorna lista vacía."""
        try:
            with open(cls.ARCHIVO, "r", encoding="utf-8") as archivo:
                return [linea.strip().split("|") for linea in archivo if linea.strip()]
        except FileNotFoundError:
            return []


if __name__ == "__main__":
    Paciente(
        input("Identificación: "),
        input("Nombre completo: "),
        input("Edad: "),
        input("Motivo de consulta: ")
    )
    print("Paciente guardado correctamente en Paciente.txt")
    print("\nPacientes registrados:")
    for registro in Paciente.listar_pacientes():
        print(" | ".join(registro))
