# Guida Pratica a Vue.js 3 per Principianti (TypeScript e Angular)

## Introduzione a Vue.js – Cos'è e perché usarlo

**Vue.js** è un framework JavaScript *progressivo* per costruire interfacce utente reattive.  
"Progressivo" significa che può essere adottato in modo incrementale: si può iniziare integrandolo in una singola parte di un’applicazione esistente, oppure usarlo per creare Single-Page Application (SPA) complete[^1].

Vue si concentra principalmente sul layer visivo (*View*): offre un sistema di **data binding reattivo** e un’architettura basata su **componenti**, semplificando lo sviluppo front-end[^2].

Grazie alla curva di apprendimento dolce e alla flessibilità, Vue è adatto sia a **piccoli progetti prototipali** sia ad **applicazioni complesse** (grazie a strumenti opzionali come **Vue Router** per il routing e **Pinia** – il successore di Vuex – per la gestione dello stato globale)[^2].

---

### Perché usare Vue.js? Ecco alcuni vantaggi chiave

- **Sintassi dichiarativa e template leggibili**: Vue utilizza template HTML arricchiti da **direttive** (come `v-if`, `v-for`) che legano i dati al DOM in modo dichiarativo.  
  Descriviamo il *cosa* deve apparire in funzione dei dati, e Vue si occupa di aggiornare il DOM in modo efficiente quando i dati cambiano[^3][^4].

- **Reattività automatica**: Vue tiene traccia delle dipendenze tra dati e interfaccia: quando modifichi uno stato reattivo, l’interfaccia si aggiorna automaticamente, senza dover manipolare manualmente il DOM.  
  Questo è ottenuto tramite un **Virtual DOM** efficiente e un **sistema reattivo** basato su `Proxy` JavaScript[^5].

- **Peso leggero e prestazioni**: Il core di Vue è relativamente piccolo e ottimizzato.  
  Le applicazioni Vue tendono ad avere tempi di caricamento rapidi e ottime prestazioni runtime grazie al Virtual DOM e agli aggiornamenti granulari.  
  Vue 3 in particolare ha migliorato ulteriormente le performance e la dimensione del bundle rispetto a framework più pesanti[^6][^7].

- **Flessibilità e integrazione graduale**:  
  Puoi utilizzare Vue per un semplice widget in una pagina esistente, oppure creare un’app completa.  
  Non richiede una struttura di progetto rigida: puoi integrarlo facilmente anche in progetti *legacy*, introducendo componenti Vue dove serve senza riscrivere tutto da zero[^8].

- **Comunità e ecosistema**:  
  Vue ha una comunità ampia e attiva.  
  Offre una suite di strumenti ufficiali: ad esempio **Vue Router** per il routing client-side, **Pinia** per lo state management globale (sostituisce Vuex in Vue 3), **Vue CLI** (ora `create-vue`) per il scaffolding (anche se oggi si preferisce **Vite**), e ottime integrazioni con TypeScript.  
  La comunità fornisce inoltre molte librerie UI (**Vuetify**, **Element Plus**, ecc.) e risorse di apprendimento.

---

### In sintesi

Vue.js è apprezzato perché **leggero**, **facile da apprendere** e **potente**.

È ideale se vuoi un framework che unisca la **semplicità di approccio** (poche barriere d’ingresso) a funzionalità sufficienti per costruire applicazioni avanzate.

La sua **filosofia progressiva** e la **reattività automatica** aiutano a scrivere codice **pulito** e **manutentibile**, concentrandosi più sulla logica dell’applicazione che sulla manipolazione del DOM.

---

[^1]: Documentazione ufficiale Vue – Introduzione
[^2]: Vue.js Docs – Component System
[^3]: Vue Template Syntax
[^4]: Vue Guide – Declarative Rendering
[^5]: Vue Reactivity Core
[^6]: Vue 3 Performance Improvements
[^7]: Bundle size comparison – Vue vs Others
[^8]: Vue Integration Strategies

# Configurare un progetto Vue 3 moderno con Vite (e VS Code)

