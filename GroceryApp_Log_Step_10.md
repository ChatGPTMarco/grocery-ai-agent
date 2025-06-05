# GroceryApp – Registro aggiornato fino allo Step 10

## ✅ Stato Attuale del Progetto
- **Nome progetto**: GroceryApp
- **Tecnologia principale**: Android (Kotlin, Jetpack Compose)
- **Persistenza locale**: DataStore + kotlinx.serialization
- **Funzionalità completate**:
  - Gestione multi-lista della spesa con supporto Aggiungi/Rinomina/Elimina/Ordina
  - UI responsive con SwipeToDismiss
  - Persistenza lista della spesa
  - Navigazione a schede (BottomNavigation): Lista & Ricette
  - Gestione ricette con persistenza e aggiunta/rimozione

---

## ✅ File implementati e aggiornati

### 1. **ShoppingListViewModel.kt**
Percorso: `viewmodel/`
- Gestisce più liste della spesa
- Funzioni: aggiungi, rimuovi, rinomina, elimina, ordina A-Z/Z-A
- Dati persistiti con DataStore

### 2. **ShoppingListScreen.kt**
Percorso: `ui/shoppinglist/`
- UI composable per la lista della spesa
- Interfaccia con `ShoppingListViewModel`
- Dialog per nuova lista e rinomina
- Icone per sorting A-Z e Z-A

### 3. **MainActivity.kt**
Percorso: `root/`
- Configura la UI e la navigazione
- BottomNavigation con due schermate:
  - Lista (Icona: `List`)
  - Ricette (Icona: `Book`)

### 4. **Recipe.kt**
Percorso: `data/`
- Modello dati per ricette
- Serializzabile con kotlinx.serialization

### 5. **RecipesRepository.kt**
Percorso: `data/`
- Gestisce salvataggio/caricamento delle ricette
- Usa DataStore con chiave `recipes_json`

### 6. **RecipesViewModel.kt**
Percorso: `viewmodel/`
- Espone lista osservabile di ricette
- Supporta `addRecipe()` e `deleteRecipe()` con persistenza

### 7. **RecipesScreen.kt**
Percorso: `ui/recipes/`
- UI composable per la gestione ricette
- Mostra nome e ingredienti
- Permette aggiunta ed eliminazione tramite `AlertDialog`
- Collegata a `RecipesViewModel`

---

## 📦 Dipendenze confermate nel `build.gradle.kts`
- `kotlinx.serialization-json`
- `androidx.datastore:datastore-preferences`
- `androidx.lifecycle:lifecycle-viewmodel-compose`
- `androidx.compose.material` + Icone estese
- `kotlinx.coroutines`

---

## 🔄 Prossimo Step
**Step 11**: Importare ingredienti di una ricetta direttamente nella lista della spesa.

Richiederà:
- Aggiunta funzione in `RecipesScreen` per selezionare una ricetta
- Invio ingredienti a `ShoppingListViewModel`
- Probabile aggiunta di conferma tramite `Dialog`

---

## 📝 Note Finali
- Il codice è pulito, conforme alle pratiche Jetpack Compose.
- Modularità ottimale per estensioni future.
- Tutte le ViewModel operano con DataStore asincrono e reattivo.

Prossimo passo quando desiderato: implementazione Step 11.