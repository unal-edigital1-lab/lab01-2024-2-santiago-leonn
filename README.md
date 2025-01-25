# lab01- sumador 
## Santiago León Naranjo

### sumador 1 bit

### Suma de bits con acarreo usando operaciones lógicas básicas.

```verilog
module sum1bcc_primitive (A, B, Ci, Cout, S);

  // Declaración de puertos de entrada
  input  A;   // Primer bit de entrada
  input  B;   // Segundo bit de entrada
  input  Ci;  // Acarreo de entrada
  
  // Declaración de puertos de salida
  output Cout; // Acarreo de salida
  output S;    // Resultado de la suma

  // Declaración de cables intermedios
  wire a_ab;    // Cable para el resultado de AND entre A y B
  wire x_ab;    // Cable para el resultado de XOR entre A y B
  wire cout_t;  // Cable para el acarreo temporal

  // Operación AND entre A y B
  and(a_ab, A, B);

  // Operación XOR entre A y B
  xor(x_ab, A, B);

  // Operación XOR entre el resultado de XOR anterior y Ci
  xor(S, x_ab, Ci);

  // Operación AND entre el resultado de XOR anterior y Ci
  and(cout_t, x_ab, Ci);

  // Operación OR entre el acarreo temporal y el resultado de AND entre A y B
  or (Cout, cout_t, a_ab);

endmodule
```

###Suma simple con acarreo utilizando un registro para almacenar el resultado de la operación

```verilog
module sum1bcc (A, B, Ci, Cout, S);

  // Declaración de puertos de entrada
  input  A;   // Primer bit de entrada
  input  B;   // Segundo bit de entrada
  input  Ci;  // Acarreo de entrada
  
  // Declaración de puertos de salida
  output Cout; // Acarreo de salida
  output S;    // Resultado de la suma

  // Declaración de un registro de 2 bits para almacenar el resultado de la suma
  reg [1:0] st;

  // Asignación del bit menos significativo del registro 'st' a la salida 'S'
  assign S = st[0];

  // Asignación del bit más significativo del registro 'st' a la salida 'Cout'
  assign Cout = st[1];

  // Bloque 'always' que se ejecuta siempre que haya un cambio en cualquiera de las entradas
  always @ ( * ) begin
    // Realiza la suma de A, B y Ci y almacena el resultado en el registro 'st'
    st  <=   A + B + Ci;
  end
  
endmodule
```
