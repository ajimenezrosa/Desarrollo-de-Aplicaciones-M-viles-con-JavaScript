
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


# 📱 Colección de Apps Simples (6–10) — React Native (sin Expo)

> **Uso en clase:** cada ejemplo es un único `App.js` listo para copiar/pegar sobre un proyecto creado con `npx react-native init`.  
> **Cómo correr (Android):**
> 1) `npx react-native init DemoApp`  
> 2) Reemplaza `App.js` por el de la app elegida  
> 3) Emulador/Dispositivo listo y ejecuta: `npx react-native start` (en una terminal)  
> 4) `npx react-native run-android` (en otra terminal)

---

## App 6: Generador de Nombres Aleatorios

**Objetivo:** mostrar un nombre aleatorio desde una lista predefinida.  
**Conceptos:** `useState`, arrays, eventos de botón.

### Código (`App.js`)
```javascript
import React, { useState } from 'react';
import { SafeAreaView, View, Text, TouchableOpacity, TextInput, FlatList, StyleSheet } from 'react-native';

export default function App() {
  const [names, setNames] = useState(["Alex", "María", "Carlos", "Lucía", "Pedro", "Ana"]);
  const [randomName, setRandomName] = useState("");
  const [newName, setNewName] = useState("");

  const handleGenerate = () => {
    if (names.length === 0) {
      setRandomName("No hay nombres en la lista");
      return;
    }
    const i = Math.floor(Math.random() * names.length);
    setRandomName(names[i]);
  };

  const handleAdd = () => {
    const clean = newName.trim();
    if (clean.length > 0) {
      setNames(prev => [...prev, clean]);
      setNewName("");
    }
  };

  const handleClear = () => {
    setNames([]);
    setRandomName("");
  };

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>🎲 Generador de Nombres</Text>

      <Text style={styles.result}>{randomName || "—"}</Text>

      <View style={styles.row}>
        <TouchableOpacity style={styles.btn} onPress={handleGenerate}>
          <Text style={styles.btnText}>Generar</Text>
        </TouchableOpacity>
        <TouchableOpacity style={[styles.btn, styles.btnSecondary]} onPress={handleClear}>
          <Text style={styles.btnText}>Limpiar</Text>
        </TouchableOpacity>
      </View>

      <View style={styles.card}>
        <Text style={styles.subtitle}>Agregar nombre</Text>
        <View style={styles.row}>
          <TextInput
            style={styles.input}
            placeholder="Nuevo nombre"
            value={newName}
            onChangeText={setNewName}
          />
          <TouchableOpacity style={styles.btn} onPress={handleAdd}>
            <Text style={styles.btnText}>Añadir</Text>
          </TouchableOpacity>
        </View>
      </View>

      <Text style={styles.subtitle}>Lista actual ({names.length}):</Text>
      <FlatList
        data={names}
        keyExtractor={(item, idx) => item + idx}
        renderItem={({ item }) => <Text style={styles.item}>• {item}</Text>}
        ListEmptyComponent={<Text style={styles.muted}>Sin nombres… agrega uno arriba.</Text>}
        style={{ alignSelf: 'stretch' }}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 20, gap: 16, backgroundColor: '#0f172a' },
  title: { fontSize: 22, fontWeight: '700', color: '#e2e8f0', textAlign: 'center' },
  subtitle: { fontSize: 16, fontWeight: '600', color: '#cbd5e1', marginBottom: 8 },
  result: { fontSize: 28, fontWeight: '800', color: '#22d3ee', textAlign: 'center', marginVertical: 8 },
  row: { flexDirection: 'row', gap: 10, alignItems: 'center' },
  btn: { backgroundColor: '#3b82f6', paddingVertical: 10, paddingHorizontal: 14, borderRadius: 12 },
  btnSecondary: { backgroundColor: '#ef4444' },
  btnText: { color: 'white', fontWeight: '700' },
  input: { flex: 1, backgroundColor: '#0b1220', borderColor: '#334155', borderWidth: 1, color: '#e2e8f0', padding: 10, borderRadius: 10 },
  card: { alignSelf: 'stretch', backgroundColor: '#0b1220', borderColor: '#1e293b', borderWidth: 1, padding: 12, borderRadius: 14 },
  item: { color: '#e2e8f0', paddingVertical: 4 },
  muted: { color: '#94a3b8', fontStyle: 'italic' },
});
````

---

## App 7: Contador de Pasos Simulado

**Objetivo:** simular un contador de pasos con incremento manual y barra de progreso a meta.
**Conceptos:** `useState`, cálculo de porcentaje, estilos dinámicos.

### Código (`App.js`)

```javascript
import React, { useState } from 'react';
import { SafeAreaView, View, Text, TouchableOpacity, StyleSheet } from 'react-native';

