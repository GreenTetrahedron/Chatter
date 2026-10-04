# Chatter

A web LLM chat application powered by Cloudflare. It is available [here](https://chatter-di8.pages.dev/)


## Flow Design

```
Pages (Frontend)
        ↓
Workers (Routes to appropriate Durable Object)
        ↓
Durable Objects (Stores conversation history per conversation)
        ↓
Workers AI (calls LLM)
```


## Configuration for Testing and Deployment

### Configuring the Angular Frontend

The frontend communicates with the Worker via the `apiUrl` environment variable.

**Development**: Edit `src/environments/environment.development.ts`

   ```ts
   export const environment = {
     apiUrl: '<dev-worker-url>'
   };
   ```

**Production**: Edit `src/environments/environment.ts`

   ```ts
   export const environment = {
     apiUrl: '<prod-worker-url>'
   };
   ```

### Building the Angular Frontend

   * Development build (uses `environment.development.ts`):

     ```bash
     ng build --configuration development
     ```
   * Production build (uses `environment.ts`):

     ```bash
     ng build
     ```


### Configuring the Worker

The table below details the environment variables required by the worker and explains each of their purposes.

| Environment Variable | Purpose | Example Expected Value |
| -- | -- | -- |
| `PAGE_URL` | Specifies the URL where the frontend is hosted on | https://chatter-di8.pages.dev/ |
| `MODEL` | Specifies the Cloudflare AI Model ID to use | @cf/meta/llama-3.1-8b-instruct-fp8 |

## Potential improvements

* Voice chat input
* Ability to delete chats
* Ability to change expiration date of conversations
* Ability to copy conversation transcript
* Ability to change system prompt
* Ability to choose the LLM used
