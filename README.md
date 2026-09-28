# Step-by-Step Introduction to the Angular Framework

📖 **Read the tutorial: [https://stahe.github.io/en-angular-etape-par-etape-sept-2026/](https://stahe.github.io/en-angular-etape-par-etape-sept-2026/)**

This course teaches you how to build a web application using the [Angular](https://angular.dev) 22 framework: a **single-page application** (SPA), whose pages are rendered **in the browser** using JSON data from a server.

It follows up on the course [Step-by-Step Introduction to the NestJS Web Framework](https://stahe.github.io/en-nestjs-html-sept-2026/), offering a different perspective, and follows the structure of the [Step-by-Step Introduction to the Vue.js Framework](https://stahe.github.io/vuejs-etape-par-etape-sept-2026/): same server, same pages, written in the Angular style.

| NestJS Course | Angular Course |
|---|---|
| the server generates the HTML pages (Handlebars) | the browser generates the pages (Angular) |
| the browser displays what it receives | the server returns only JSON |
| controllers, views, `res.render` | components, router, services |
| guards `JwtAuthGuard`, `RolesGuard` | router guards (the server maintains its own) |
| dictionaries read by the server | dictionaries on the client (ngx-translate); the server returns only keys |
| flash message in a cookie | flash message in a signal service |

The pages, however, remain unchanged: they are the same ones from the **RdvMedecins** application already presented with the other frameworks.

## The Approach: Many Short Examples, Then a Case Study

Since Angular is more feature-rich than Vue.js, the course is structured around **25 short examples**, each focused on a single concept. They form a single Angular workspace: a single `npm install` command, followed by `npm start <example>` to run one.

| Chapter | Content | Examples |
|---|---|---|
| Getting Started | an Angular workspace, signals (`signal`, `computed`, `effect`, `linkedSignal`), templates (`@if`, `@for`, `@let`), events, `ngModel`, signal-driven forms, validation, reactive forms, pipes | 01–09 |
| Components | `input()`, `output()`, `model()`, content projection, lifecycle, services and dependency injection, directives, confirmation dialog | 10–16 |
| Routing | the router, parameters, query, lazy loading, navigation guards | 17–18 |
| Observables and Shared State | RxJS (`debounceTime`, `switchMap`, `toSignal`), signal services, `localStorage` | 19–20 |
| Internationalization | ngx-translate: parameters, plurals, dates, amounts | 21 |
| The Server: A Black Box | JSON server installation, its API, 48 `curl` examples | – |
| Communicating with the Server | `HttpClient`, `ng serve` proxy, `httpOnly` cookie, interceptor, API access layer, `httpResource`, server errors attached to fields | 22–25 |

Each example is presented with its complete code, commented line by line, and a screenshot of its execution.

## The Server: A Black Box

The server is the NestJS server from the previous lesson, whose controllers return **JSON**—the same as for the Vue.js client. This lesson treats it as a **black box**: we install it, study its API, and query it with `curl`—but we don’t need to read its code (which is provided and commented for the curious).

- All errors have the same format: `{ "statusCode": 409, "cle": "ERRORS. LOGIN_TAKEN", "params": {...}, "champs": {...} }` — translation **keys**, never actual text;
- authentication via a JWT token in an `httpOnly` / `sameSite=strict` cookie: the client-side JavaScript never sees the token;
- CSRF protection: `sameSite` cookie, and all POST requests must be in JSON;
- A “test mode” for the CAPTCHA to allow querying the API with `curl`.


## The Case Study: The RdvMedecins Angular Client

A complete application for **booking appointments at a medical practice**, with **all** files (about 50) listed and commented.

- **Modern Angular**: standalone components, signals, change detection without zone.js, signal-based forms with custom controls (`FormValueControl`), pages loaded on demand.
- **Three roles**: `ADMIN` (manages doctors and clients), `DOCTOR` (schedules and cancels appointments), `USER` (the patient: books appointments for themselves, manages their account).
- **Privacy**: A patient never receives the names of other patients—the server does not send them.
- **Full page state in the URL**: `/agenda?idMedecin=1&jour=2026-10-05&reserver=7` reopens the booking window after pressing F5; the Previous/Next buttons work.
- **Server-side validation**: Forms display errors returned by the API below each field; optimistic locking, duplicate names, login already taken, etc.
- **Session**: Restored after pressing F5 (`GET /api/auth/moi`); expiration managed in a single location (an HTTP interceptor, 401 response).
- **French / English**, translated tab titles, keyboard-accessible confirmation window, Bootstrap 5.
- **Deployment**: the compiled client is served by the JSON server itself (same origin, no CORS).

## Technologies

Angular 22.2 (standalone components, signals, signal-driven forms, zoneless) · TypeScript 6.0 · Angular CLI · RxJS 7.8 · ngx-translate 18 · Bootstrap 5.3 · server-side: NestJS 10 · TypeORM · MySQL 8 / MariaDB · Passport JWT · svg-captcha

## Prerequisites

- A basic understanding of JavaScript (or TypeScript), HTML, and the HTTP protocol.
- Node.js 24 (or at least 22.22.3), Visual Studio Code with the Angular Language Service extension, and a MySQL server (e.g., Laragon on Windows) for the JSON server. Installation instructions are provided in the course appendices.

## Author

This course, its examples, the JSON server, and the case study were written by **Claude**, the AI from [Anthropic](https://www.anthropic.com) (September 2026) at the request of **Serge Tahé**
