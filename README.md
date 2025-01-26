Week 2: Express.js Fundamentals Assignment

**Objective:**

- Apply Express.js concepts learned throughout the week.
- Practice building an Express.js server with routing, middleware, and error handling.

**Instructions:**

1. **Setup Express.js Project:**

   - Install Node.js using NVM and initialize an Express project.
   - Create a new project folder called `express-assignment`.
   - Run the following commands:
     ```sh
     mkdir express-assignment
     cd express-assignment
     npm init -y
     npm install express
     ```

2. **Project Structure:**

   - Organize your project files as follows:
     ```
     express-assignment/
     │-- routes/
     │    ├── userRoutes.js
     │    ├── productRoutes.js
     │-- middleware/
     │    ├── logger.js
     │-- index.js
     │-- package.json
     │-- README.md
     ```

3. **Implement Routing:**

   - Create `routes/userRoutes.js` with the following routes:
     ```js
     const express = require('express');
     const router = express.Router();

     router.get('/', (req, res) => res.send('User List'));
     router.get('/:id', (req, res) => res.send(`User ID: ${req.params.id}`));

     module.exports = router;
     ```
   - Create `routes/productRoutes.js` with the following routes:
     ```js
     const express = require('express');
     const router = express.Router();

     router.get('/', (req, res) => res.send('Product List'));
     router.post('/', (req, res) => res.send('Product Added'));

     module.exports = router;
     ```

4. **Implement Middleware:**

   - Create a middleware function in `middleware/logger.js` to log requests:
     ```js
     function logger(req, res, next) {
         console.log(`${req.method} ${req.url} at ${new Date().toISOString()}`);
         next();
     }
     module.exports = logger;
     ```

5. **Set Up the Express Server:**

   - In `index.js`, set up the Express app with routes and middleware:
     ```js
     const express = require('express');
     const app = express();
     const logger = require('./middleware/logger');
     const userRoutes = require('./routes/userRoutes');
     const productRoutes = require('./routes/productRoutes');

     app.use(logger);
     app.use('/users', userRoutes);
     app.use('/products', productRoutes);

     const PORT = process.env.PORT || 3000;
     app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
     ```

6. **Error Handling:**

   - Implement a global error handler at the end of `index.js`:
     ```js
     app.use((err, req, res, next) => {
         console.error(err.stack);
         res.status(500).send('Something went wrong!');
     });
     ```

7. **Testing:**

   - Run the server using:
     ```sh
     node index.js
     ```
   - Test the routes using Postman or your browser by visiting:
     - `http://localhost:3000/users`
     - `http://localhost:3000/products`

8. **Documentation:**

   - Add a `README.md` with instructions on how to run the project.

9. **Submission:**

   - Push your code to your GitHub repository.

**Evaluation Criteria:**

- Correct implementation of routes and middleware.
- Proper error handling.
- Project structure and code organization.
- Clear and concise documentation.
- Successful testing of endpoints.

