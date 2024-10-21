
# **Manual de Desarrollo de Aplicaciones Móviles con React Native usando npx react-native**

## **Índice**

1. [Contador de Clics](#app-1-contador-de-clics)
2. [Calculadora de Propinas](#app-2-calculadora-de-propinas)
3. [Conversor de Monedas](#app-3-conversor-de-monedas)
4. [Recordatorio de Tareas](#app-4-recordatorio-de-tareas)
5. [Calculadora Simple](#app-5-calculadora-simple)
6. [Generador de Nombres Aleatorios](#app-6-generador-de-nombres-aleatorios)
7. [Contador de Pasos Simulado](#app-7-contador-de-pasos-simulado)
8. [App de Frases Motivacionales](#app-8-app-de-frases-motivacionales)
9. [Cambio de Fondo de Pantalla](#app-9-cambio-de-fondo-de-pantalla)
10. [Mini Trivia](#app-10-mini-trivia)

---

## **App 1: Contador de Clics**

#### **Descripción**:
Una aplicación simple que cuenta cuántas veces el usuario presiona un botón.

#### **Explicación del código:**
- `useState`: Usamos este hook para manejar el estado del contador. Inicialmente, el contador está en `0`.
- `Button`: El botón tiene una propiedad `onPress`, que se activa cada vez que se presiona. Al presionar el botón, se incrementa el valor del contador o se reinicia.
- `Text`: Este componente muestra cuántas veces se ha presionado el botón.

#### **Código completo:**

```jsx
import React, { useState } from 'react';
import { SafeAreaView, StyleSheet, Text, Button } from 'react-native';

const App = () => {
  const [count, setCount] = useState(0);

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.text}>Has presionado {count} veces</Text>
      <Button title="Haz clic aquí" onPress={() => setCount(count + 1)} />
      <Button title="Reiniciar" onPress={() => setCount(0)} />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  text: {
    fontSize: 24,
    marginBottom: 20,
  },
});

export default App;
```

---

## **App 2: Calculadora de Propinas**

#### **Descripción**:
Calcula la cantidad de propina según el total de la cuenta y el porcentaje deseado.

#### **Explicación del código:**
- `useState`: Maneja los valores del monto de la cuenta (`bill`), el porcentaje de propina (`tipPercentage`), y el total calculado (`total`).
- `TextInput`: Permite al usuario ingresar el monto de la cuenta y el porcentaje de propina.
- `Button`: Al presionarlo, se ejecuta la función `calculateTip` que calcula la propina y muestra el total.

#### **Código completo:**

```jsx
import React, { useState } from 'react';
import { SafeAreaView, StyleSheet, Text, TextInput, Button } from 'react-native';

const App = () => {
  const [bill, setBill] = useState('');
  const [tipPercentage, setTipPercentage] = useState(10);
  const [total, setTotal] = useState(null);

  const calculateTip = () => {
    const tip = (parseFloat(bill) * tipPercentage) / 100;
    const totalAmount = parseFloat(bill) + tip;
    setTotal(totalAmount.toFixed(2));
  };

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>Calculadora de Propinas</Text>
      <TextInput
        style={styles.input}
        placeholder="Monto de la cuenta"
        keyboardType="numeric"
        value={bill}
        onChangeText={setBill}
      />
      <TextInput
        style={styles.input}
        placeholder="Porcentaje de propina"
        keyboardType="numeric"
        value={String(tipPercentage)}
        onChangeText={(value) => setTipPercentage(parseInt(value))}
      />
      <Button title="Calcular" onPress={calculateTip} />
      {total && <Text style={styles.result}>Total a pagar: ${total}</Text>}
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    paddingHorizontal: 20,
  },
  title: {
    fontSize: 24,
    textAlign: 'center',
    marginBottom: 20,
  },
  input: {
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    marginBottom: 10,
    paddingHorizontal: 10,
  },
  result: {
    marginTop: 20,
    fontSize: 18,
    textAlign: 'center',
  },
});

export default App;
```

---

## **App 3: Conversor de Monedas**

#### **Descripción**:
Convierte valores entre dos monedas predeterminadas (por ejemplo, de USD a EUR).

#### **Explicación del código:**
- `useState`: Se utiliza para manejar la cantidad a convertir y el resultado de la conversión.
- `TextInput`: Permite al usuario ingresar la cantidad a convertir.
- `conversionRate`: Tasa de conversión fija de USD a EUR en este ejemplo.
- `Button`: Realiza la conversión cuando es presionado.

#### **Código completo:**

```jsx
import React, { useState } from 'react';
import { SafeAreaView, StyleSheet, Text, TextInput, Button } from 'react-native';

const App = () => {
  const [amount, setAmount] = useState('');
  const [converted, setConverted] = useState(null);
  const conversionRate = 1.2; // USD a EUR

  const convertCurrency = () => {
    const result = (parseFloat(amount) * conversionRate).toFixed(2);
    setConverted(result);
  };

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>Conversor de Monedas</Text>
      <TextInput
        style={styles.input}
        placeholder="Cantidad en USD"
        keyboardType="numeric"
        value={amount}
        onChangeText={setAmount}
      />
      <Button title="Convertir" onPress={convertCurrency} />
      {converted && <Text style={styles.result}>EUR: {converted}</Text>}
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    paddingHorizontal: 20,
  },
  title: {
    fontSize: 24,
    textAlign: 'center',
    marginBottom: 20,
  },
  input: {
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    marginBottom: 10,
    paddingHorizontal: 10,
  },
  result: {
    marginTop: 20,
    fontSize: 18,
    textAlign: 'center',
  },
});

export default App;
```

---

## **App 4: Recordatorio de Tareas**

#### **Descripción**:
Una aplicación para gestionar y eliminar tareas.

#### **Explicación del código:**
- `useState`: Maneja las tareas ingresadas por el usuario y la lista de tareas.
- `FlatList`: Muestra las tareas en una lista que se actualiza dinámicamente.
- `Button`: Se utiliza para añadir tareas y eliminarlas al ser presionadas.

#### **Código completo:**

```jsx
import React, { useState } from 'react';
import { SafeAreaView, StyleSheet, Text, TextInput, Button, FlatList } from 'react-native';

const App = () => {
  const [task, setTask] = useState('');
  const [tasks, setTasks] = useState([]);

  const addTask = () => {
    setTasks([...tasks, { key: Math.random().toString(), value: task }]);
    setTask('');
  };

  const removeTask = (key) => {
    setTasks((prevTasks) => prevTasks.filter(task => task.key !== key));
  };

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>Recordatorio de Tareas</Text>
      <TextInput
        style={styles.input}
        placeholder="Añadir tarea"
        value={task}
        onChangeText={setTask}
      />
      <Button title="Añadir" onPress={addTask} />
      <FlatList
        data={tasks}
        renderItem={({ item }) => (
          <Text onPress={() => removeTask(item.key)} style={styles.task}>{item.value}</Text>
        )}
      />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    paddingHorizontal: 20,


  },
  title: {
    fontSize: 24,
    textAlign: 'center',
    marginBottom: 20,
  },
  input: {
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    marginBottom: 10,
    paddingHorizontal: 10,
  },
  task: {
    fontSize: 18,
    marginTop: 10,
    padding: 10,
    backgroundColor: '#f8f8f8',
  },
});

export default App;
```

---

## **App 5: Calculadora Simple**

#### **Descripción**:
Calculadora que realiza operaciones básicas de suma, resta, multiplicación y división.

#### **Explicación del código:**
- `useState`: Para manejar los valores ingresados por el usuario y el resultado.
- `TextInput`: Permite al usuario ingresar números para las operaciones.
- `Button`: Realiza la operación seleccionada.

#### **Código completo:**

```jsx
import React, { useState } from 'react';
import { SafeAreaView, StyleSheet, Text, TextInput, Button, View } from 'react-native';

const App = () => {
  const [num1, setNum1] = useState('');
  const [num2, setNum2] = useState('');
  const [result, setResult] = useState(null);

  const handleOperation = (operation) => {
    const number1 = parseFloat(num1);
    const number2 = parseFloat(num2);
    let res = 0;

    switch (operation) {
      case 'sum':
        res = number1 + number2;
        break;
      case 'subtract':
        res = number1 - number2;
        break;
      case 'multiply':
        res = number1 * number2;
        break;
      case 'divide':
        res = number1 / number2;
        break;
      default:
        break;
    }
    setResult(res);
  };

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>Calculadora Simple</Text>
      <TextInput
        style={styles.input}
        placeholder="Número 1"
        keyboardType="numeric"
        value={num1}
        onChangeText={setNum1}
      />
      <TextInput
        style={styles.input}
        placeholder="Número 2"
        keyboardType="numeric"
        value={num2}
        onChangeText={setNum2}
      />
      <View style={styles.buttonContainer}>
        <Button title="Sumar" onPress={() => handleOperation('sum')} />
        <Button title="Restar" onPress={() => handleOperation('subtract')} />
        <Button title="Multiplicar" onPress={() => handleOperation('multiply')} />
        <Button title="Dividir" onPress={() => handleOperation('divide')} />
      </View>
      {result !== null && <Text style={styles.result}>Resultado: {result}</Text>}
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    paddingHorizontal: 20,
  },
  title: {
    fontSize: 24,
    textAlign: 'center',
    marginBottom: 20,
  },
  input: {
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    marginBottom: 10,
    paddingHorizontal: 10,
  },
  buttonContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 20,
  },
  result: {
    fontSize: 18,
    textAlign: 'center',
  },
});

export default App;
```

---

Con esta estructura, tus estudiantes podrán seguir los pasos y comprender el propósito de cada bloque de código. ¿Te gustaría que lo exportara en formato Markdown para su publicación directa en GitHub?