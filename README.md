## Actividades Sasinka Cristian

ordenadas por ramas y dias

## Relaciones de Jerarquía en el Modelo POO

En el patrón de diseño implementado, la clase `Aeroplano` actúa como clase padre o contenedor, mientras que los componentes estructurales del mismo (Turbina, Helice, Tren de Aterrizaje, Cubierta y Alas) representan las clases parte que la integran.

### Tipos de Relaciones

Las relaciones entre la clase contenedor y sus componentes pueden establecerse de dos formas:

1. **Relación de Composición**: El componente es creado y gestionado exclusivamente por la clase contenedor. Su ciclo de vida depende completamente del objeto padre.
2. **Relación de Agregación**: El componente existe independientemente y es inyectado como dependencia en el constructor del objeto padre.

### Implementación en Código

En la implementación actual, todas las relaciones son de **agregación**, ya que los componentes son recibidos como parámetros en el constructor:

```typescript
constructor(phelice: Helice, pTrenAterrizaje: TrendeAterrizaje, pAlas: Alas, pCubierta: Cubierta) {
     this.helice = phelice;
     this.trenAterrizaje = pTrenAterrizaje;
     this.alas = pAlas;
     this.cubierta = pCubierta;
}
```

Para convertir una relación a **composición**, el componente debe ser instanciado internamente por la clase contenedor:

```typescript
class Aeroplano {
    private helice: Helice;
    private trenAterrizaje: TrendeAterrizaje;
    private alas: Alas;
    private cubierta: Cubierta;
    private turbina: Turbina;

    constructor(phelice: Helice, pTrenAterrizaje: TrendeAterrizaje, pAlas: Alas, pCubierta: Cubierta) {
         this.helice = phelice;
         this.trenAterrizaje = pTrenAterrizaje;
         this.alas = pAlas;
         this.cubierta = pCubierta;
         this.turbina = new Turbina(4);
    }

    public ToString(): string {
        let mensaje = "Aeroplano compuesto por: ";
        mensaje += this.helice.ToString();
        mensaje += this.alas.ToString();
        mensaje += this.trenAterrizaje.ToString();
        mensaje += this.cubierta.ToString();
        mensaje += this.turbina.ToString();
        return mensaje;
    }
}
```

### Diferencias Técnicas: Composición vs Agregación

#### Ciclo de Vida de los Componentes

- **Composición**: El componente se instancia junto con el objeto padre y es destruido conjuntamente con este. Ejemplo: al eliminar el avión, la turbina también se elimina.
- **Agregación**: Los componentes existen independientemente. Si se destruye el avión, los componentes (hélices, tren de aterrizaje, cubierta) продолжа existiendo en el sistema.

#### Gestión de Memoria

- **Composición**: Más eficiente y segura, ya que no genera memory leaks ni residuos de objetos huérfanos.
- **Agregación**: Requiere gestión manual explícita para evitar fugas de memoria, dado que los objetos componentes Persisten después de la destrucción del contenedor.

#### Visibilidad

- **Composición**: Los componentes suelen ser internos e invisibles para otros objetos del sistema.
- **Agregación**: Los componentes remain visibles y reutilizables por otras partes del sistema.