export default function App() {
  const GOAL = 5000; // Meta de pasos simulada
  const [steps, setSteps] = useState(0);

  const pct = Math.min(steps / GOAL, 1);
  const pctLabel = Math.round(pct * 100) + "%";

  const add = (n) => setSteps(prev => Math.max(prev + n, 0));
  const reset = () => setSteps(0);

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>👟 Contador de Pasos (Simulado)</Text>

      <Text style={styles.counter}>{steps} pasos</Text>
      <Text style={styles.meta}>Meta: {GOAL}</Text>

      <View style={styles.progress}>
        <View style={[styles.progressInner, { width: `${pct * 100}%` }]} />
      </View>
      <Text style={styles.percent}>{pctLabel}</Text>

      <View style={styles.row}>
        <TouchableOpacity style={styles.btn} onPress={() => add(100)}>
          <Text style={styles.btnText}>+100</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.btn} onPress={() => add(500)}>
          <Text style={styles.btnText}>+500</Text>
        </TouchableOpacity>
        <TouchableOpacity style={[styles.btn, styles.btnWarn]} onPress={reset}>
          <Text style={styles.btnText}>Reset</Text>
        </TouchableOpacity>
      </View>

      <Text style={styles.muted}>* Simula pasos para practicar UI/estado.</Text>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 20, gap: 16, backgroundColor: '#0f172a' },
  title: { fontSize: 22, fontWeight: '700', color: '#e2e8f0', textAlign: 'center' },
  counter: { fontSize: 40, fontWeight: '800', color: '#22d3ee', textAlign: 'center' },
  meta: { color: '#cbd5e1', textAlign: 'center' },
  progress: { height: 16, backgroundColor: '#0b1220', borderColor: '#1e293b', borderWidth: 1, borderRadius: 999, overflow: 'hidden' },
  progressInner: { height: '100%', backgroundColor: '#10b981' },
  percent: { color: '#e2e8f0', textAlign: 'center' },
  row: { flexDirection: 'row', gap: 10, alignItems: 'center', justifyContent: 'center' },
  btn: { backgroundColor: '#3b82f6', paddingVertical: 10, paddingHorizontal: 16, borderRadius: 12 },
  btnWarn: { backgroundColor: '#ef4444' },
  btnText: { color: 'white', fontWeight: '700' },
  muted: { color: '#94a3b8', textAlign: 'center', marginTop: 8, fontStyle: 'italic' },
});
```

---

## App 8: App de Frases Motivacionales

**Objetivo:** mostrar frases motivacionales aleatorias y permitir “favoritos” locales.
**Conceptos:** `useState`, listas, aleatoriedad simple.

### Código (`App.js`)

```javascript
import React, { useState } from 'react';
import { SafeAreaView, View, Text, TouchableOpacity, FlatList, StyleSheet } from 'react-native';

const PHRASES = [
  "Cree en ti; ya estás a mitad de camino.",
  "La disciplina supera al talento cuando el talento no se disciplina.",
  "Pequeños pasos, grandes resultados.",
  "El éxito es la suma de esfuerzos repetidos día tras día.",
  "Tu única limitación es tu mente."
];

