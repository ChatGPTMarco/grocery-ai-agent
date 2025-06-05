# GroceryApp – Project Development Log (Steps 1 to 7)

---

## ✅ Step 1: Installazione ambiente di sviluppo

- Installato Android Studio.
- Creato nuovo progetto: nome `GroceryApp`, linguaggio `Kotlin`, Minimum SDK: API 26.
- Verificata compilazione e avvio dell'app su emulatore Android.

---

## ✅ Step 2: Struttura architetturale del progetto

- Creati i seguenti package per supportare l'architettura MVVM:
  - `data`
  - `network`
  - `ui.shoppinglist`
  - `ui.recipes`
  - `utils`
  - `viewmodel`
- Verificata la corretta visualizzazione dei package nel modulo `app`.

---

## ✅ Step 3: Prima schermata (Shopping List)

- Creato file `ShoppingListScreen.kt` in `ui.shoppinglist`.
- Implementata UI con Jetpack Compose:
  - Titolo statico "Shopping List"
  - Lista fissa di 5 elementi
- Modificato `MainActivity.kt` per visualizzare `ShoppingListScreen`.
- Verificata corretta visualizzazione della UI su emulatore.

---

## ✅ Step 4: Gestione dinamica della lista con ViewModel

- Creato `ShoppingListViewModel.kt` in `viewmodel/`.
- Implementata lista osservabile (`mutableStateListOf`).
- Collegata la lista al Composable per aggiornarla in tempo reale.
- Aggiunto input utente con `OutlinedTextField` e pulsante "Add".
- Sincronizzazione UI automatica al variare della lista.
- Aggiunta dipendenza:  
  ```kotlin
  implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.6.1")
  ```

---

## ✅ Step 5: Persistenza locale con DataStore

- Creato `ShoppingListRepository.kt` in `data/`.
  - Utilizzo di `preferencesDataStore`
  - Salvataggio e lettura di `List<String>` come stringa CSV
- Import corretti configurati:
  ```kotlin
  implementation("androidx.datastore:datastore-preferences:1.0.0")
  implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3")
  ```
- Rispettato lo style Kotlin (nominativi conformi)
- File verificato senza errori di compilazione
- Pronto per l’integrazione nel ViewModel

---

## ✅ Step 6: Collegamento ViewModel <-> Repository per persistenza effettiva

- Completata l’integrazione tra `ShoppingListViewModel` e `ShoppingListRepository`.
- Il `ViewModel` utilizza coroutine e `viewModelScope` per caricare e salvare la lista della spesa in modo asincrono.
- Aggiunta funzione `loadShoppingList()` nel blocco `init` del ViewModel per caricare i dati salvati all’avvio.
- Aggiunta funzione `saveShoppingList()` chiamata automaticamente ogni volta che si aggiunge o rimuove un elemento.
- Nel `Repository`, implementato salvataggio persistente tramite `DataStore` utilizzando una stringa CSV per serializzare `List<String>`.
- Corretto il `package` e gli `import` nei file Kotlin per garantire la corretta visibilità tra classi.
- La UI (`ShoppingListScreen.kt`) è ora collegata al ViewModel tramite:
  - `viewModel()` per istanziare il ViewModel
  - Osservazione diretta di `shoppingItems`
  - Chiamata a `addItem()` e `removeItem()` da parte dell’interfaccia utente
- Verificato corretto funzionamento della persistenza:
  - Aggiunto elemento alla lista
  - Chiusura completa dell’app
  - Alla riapertura, l’elemento è stato correttamente ricaricato dal salvataggio locale

📌 Sistema ora supporta il **caricamento automatico e salvataggio persistente della lista della spesa**, rendendo la funzionalità completa e pronta per futuri miglioramenti (es. sincronizzazione cloud o notifiche).

---

## ✅ Step 7: Swipe to Delete – Rimozione elementi con gesture

- Obiettivo: migliorare l’esperienza utente permettendo la rimozione di elementi con swipe laterale.
- Sostituita la lista `Column` con una `LazyColumn` usando `SwipeToDismiss`.
- Implementato `rememberDismissState` per rilevare lo stato dello swipe.
- Collegata la gesture alla funzione `viewModel.removeItem(index)`.
- Visualizzazione del messaggio "Eliminato" **solo durante lo swipe attivo**, evitando la persistenza del testo dopo la rimozione.
- Verificata la rimozione degli elementi anche dal salvataggio persistente tramite DataStore.
- Confermata corretta compatibilità con Jetpack Compose **Material 2**, migrando:
  - Il tema (`Theme.kt`) da Material3 a Material2
  - La tipografia (`Type.kt`) con `Typography` e `TextStyle` appropriati
  - I colori (`Color.kt`) definiti in modo compatibile
- Verificata corretta compilazione, assenza di errori, e mantenimento della coerenza visiva.

📌 L’interazione touch è ora **moderna e coerente con le linee guida Material Design**, rendendo l’app più intuitiva per l’utente finale.