Per iniziare a sviluppare con **Vue 3**, configureremo un nuovo progetto utilizzando **Vite** come *build tool*.  
Vite è scelto per la sua **velocità** e **semplicità** nell'ambiente di sviluppo (HMR rapidissimo) e perché è ormai l’impostazione predefinita per i nuovi progetti Vue.

### Prerequisiti

Assicurati di avere:

- **Node.js** aggiornato (versione **18+** consigliata) installato sul tuo sistema[^17]
- Una connessione internet per scaricare le dipendenze
- **Visual Studio Code (VS Code)** come editor
- L’estensione ufficiale **Vue Language Features (Volar)** per un miglior supporto ai file `.vue` (SFC) e a TypeScript[^13]

---

## 1. Creazione del progetto

Apri il terminale nella directory in cui vuoi creare il progetto e lancia il comando di scaffolding ufficiale:

```bash
npm create vue@latest
```

Questo comando utilizza create-vue, il tool di scaffolding ufficiale di Vue, che a sua volta imposterà un progetto basato su Vite.

Dopo qualche secondo, verranno presentati una serie di prompt interattivi dove potrai scegliere le opzioni per il tuo progetto. Ad esempio:

- Project name: inserisci il nome della cartella/progetto.
- **Add TypeScript?** → seleziona **Yes** (vogliamo usare TypeScript).
- **Add JSX Support?** → puoi mettere **No**, non ci serve JSX per ora.
- **Add Vue Router for SPA development?** → seleziona **Yes** (includerà la configurazione base di Vue - Router).
- **Add Pinia for state management?** → seleziona **Yes** (includerà Pinia come store globale).

- **Altre opzioni:** Testing, ESLint, Prettier, ecc. – puoi scegliere Yes per ESLint/Prettier per avere subito linting e formattazione, oppure aggiungerli in seguito.
Per il nostro scopo didattico, non approfondiremo Testing e E2E, puoi mettere No a quelle per semplicità.

### Esempio di configurazione (prompt in inglese)

>✔ Project name: … vue3-todo-app
>✔ Add TypeScript? … Yes
>✔ Add JSX Support? … No
>✔ Add Vue Router for Single Page Application development? … Yes
>✔ Add Pinia for state management? … Yes
>✔ Add Vitest for Unit testing? … No
>✔ Add an End-to-End Testing Solution? … No
>✔ Add ESLint for code quality? … Yes
>✔ Add Prettier for code formatting? … Yes
>✔ Add Vue DevTools 7 extension for debugging? … No
---
> *(Le opzioni potrebbero variare in base alle versioni, ma in generale scegli **Vue 3 + TypeScript + Router + Pinia** e strumenti di qualità del codice come **ESLint**)[^12].*

Una volta confermate le scelte, `create-vue` genererà la struttura del progetto nella cartella indicata e installerà le dipendenze di base.  
Al termine dovresti vedere un messaggio di completamento("Done")

## 2. Installazione dipendenze e avvio server di sviluppo

Spostati nella directory del progetto e installa i pacchetti (se non sono già installati automaticamente):

```bash
cd vue3-todo-app
npm install
```

Ora puoi avviare il server di sviluppo locale:

```bash
npm run dev
```

