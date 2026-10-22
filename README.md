1. Most Challenging Part
Async Error Handling: Managing async/await flows and returning structured JSON error responses without crashing the app.

Input Validation: Safely parsing URL route parameters and validating unique constraints like email uniqueness during updates.
2. TypeORM vs. Raw SQL
TypeScript Entities: Maps database tables directly to classes, avoiding manual SQL string queries.

Type Safety & Auto-complete: Reduces runtime errors with strong typing for queries and relations.
3. Hiding Passwords & ImplementationWhy: Protects sensitive user credentials from leaking in API responses or logs.Implementation:Added { select: false } to the password entity column.   Used destructuring in the controller to omit password from the JSON response object (const { password: _, ...userWithoutPassword } = savedUser).   
4. When to Use Transactions
Scenario: E-commerce checkout (creating an order, deducting inventory, charging balance).

Why: Ensures all operations succeed together or fail/rollback entirely, preventing corrupted data.
5. synchronize: true vs. Migrationssynchronize: true: Automatically updates database schema on app start. Use only in development.   Migrations: Version-controlled SQL scripts for manual schema changes. Use in production to prevent accidental data loss.
6. Adding a Product Entity (One-to-Many)Product Entity: Add @ManyToOne(() => User, (user) => user.products).User Entity: Add @OneToMany(() => Product, (product) => product.user) products!: Product[];.Config: Register Product inside the entities array in data-source.ts.   
7. Security Improvements for Production
Password Hashing: Hash passwords using bcrypt or argon2.

Authentication: Protect endpoints using JWT or session tokens.

Rate Limiting & Validation: Use express-rate-limit to prevent brute-force attacks and validate input with class-validator.

Environment: Set NODE_ENV=production, turn off synchronize, and restrict CORS origins.