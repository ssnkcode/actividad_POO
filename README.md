## Actividades Sasinka Cristian ##

ordenadas por ramas y dias

## Relaciones de jerarquia

el modelo padre seria aeroplano, luego contamos con las diferentes partes del mismo, turbina, helice, tren de aterrizaje, cubierta y alas

las alas, la cubierta, el tren de aterrizaje forman una relacion de composicion, mientras que la helice y turbina forma una relacion de agregacion.

ahora desde el codigo, vemos que todas las relaciones son de agregacion ya que todas las demas partes se envian como argumentos para el constructor de la clase aeroplano

constructor ( phelice:Helice,  pTrenAterrizaje:TrendeAterrizaje,  pAlas:Alas,  pCubierta:Cubierta)
    {
         this.helice = phelice;
         this.trenAterrizaje = pTrenAterrizaje;
         this.alas = pAlas;
         this.cubierta = pCubierta;
    }
para que sea una relacion de composicion, podriamos editar la clase aeroplano, para que se cree dentro la turbina que utilizaremos, que no hace uso de la misma,

en ese caso el codigo quedaria:

class Aeroplano
{
    private  helice: Helice ;
    private  trenAterrizaje:TrendeAterrizaje;
    private  alas: Alas ;
    private  cubierta:Cubierta ;
    private  turbina:Turbina;
    constructor( phelice:Helice,  pTrenAterrizaje:TrendeAterrizaje,  pAlas:Alas,  pCubierta:Cubierta)
    {
         this.helice = phelice;
         this.trenAterrizaje = pTrenAterrizaje;
         this.alas = pAlas;
         this.cubierta = pCubierta;
         this.turbina = new Turbina(4);
    }
    public  ToString()
    {
        let mensaje = "Aeroplano compuesto por: ";
        mensaje += this.helice.ToString();
        mensaje += this.alas.ToString();
        mensaje += this.trenAterrizaje.ToString();
        mensaje += this.cubierta.ToString();
        mensaje += this.turbina.ToString();
        return mensaje;

    }
}
¿Cuál es la diferencia en tiempo de ejecución de la asociación por Composición y la asociación por Agregación?
Ciclo de vida de los componentes:
cuando se crea el aeroplano, al tener una relacion de composicion con la turbina, ambos se crean y destruyen al mismo tiempo. Con las helices, cubierta, tren de aterrizaje, se crean antes, pero si se destruye el avion, los mismos siguen "vivos" en nuestro sistema.

Memoria:
con respecto a la memoria, la relacion de composicion es mas eficiente debido a que no deja residuos accidentales cuando eliminamos al objeto padre, ya que tambien se eliminan los componentes internos. en la relacion de agregacion es mas peligroso y requiere que seamos mas cuidadosos ya que la eliminacion del objeto padre no elimina consigo a los elementos internos y pueden quedar indefinidamente en el sistema.

Visibilidad:
en composicion las partes son invisibles, o suelen serlo, para el resto del sistema, mientras que las partes en agregacion son visibles
