State
public interface IState
{
    void HandleRequest(Context context);
}
public class ConcreteStateA : IState
{
    public void HandleRequest(Context context)
    {
        Console.WriteLine("State A handling request");
        context.State = new ConcreteStateB(); // Cambiar el estado al siguiente
    }
}

public class ConcreteStateB : IState
{
    public void HandleRequest(Context context)
    {
        Console.WriteLine("State B handling request");
        context.State = new ConcreteStateA(); // Cambiar el estado al siguiente
    }
}
public class Context
{
    public IState State { get; set; }

    public Context(IState initialState)
    {
        State = initialState;
    }

    public void Request()
    {
        State.HandleRequest(this);
    }
}
class Program
{
    static void Main(string[] args)
    {
        Context context = new Context(new ConcreteStateA()); // Empezamos con el estado A

        // Realizamos varias solicitudes que cambiarán el estado
        context.Request();  // Salida: State A handling request
        context.Request();  // Salida: State B handling request
        context.Request();  // Salida: State A handling request
    }
}

Strategy
public interface IComportamiento
{
    void Ejecutar();
}
public class ComportamientoA : IComportamiento
{
    public void Ejecutar()
    {
        Console.WriteLine("Ejecutando Comportamiento A");
    }
}

public class ComportamientoB : IComportamiento
{
    public void Ejecutar()
    {
        Console.WriteLine("Ejecutando Comportamiento B");
    }
}
public class Contexto
{
    private IComportamiento _comportamiento;

    // Constructor para establecer la estrategia inicial
    public Contexto(IComportamiento comportamiento)
    {
        _comportamiento = comportamiento;
    }

    // Método para cambiar la estrategia en tiempo de ejecución
    public void CambiarComportamiento(IComportamiento nuevoComportamiento)
    {
        _comportamiento = nuevoComportamiento;
    }

    // Ejecutar el comportamiento actual
    public void EjecutarComportamiento()
    {
        _comportamiento.Ejecutar();
    }
}
public class Program
{
    public static void Main()
    {
        // Crear el contexto con un comportamiento inicial
        Contexto contexto = new Contexto(new ComportamientoA());
        
        // Ejecutar el comportamiento inicial
        contexto.EjecutarComportamiento();
        
        // Cambiar el comportamiento a otro
        contexto.CambiarComportamiento(new ComportamientoB());
        
        // Ejecutar el nuevo comportamiento
        contexto.EjecutarComportamiento();
    }
}
Ejecutando Comportamiento A
Ejecutando Comportamiento B

