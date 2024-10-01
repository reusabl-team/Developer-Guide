# Developer Code Standardization

#### 1. **Project Structure**
- **Follow Default Structure**: Use the default Laravel folder structure without unnecessary modifications.
  - `app/`: Contains application logic.
  - `config/`: Contains configuration files.
  - `database/`: Contains migrations, seeders, and factories.
  - `resources/`: Contains views and assets.
  - `routes/`: Contains route definitions.
- **`app/Services` Folder**:
  - Create a `Services` folder for complex or reusable business logic.
  - Example: `app/Services/UserService.php`

#### 2. **Naming Conventions**
- **Variables and Functions**: Use `camelCase`.
  - Example:
    ```php
    public function getUserData() {}
    ```
- **Classes and Models**: Use `PascalCase`.
  - Example:
    ```php
    class User {}
    ```
- **Database Tables and Columns**: Use `snake_case`.
  - Example: `user_profiles`, `created_at`
- **Files and Classes**: File names should match the class name.
  - Example: `app/Models/User.php` for the `User` class.

#### 3. **Using Controllers**
- **Resource Controllers**: Use resource controllers for implementing CRUD operations.
  - Example:
    ```php
    Route::resource('users', UserController::class);
    ```
- **Middleware**: Apply middleware for authentication, authorization, and input validation.
  - Example:
    ```php
    Route::middleware(['auth'])->group(function () {
        Route::resource('posts', PostController::class);
    });
    ```

#### 4. **Validation**
- **FormRequest**: Use `FormRequest` for data validation.
  - Create a request:
    ```bash
    php artisan make:request StoreUserRequest
    ```
  - Example validation in `StoreUserRequest`:
    ```php
    public function rules()
    {
        return [
            'name' => 'required|string|max:255',
            'email' => 'required|string|email|max:255|unique:users',
        ];
    }
    ```

#### 5. **Routing**
- **Group Routes**: Use route groups for middleware and prefixes.
  - Example:
    ```php
    Route::prefix('admin')->middleware('auth')->group(function () {
        Route::resource('users', AdminUserController::class);
    });
    ```
- **Separate API Routes**: Use `routes/api.php` for API routes and `routes/web.php` for web routes.

#### 6. **Using Eloquent**
- **Mass Assignment**: Use `fillable` or `guarded` on models to protect against mass assignment vulnerabilities.
  - Example:
    ```php
    protected $fillable = ['name', 'email'];
    ```
- **Query Scope**: Create query scopes for commonly used queries.
  - Example:
    ```php
    public function scopeActive($query)
    {
        return $query->where('active', 1);
    }
    ```

#### 7. **Testing**
- **Use PHPUnit**: Write unit and integration tests for all major features.
  - Run tests:
    ```bash
    php artisan test
    ```
- **Database Testing**: Use SQLite for testing, and run migrations in the setup.
  - Example:
    ```php
    public function setUp(): void
    {
        parent::setUp();
        $this->artisan('migrate');
    }
    ```

#### 8. **Documentation**
- **Commenting**: Use PHPDoc for documenting functions and classes.
  - Example:
    ```php
    /**
     * Get user by ID.
     *
     * @param int $id
     * @return User
     */
    public function getUserById(int $id): User
    {
        return User::find($id);
    }
    ```
- **README.md**: Include explanations on how to run the project, dependencies, and usage instructions.

#### 9. **Version Control**
- **Git**: Use Git for version control following best practices.
  - Develop each feature in a separate branch.
- **Commit Messages**: Use clear and descriptive commit messages.
  - Example: `Add user registration feature`, `Fix bug in login process`.

#### 10. **Configuration and Environment**
- **`.env` File**: Do not upload `.env` to the repository. Use `.env.example` as a template.
- **Caching**: Use caching for configuration and routes:
  ```bash
  php artisan config:cache
  php artisan route:cache
  ```

#### 11. **Dependency Management**
- **Composer**: Use Composer to manage dependencies.
- **Autoloading**: Use PSR-4 autoloading for organizing classes.

#### 12. **Security Practices**
- **Input Sanitization**: Always sanitize user input.
- **Use HTTPS**: Ensure the application runs on HTTPS.
- **CSRF and XSS Protections**: Use CSRF protection and sanitize output to prevent XSS.

#### 13. **Linting and Code Formatting**
- **Use PHP CS Fixer**: To ensure code consistency.
- **Code Formatting**: Apply PSR-12 standards and use tools like PHPStorm or VSCode to assist.

