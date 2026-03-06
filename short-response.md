# Short Response Questions

Answer each question below in your own words. Aim for 3–5 sentences per answer. Be specific — use the exact terms and concepts from the lesson.

Your responses will each be evaluated out of 6 points. You can earn 3 points for writing quality and 3 points for the accuracy and precision of the technical content per question.

---

## Question 1: Express vs `node:http`

Express is described as a framework that "wraps" `node:http`. What does that mean? Compare how you would handle a `GET /api/users` request in `node:http` versus in Express. What does Express do for you automatically that you had to write manually with `node:http`?

**Your answer here**:

--- Express is built on top of `node:http,` meaning it uses it under the hood but adds convenience abstractions. In raw node:http, you get a single callback for every request and have to manually check req.method and req.url, call JSON.stringify(), set headers, and call res.end(). Express replaces all of that with dedicated route handlers like app.get('/api/users', ...), a res.json() method that handles serialization and headers automatically, and req.params/req.query for parsed URL data. It also adds the middleware system via app.use(), which node:http has no equivalent for. Essentially, Express just removes the boilerplate so you can focus on application logic instead of HTTP plumbing.

## Question 2: Endpoints, Controllers, and Middleware

What are **controllers** and **middleware** in Express? What are each responsible for and how do they work together to handle incoming requests?

**Your answer here**:

--- Middleware are functions that run before your route logic and handle things like authentication, logging, and body parsing. They either pass the request along via next() or short-circuit with a response. Controllers are where your actual business logic lives for a specific route, reading from the request, doing whatever work is needed, and sending back the response. Together, a request flows through middleware first (which can guard or transform it), then lands in the controller to be fulfilled.

## Question 3: Query Strings and Route Parameters

How are **query strings** and **route parameters** similar? How are they different? In your answer, provide an example of when you would use each.

**Your answer here**:

---Both are ways of passing data to the server through the URL, and both are automatically parsed by Express — into req.params and req.query respectively.
The difference is purpose. Route parameters are baked into the URL path and identify a specific resource. Query strings come after the ? and are used to filter or modify results.

example : ```js const id = Number(req.params.id); ```

## Question 4: Same-Origin Requests

For API fetch calls from a client-side application, explain the difference between fetching from endpoints with relative paths like `/api/quotes` and fetching from endpoints with a full URL like `https://dog.ceo/api/breeds/image/random`. Why do we not send a fetch using a url like `http://localhost:8080/api/quotes`?

**Your answer here**: 

--- A relative path like `/api/quotes` automatically sends the request to whatever server served the page. It works on localhost and in production without any changes. Hardcoding http://localhost:8080/api/quotes breaks in production because localhost refers to the user's own machine, not your deployed server like. Full URLs like https://dog.ceo/... are fine because they're always pointing to the same external server regardless of environment.