export default function App() {
  const [current, setCurrent] = useState(PHRASES[0]);
  const [favs, setFavs] = useState([]);

  const nextRandom = () => {
    const i = Math.floor(Math.random() * PHRASES.length);
    setCurrent(PHRASES[i]);
  };

  const addFav = () => {
    if (!favs.includes(current)) setFavs(prev => [current, ...prev]);
  };

  const clearFavs = () => setFavs([]);

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>💡 Frases Motivacionales</Text>

      <View style={styles.card}>
        <Text style={styles.quote}>“{current}”</Text>
        <View style={styles.row}>
          <TouchableOpacity style={styles.btn} onPress={nextRandom}>
            <Text style={styles.btnText}>Otra frase</Text>
          </TouchableOpacity>
          <TouchableOpacity style={[styles.btn, styles.btnAlt]} onPress={addFav}>
            <Text style={styles.btnText}>Favorito</Text>
          </TouchableOpacity>
        </View>
      </View>

      <View style={styles.headerRow}>
        <Text style={styles.subtitle}>⭐ Favoritos ({favs.length})</Text>
        <TouchableOpacity onPress={clearFavs}>
          <Text style={styles.clear}>Limpiar</Text>
        </TouchableOpacity>
      </View>

      <FlatList
        data={favs}
        keyExtractor={(item, idx) => item + idx}
        renderItem={({ item }) => <Text style={styles.item}>• {item}</Text>}
        ListEmptyComponent={<Text style={styles.muted}>Sin favoritos aún.</Text>}
        style={{ alignSelf: 'stretch' }}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 20, gap: 16, backgroundColor: '#0f172a' },
  title: { fontSize: 22, fontWeight: '700', color: '#e2e8f0', textAlign: 'center' },
  card: { backgroundColor: '#0b1220', borderColor: '#1e293b', borderWidth: 1, padding: 16, borderRadius: 16, gap: 12 },
  quote: { color: '#22d3ee', fontSize: 18, fontStyle: 'italic' },
  row: { flexDirection: 'row', gap: 10 },
  headerRow: { flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center' },
  subtitle: { fontSize: 16, fontWeight: '700', color: '#cbd5e1' },
  btn: { backgroundColor: '#3b82f6', paddingVertical: 10, paddingHorizontal: 14, borderRadius: 12 },
  btnAlt: { backgroundColor: '#10b981' },
  btnText: { color: 'white', fontWeight: '700' },
  item: { color: '#e2e8f0', paddingVertical: 6 },
  muted: { color: '#94a3b8', fontStyle: 'italic' },
  clear: { color: '#ef4444', fontWeight: '700' },
});
```

---

## App 9: Cambio de Fondo de Pantalla

**Objetivo:** alternar el color de fondo de la app desde una paleta predefinida.
**Conceptos:** `useState`, estilos condicionados, arrays.

### Código (`App.js`)

```javascript
import React, { useState } from 'react';
import { SafeAreaView, View, Text, TouchableOpacity, StyleSheet } from 'react-native';

const PALETTE = [
  '#0f172a', // azul oscuro
  '#111827', // gris-azul
  '#1f2937', // pizarra
  '#0b1220', // fondo panel
  '#022c22', // verde profundo
  '#1e1b4b', // púrpura oscuro
];

export default function App() {
  const [idx, setIdx] = useState(0);

  const next = () => setIdx((prev) => (prev + 1) % PALETTE.length);
  const prev = () => setIdx((prev) => (prev - 1 + PALETTE.length) % PALETTE.length);

  const bg = { backgroundColor: PALETTE[idx] };

  return (
    <SafeAreaView style={[styles.container, bg]}>
      <View style={styles.center}>
        <Text style={styles.title}>🖼️ Cambiar Fondo</Text>
        <Text style={styles.code}>{PALETTE[idx]}</Text>

        <View style={styles.row}>
          <TouchableOpacity style={[styles.btn, styles.btnAlt]} onPress={prev}>
            <Text style={styles.btnText}>Anterior</Text>
          </TouchableOpacity>
          <TouchableOpacity style={styles.btn} onPress={next}>
            <Text style={styles.btnText}>Siguiente</Text>
          </TouchableOpacity>
        </View>

        <View style={styles.previewRow}>
          {PALETTE.map((c, i) => (
            <View
              key={c}
              style={[
                styles.dot,
                { backgroundColor: c, borderWidth: i === idx ? 2 : 0 }
              ]}
            />
          ))}
        </View>
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1 },
  center: { flex: 1, alignItems: 'center', justifyContent: 'center', gap: 12, padding: 20 },
  title: { fontSize: 22, fontWeight: '800', color: '#e2e8f0' },
  code: { color: '#22d3ee', fontWeight: '700' },
  row: { flexDirection: 'row', gap: 10 },
  btn: { backgroundColor: '#3b82f6', paddingVertical: 10, paddingHorizontal: 16, borderRadius: 12 },
  btnAlt: { backgroundColor: '#10b981' },
  btnText: { color: 'white', fontWeight: '700' },
  previewRow: { flexDirection: 'row', gap: 8, marginTop: 12, flexWrap: 'wrap', justifyContent: 'center' },
  dot: { width: 28, height: 28, borderRadius: 999, borderColor: '#e2e8f0' },
});
```

---

## App 10: Mini Trivia

**Objetivo:** preguntas de opción múltiple, puntaje y fin de juego básico.
**Conceptos:** `useState`, render condicional, arrays de objetos.

### Código (`App.js`)

```javascript
import React, { useState } from 'react';
import { SafeAreaView, View, Text, TouchableOpacity, StyleSheet } from 'react-native';

