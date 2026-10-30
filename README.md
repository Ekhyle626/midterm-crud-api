1. Most Challenging Parts
Async Error Handling: Managing asynchronous promise flows and returning consistent, structured JSON error responses without crashing the application.

Input Validation: Safely parsing URL route parameters and enforcing data constraints (such as email uniqueness) across create and update endpoints.

2. TypeORM vs. Raw SQL
TypeScript Entities: Maps database tables directly to classes and uses convenient repository methods (find, save) instead of writing manual SQL strings.

Type Safety & Auto-complete: Provides strong typing across queries and relations, drastically reducing runtime errors and typos in table or column names.

3. Excluding Passwords & Implementation
Why: Protects sensitive user credentials from leaking in API responses, network logs, or client-side storage.

Implementation:

Add { select: false } to the entity password column definition.

Use object destructuring in the controller to strip the password before returning the response object:const { password: _, ...userWithoutPassword } = savedUser;

4. When to Use Database Transactions
Scenario: E-commerce checkout (creating an order, deducting stock, and debiting the account balance).

Why: Guarantees atomicity. If any single step fails, all previous operations roll back entirely, preventing corrupted or inconsistent database states.

5. synchronize: true vs. Migrations
synchronize: true: Automatically updates the database schema every time the application starts. Use only in development.

Migrations: Version-controlled SQL scripts for manual, controlled schema changes. Use in production to prevent accidental data loss.

6. Adding a Relationship (One-to-Many Example)
Child Entity (e.g., Comment/Product): Define fields and add @ManyToOne(() => Parent, (parent) => parent.children).

Parent Entity (e.g., Task/User): Add @OneToMany(() => Child, (child) => child.parent) children!: Child[];.

Configuration: Register both entities inside the entities array in your data-source.ts file.

7. Security Improvements for Production
Password Hashing: Hash passwords using secure algorithms like bcrypt or argon2 before saving them to the database.

Auth & Rate Limiting: Protect sensitive endpoints using JWT/cookies and use express-rate-limit to prevent brute-force attacks.

Environment Configuration: Set NODE_ENV=production, turn off synchronize, restrict CORS origins, and use security headers middleware (such as helmet).

8. The ! (Definite Assignment Operator)
Satisfies TypeScript's strict strictPropertyInitialization rule by telling the compiler that the property will be initialized at runtime by TypeORM rather than inside a constructor.

9. Explicit Column Types (e.g., type: 'varchar')
Ensures cross-database compatibility and enforces database-level integrity (such as exact column types and maximum character limits).

10. TypeORM Relationships vs. Raw SQL Foreign Keys
Difference: TypeORM abstracts foreign keys and SQL JOIN clauses into object-oriented decorators (@ManyToOne, @OneToMany) and TypeScript properties.

Advantages: Simplifies nested entity loading (e.g., via relations: ['comments']), provides compile-time type safety, and eliminates manual SQL JOIN queries.