Vite avvierà un server (tipicamente su <http://localhost:5173/> o una porta simile, indicata in console) con l’app Vue di esempio in esecuzione.

Apri il link nel browser: dovresti vedere la pagina di benvenuto di Vue 3, con il logo di Vue e alcuni link (in inglese) alla documentazione.

Se vedi questo, la configurazione di base è riuscita!

## 3. Aprire il progetto in VS Code

Avvia VS Code nella cartella del progetto:

- Con terminale (se hai code nella PATH):

```bash
code .
```

Oppure da interfaccia grafica: File > Open Folder in VS Code.

#### Estensione consigliata: Vue Language Features (Volar)

Installando l’estensione Vue Language Features (Volar)1 ottieni:

- Highlight sintattico per i file .vue
- Auto-completamento per i componenti
- Suggerimenti sui tipi TypeScript
- Integrazione con ESLint/Prettier (se attivati)

Questa estensione è fondamentale per la produttività con Vue 3 (ha sostituito la vecchia Vetur).

In VS Code, se apri ad esempio il file:

```bash
src/components/HelloWorld.vue
```

## 4. Struttura iniziale del progetto

Diamo un’occhiata a cosa è stato creato:

### `src/`

Contiene il **codice sorgente dell’app**. Al suo interno troviamo:

- **`main.ts`**:  
  Il punto di ingresso dell’applicazione.  
  Qui Vue **crea l’app** e la **monta nel DOM**. Vedremo a breve il suo contenuto.

- **`App.vue`**:  
  Il **componente radice** dell’app (root component).  
  Rappresenta l’intera applicazione ed è montato da `main.ts` sul DOM.

- **`components/`**:  
  Contiene **componenti riutilizzabili**. Inizialmente include:
  - `HelloWorld.vue`: un componente di esempio.
  - Possibili altre risorse, come un logo o altri componenti base.

### `router/` (opzionale)

Se hai incluso **Vue Router**, sarà presente questa cartella, contenente:

- **`index.ts`**:  
  Definisce le **rotte** e configura il router per la SPA.

### `stores/` o `store/` (opzionale)

Se hai incluso **Pinia**, potresti trovare questa cartella, con:

- Un file di esempio (`index.ts`, `counter.ts`, ecc.), spesso vuoto o con uno **store di esempio**.

### Configurazioni ESLint/Prettier (opzionali)

Se hai scelto **ESLint** e/o **Prettier**, saranno inclusi:

- `.eslintrc.cjs`  
- `.prettierrc`  
- Altri file e **script npm correlati** per il linting e la formattazione.

### Altri file di configurazione

- **`vite.config.ts`**:  
    File di configurazione per **Vite**.  
    Generalmente non serve modificarlo per iniziare.  
    Contiene già:
  - L’**alias `@`** per `src/`
  - I **plugin per Vue**

- **`tsconfig.json`**:  
  Configurazione per **TypeScript**.

- **`package.json`**:  
  Elenco delle **dipendenze**, degli **script npm**, e altre informazioni di progetto.

## 5. Esecuzione e Hot-Reload

Modifica, ad esempio, il **messaggio di benvenuto** in `App.vue` o `HelloWorld.vue` e salva il file.  
**Vite** applicherà automaticamente l’**Hot Module Replacement (HMR)**, ricaricando la pagina nel browser **senza perdere lo stato**.

> 🔁 Questo ciclo di feedback rapido è uno dei motivi per cui **Vite è molto piacevole da usare** rispetto a strumenti più vecchi.

---

Siamo ora pronti per **esplorare l’architettura di base di un’app Vue** e iniziare a sviluppare **componenti personalizzati**.

---

### 💡 Consiglio

Se incontri **difficoltà durante la creazione del progetto**, verifica che **Node.js sia aggiornato**.

In alternativa, puoi provare un ambiente online come:

- [StackBlitz](https://stackblitz.com)
- [Vitest](https://vitest.dev)
- Oppure visita 👉 [`vite.new/vue`](https://vite.new/vue)

> Questo link crea un progetto Vue 3 di base direttamente nel browser[^20].  
> Ma per lavorare su un **progetto reale**, l’ambiente **locale** resta la scelta migliore.

---

[^20]: vite.new/vue – Crea un template Vue 3 di base nel browser

## Struttura di base di un'app Vue e Single File Components

Una applicazione Vue è essenzialmente composta da componenti. In Vue 3, ogni
componente (inclusa l'app principale) è tipicamente definito come Single File
Component (SFC) in un file .vue. Un SFC contiene tre sezioni principali: - <template> –
blocco che contiene il markup HTML (con binding dinamici). - <script> – blocco
JavaScript/TypeScript con la logica del componente. - <style> – blocco CSS/SCSS per i
stili locali al componente (opzionalmente con attributo scoped per confinare i CSS al
componente).

Vediamo la struttura del file main.ts generato nel progetto (che inizializza l'app):