const QUESTIONS = [
  {
    q: "¿Cuál es el lenguaje de programación usado por React Native?",
    options: ["Java", "Swift", "JavaScript", "Kotlin"],
    answer: 2,
  },
  {
    q: "¿Qué hook se usa para manejar estado en componentes funcionales?",
    options: ["useEffect", "useState", "useMemo", "useRef"],
    answer: 1,
  },
  {
    q: "¿Qué componente se usa para listas performantes?",
    options: ["ListView", "ScrollView", "FlatList", "Image"],
    answer: 2,
  },
];

export default function App() {
  const [idx, setIdx] = useState(0);
  const [score, setScore] = useState(0);
  const [selected, setSelected] = useState(null);
  const [finished, setFinished] = useState(false);

  const current = QUESTIONS[idx];

  const choose = (i) => setSelected(i);

  const next = () => {
    if (selected === null) return;
    if (selected === current.answer) setScore(s => s + 1);

    setSelected(null);
    if (idx + 1 < QUESTIONS.length) {
      setIdx(i => i + 1);
    } else {
      setFinished(true);
    }
  };

  const reset = () => {
    setIdx(0);
    setScore(0);
    setSelected(null);
    setFinished(false);
  };

  if (finished) {
    return (
      <SafeAreaView style={styles.container}>
        <Text style={styles.title}>🎉 ¡Completado!</Text>
        <Text style={styles.score}>Puntaje: {score} / {QUESTIONS.length}</Text>
        <TouchableOpacity style={styles.btn} onPress={reset}>
          <Text style={styles.btnText}>Reintentar</Text>
        </TouchableOpacity>
      </SafeAreaView>
    );
  }

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>❓ Mini Trivia</Text>
      <Text style={styles.progress}>Pregunta {idx + 1} de {QUESTIONS.length}</Text>

      <View style={styles.card}>
        <Text style={styles.question}>{current.q}</Text>

        {current.options.map((opt, i) => {
          const isSel = selected === i;
          return (
            <TouchableOpacity
              key={i}
              style={[styles.option, isSel && styles.optionSel]}
              onPress={() => choose(i)}
            >
              <Text style={styles.optionText}>{opt}</Text>
            </TouchableOpacity>
          );
        })}

        <TouchableOpacity style={[styles.btn, selected === null && styles.btnDisabled]} onPress={next} disabled={selected === null}>
          <Text style={styles.btnText}>{idx + 1 === QUESTIONS.length ? "Finalizar" : "Siguiente"}</Text>
        </TouchableOpacity>
      </View>

      <Text style={styles.muted}>* Marca una respuesta y continúa.</Text>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 20, gap: 16, backgroundColor: '#0f172a' },
  title: { fontSize: 22, fontWeight: '800', color: '#e2e8f0', textAlign: 'center' },
  progress: { color: '#cbd5e1', textAlign: 'center' },
  card: { backgroundColor: '#0b1220', borderColor: '#1e293b', borderWidth: 1, padding: 16, borderRadius: 16, gap: 12 },
  question: { color: '#e2e8f0', fontSize: 18, fontWeight: '700' },
  option: { backgroundColor: '#111827', borderColor: '#1f2937', borderWidth: 1, padding: 12, borderRadius: 12 },
  optionSel: { backgroundColor: '#334155', borderColor: '#475569' },
  optionText: { color: '#e2e8f0' },
  btn: { backgroundColor: '#3b82f6', paddingVertical: 12, borderRadius: 12, alignItems: 'center' },
  btnDisabled: { opacity: 0.5 },
  btnText: { color: 'white', fontWeight: '800' },
  score: { color: '#22d3ee', fontSize: 20, textAlign: 'center', marginBottom: 12 },
  muted: { color: '#94a3b8', textAlign: 'center', fontStyle: 'italic' },
});
```

---
