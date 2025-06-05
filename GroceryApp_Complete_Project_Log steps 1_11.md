
# GroceryApp – Registro Completo dello Sviluppo (Steps 1-11)

---

## ✅ Step 1: Installazione ambiente di sviluppo

- Installato Android Studio.
- Creato nuovo progetto `GroceryApp` in Kotlin, Min SDK: API 26.
- Verificato l'avvio e compilazione su emulatore Android.

---

## ✅ Step 2: Struttura Architetturale (MVVM)

- Creati package:
  - `data`, `network`, `ui.shoppinglist`, `ui.recipes`, `utils`, `viewmodel`
- Struttura conforme al pattern MVVM.

---

## ✅ Step 3: Prima UI – Shopping List

- Composable `ShoppingListScreen.kt` con lista fissa e titolo statico.
- Visualizzata via `MainActivity.kt`.

---

## ✅ Step 4: ViewModel per lista dinamica

- `ShoppingListViewModel.kt` con `mutableStateListOf`.
- UI collegata al ViewModel, input `OutlinedTextField` e bottone "Add".
- Aggiornamento reattivo automatico.

---

## ✅ Step 5: Persistenza con DataStore

- `ShoppingListRepository.kt` usa `preferencesDataStore` e formato CSV.
- Dipendenze:
  ```kotlin
  implementation("androidx.datastore:datastore-preferences:1.0.0")
  implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3")
  ```

---

## ✅ Step 6-7: Integrazione Persistenza

- ViewModel integrato con Repository.
- Testata lettura/scrittura persistente della lista.

---

## ✅ Step 8: Supporto Multi-Lista

- `Map<String, List<String>>` in `ShoppingListRepository.kt`.
- Serializzazione JSON (`kotlinx.serialization`).
- UI: selettore lista (`DropdownMenu`), crea/rinomina/elimina, `SwipeToDismiss`.
- Dipendenze:
  ```kotlin
  implementation("org.jetbrains.kotlinx:kotlinx-serialization-json:1.5.1")
  implementation("androidx.compose.material:material-icons-extended:1.5.4")
  ```

---

## ✅ Step 9: Navigazione e Modulo Ricette

- `BottomNavigation` con due tab: Lista & Ricette.
- `RecipesScreen.kt`, `RecipesViewModel.kt`, `RecipesRepository.kt`.
- Persistenza ricette via DataStore (key: `recipes_json`).

---

## ✅ Step 10: Ordinamento e UI Responsive

- `ShoppingListViewModel.kt`: funzioni `sortAZ`, `sortZA`.
- `ShoppingListScreen.kt`: pulsanti ordinamento.
- Tema `GroceryAppTheme.kt` con supporto chiaro/scuro.

---

## ✅ Step 11: UX Avanzata & Reorderable List

- Componente `ReorderableShoppingList.kt` con drag & drop.
- Persistenza ordine integrata.
- `MainActivity.kt` con `Scaffold` e `TopAppBar`.
- Fix warning Kotlin (import, nomi, compatibilità Compose).
- Pianificato:
  - `TextField` per nuovi elementi
  - `Snackbar` con Undo
  - Dropdown per multi-liste

---

## 🚧 Problemi Ricorrenti & Soluzioni

- ❌ **Persistenza non visibile immediatamente** → Soluzione: sincronizzazione post-load nel ViewModel.
- ❌ **Warning su parole italiane** → Ignorati, validi solo per spell-check IDE.
- ❌ **Import inutilizzati** → Risolto con `Optimize Imports`.

---

## 🔚 Stato Attuale

- Architettura MVVM completa
- UI responsive e navigabile
- Persistenza asincrona locale (DataStore)
- Moduli: Liste della spesa, Ricette, Ordine drag & drop

