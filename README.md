# GargiHawaldar_Backend
# Tic-Tac-Toe Backend

## **Introduction**
This backend project implements a functional Tic-Tac-Toe game using Node.js. It includes user authentication, game logic, and APIs to manage user registration, login, gameplay, and match history. The project uses an in-memory MongoDB instance for data persistence.

---

## **Features**
1. **User Registration and Authentication**
   - Users can register with a username and password.
   - Token-based authentication using JWT for secure access.

2. **Tic-Tac-Toe Gameplay**
   - Two authenticated users can play a game.
   - Tracks player turns and validates moves.
   - Determines the game result: win, draw, or ongoing.

3. **Match History**
   - Stores all games played by users.
   - API to fetch match history, including:
     - Opponent details.
     - Final game result (win/loss/draw).
     - Timeline of moves made during the match.

4. **Profile Management**
   - Users can update their profile details.

---

## **Approach and Design**

### **1. Authentication**
- **Registration**: A new user record is created in the database after validating the input.
- **Login**: Users log in using their credentials. Upon successful authentication, a JWT token is generated and returned.
- **Token-Based Authorization**: Middleware is used to validate the JWT for secure access to protected routes.

### **2. Gameplay**
- **Game Initialization**: A game can only start if two authenticated users are involved.
- **Turn-Based Logic**: Alternates between player moves, ensuring the rules of Tic-Tac-Toe are followed.
- **Winner Declaration**: The backend evaluates the board after each move to determine a winner, a draw, or whether the game should continue.
- **Move Validation**: Prevents invalid moves, such as overwriting a cell or playing out of turn.

### **3. Match History**
- Each game stores the following:
  - Players' IDs.
  - Timeline of moves.
  - Final result (win/loss/draw).
- Users can retrieve their match history with details about opponents and moves.

### **4. Database Design**
- **Collections:**
  - `users`: Stores user credentials and profile data.
  - `games`: Stores game states, including moves, players, and results.

### **5. Error Handling**
- Comprehensive validation for user inputs and gameplay actions.
- Meaningful error messages for invalid operations (e.g., unauthorized access, invalid moves).

---

## **Endpoints**

### **Authentication**
- **POST /api/auth/register**: Register a new user.
- **POST /api/auth/login**: Authenticate and obtain a token.

### **Gameplay**
- **POST /api/game/start**: Start a new game between two users.
- **POST /api/game/:gameId/move**: Make a move in an ongoing game.

### **Match History**
- **GET /api/game/history**: Fetch a user's match history.

### **Profile Management**
- **PUT /api/users/profile**: Update user profile details.

---

## **Assumptions**
1. A game involves exactly two players.
2. Only authenticated users can start or play a game.
3. The board size is fixed to 3x3 for standard Tic-Tac-Toe rules.
4. JWT tokens are valid for 1 hour.
5. Moves are indexed from `0` to `8` representing the 3x3 grid.

---

## **Setup and Installation**

### **Prerequisites**
- Node.js installed.
- Postman (for API testing).

### **Steps**
1. Clone the repository:
   ```bash
   git clone <repository_url>
   cd tictactoe-backend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the server:
   ```bash
   node server.js
   ```
4. The server will run on `http://localhost:5000`.

### **Testing**
- Use Postman to test the endpoints as described in the provided examples.
- Run `npm test` (if unit tests are implemented).

---

## **Libraries Used**
1. **Express.js**: For creating REST APIs.
2. **JWT**: For authentication.
3. **Mongoose**: To interact with the MongoDB database.
4. **Bcrypt.js**: For password hashing.
5. **In-Memory MongoDB**: For lightweight, local testing of the database.
