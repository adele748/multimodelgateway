# Specifiche Tecniche - MultiModel Gateway

## Architettura iniziale MVP

### Frontend (Browser Client)
- **Framework**: React.js 18+
- **UI Library**: Tailwind CSS 3.0+
- **State Management**: Zustand 4.0+
- **API Client**: Axios
- **Comunicazione Real-Time**: Socket.io
- **Bundler**: Vite
- **Testing**: Jest + React Testing Library
- **Linting/Formatting**: ESLint + Prettier

### Backend
- **Runtime**: Node.js 18+ LTS
- **Framework**: Express.js 4
- **Database**: SQLite (sviluppo), PostgreSQL (produzione)
- **ORM**: Prisma
- **Autenticazione**: JWT + bcrypt
- **Logging**: Winston/Pino
- **Testing**: Jest/Mocha
- **MCP Integration**: SDK ufficiale TypeScript (modelcontextprotocol/typescript-sdk)

### DevOps & Infrastruttura
- **Containerization**: Docker
- **CI/CD**: GitHub Actions
- **Hosting iniziale**: Vercel (frontend), Railway/Render (backend)
- **Monitoraggio**: Sentry per error tracking

## Integrazioni API

### Modelli AI supportati inizialmente
1. **Claude (Anthropic)**
   - API: Claude API v1
   - Modelli: Claude 3 Opus, Claude 3 Sonnet, Claude 3 Haiku
   - Autenticazione: API Key

2. **GPT (OpenAI)**
   - API: Chat Completions API
   - Modelli: GPT-4o, GPT-3.5 Turbo
   - Autenticazione: API Key

### Implementazione MCP
- Utilizzo dell'SDK ufficiale TypeScript
- Implementazione iniziale delle funzionalità core:
  - `initialize`: Stabilire connessione
  - `resources/read`: Lettura risorse
  - `tools/call`: Chiamata strumenti
  - Gestione notifiche base

## Struttura dati

### Modelli DB principali
1. **User**
   - id, email, passwordHash, createdAt, settings

2. **ApiKey**
   - id, userId, provider, key (encrypted), label, createdAt

3. **Conversation**
   - id, userId, title, modelId, createdAt, updatedAt, settings

4. **Message**
   - id, conversationId, role, content, createdAt, metadata

5. **Resource**
   - id, userId, type, name, uri, metadata, createdAt

### Schema API REST principali
- `POST /api/auth/login`
- `POST /api/auth/register`
- `GET /api/conversations`
- `POST /api/conversations`
- `GET /api/conversations/:id/messages`
- `POST /api/chat/completions`
- `GET /api/models`
- `GET /api/resources`
- `POST /api/resources`

### Endpoints WebSocket
- `/ws/chat` - Per streaming risposte in tempo reale
- `/ws/notifications` - Per notifiche dal sistema

## Requisiti funzionali MVP

### Autenticazione & Utenti
- Registrazione e login utenti
- Gestione profilo base
- Salvataggio sicuro delle chiavi API

### Chat Interface
- Visualizzazione messaggi thread-based
- Supporto markdown nei messaggi
- Indicatori di caricamento durante le risposte
- Copia/esportazione conversazioni
- Interruzione generazione risposte

### Gestione modelli
- Selezione modello per conversazione
- Configurazione parametri generazione (temperatura, token max)
- Visualizzazione modelli disponibili in base a chiavi configurate

### MCP Implementazione base
- Connessione file system locale (sandbox)
- Lettura documenti base (testo, markdown, PDF)
- Supporto strumenti semplici (calcolatrice, ricerca web)

### Gestione risorse
- Upload file base
- Visualizzazione documenti
- Riferimenti a file nelle conversazioni

## Requisiti non funzionali

### Performance
- Tempo risposta API <300ms (escluso tempo modello AI)
- Caricamento iniziale app <2s
- Ottimizzazione bundle frontend (<500KB iniziale)

### Sicurezza
- Crittografia dati sensibili (chiavi API)
- Sanitizzazione input
- Rate limiting
- Validazione richieste
- Nessuna esposizione di informazioni sensibili nei log

### Scalabilità
- Architettura che faciliti future espansioni
- Componenti modulari con accoppiamento ridotto
- Pattern consistenti per aggiungere nuovi provider AI

### Accessibilità
- Conformità WCAG 2.1 livello AA
- Supporto tema chiaro/scuro
- Navigazione tramite tastiera
- Compatibilità screen reader

## Browser support
- Chrome/Edge (ultime 2 versioni)
- Firefox (ultime 2 versioni)
- Safari (ultime 2 versioni)
- Mobile browsers responsive design

## Considerazioni future
- Preparazione per eventuale migrazione a Electron/Tauri
- Struttura abilitante per PWA
- Design system scalabile per facilitare espansione UI
- Hooks per plugin di terze parti