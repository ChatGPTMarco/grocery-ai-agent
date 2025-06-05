# GroceryApp – Project Development Log

## ✅ Step 8: Supporto Multi-Lista per la Spesa (Persistenza e UI)

### 🎯 Obiettivo
Permettere all'utente di gestire più liste della spesa distinte, ognuna con un nome proprio, con salvataggio persistente locale e interfaccia dinamica.

---

### 🧱 Modifiche Architetturali

#### 🔄 Repository – `ShoppingListRepository.kt`
- Sostituzione della singola lista con una struttura `Map<String, List<String>>`
- Serializzazione JSON tramite `kotlinx.serialization`
- Nuove funzioni:
  - `suspend fun saveAllLists(lists: Map<String, List<String>>)`
  - `suspend fun loadAllLists(): Map<String, List<String>>`

#### 🧠 ViewModel – `ShoppingListViewModel.kt`
- Stato reattivo:
  - `val shoppingLists = mutableStateOf<Map<String, List<String>>>(...)`
  - `val currentListName = mutableStateOf("Lista Principale")`
- Funzioni aggiuntive:
  - `createList`, `deleteList`, `renameList`, `switchToList`
  - `addItem`, `removeItem`, `saveAllLists`, `loadAllLists`

#### 🎨 UI – `ShoppingListScreen.kt`
- Selettore con `DropdownMenu` per lista attiva
- Pulsanti icona per:
  - ➕ Crea lista
  - ✏️ Rinomina lista
  - 🗑️ Elimina lista
- Dialog di input per nome lista (nuova/rename)
- Supporto `SwipeToDismiss` per rimuovere elementi

#### 🛠️ build.gradle.kts (modulo app)
- Aggiunta:
  ```kotlin
  implementation("org.jetbrains.kotlinx:kotlinx-serialization-json:1.5.1")
  implementation("androidx.compose.material:material-icons-extended:1.5.4")
  ```
- Abilitazione plugin:
  ```kotlin
  id("org.jetbrains.kotlin.plugin.serialization") version "2.2.0-RC"
  ```

---

### ✅ Risultato finale
- UI dinamica e funzionale, con supporto multi-lista completo
- Salvataggio persistente locale per ogni lista
- Tutti i componenti verificati e funzionanti su emulatore
- Nessun errore di compilazione