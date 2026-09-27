# React Shopping List / Store Inventory

This started as a to-do list for a Humber course project and turned into a small store inventory app. The back end is Node/Express with MongoDB, and the front end is React.

## What it does

**Back end (Express + MongoDB)**
- REST routes to list, add and update store items (each item has a name and a price)
- `/api/json` returns all the items as JSON, which the React app uses
- Register and login with Passport (local strategy). Passwords are hashed with bcrypt
- You have to be logged in to add an item
- Server-side pages are done with EJS (`views/` folder)

**Front end (React)**
- `FetchAPI.js` calls the back end and shows the inventory with prices
- `ItemIndexer.js` is a component where you add items and mark them completed. It uses `useState` and `useEffect`
- `useItemCounter.js` is a custom hook I wrote that counts how many items were added

## Run it locally

You need Node.js and MongoDB running locally on the default port (27017). The back end connects to `mongodb://127.0.0.1:27017/`.

**Back end** (runs on port 3000)
```
cd Backend/ItemIndexer
copy .env.example .env
npm install
node index.js
```
Put your own random value for `SECRET` in `.env`. It's used for the login sessions.

Then open http://localhost:3000

**Front end**
```
cd FrontEnd/client
npm install
npm start
```
The back end is already on port 3000, so React will ask to use another port. Type `y` and it opens on 3001.

## API routes

| Method | Route | What it does |
|---|---|---|
| GET | `/api/items` | Page with all items |
| GET | `/api/json` | All items as JSON |
| GET | `/api/items/add` | Add item form (login required) |
| POST | `/api/items` | Add an item |
| POST | `/api/items/update/:id` | Update an item |
| GET/POST | `/register` | Create an account |
| GET/POST | `/login` | Log in |

## Things I'd fix next

- There are two `POST /login` routes in `index.js`. Express only runs the first one, so the JWT code in the second one never runs. I'd remove it or merge them
- `POST /api/items` isn't behind the login check, only the form page is
- `ItemIndexer` isn't shown in `App.js` yet, only `FetchAPI` is
- Add a delete route and some tests