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



# Commit Message Standardization

#### 1. **General Guidelines**
- **Be Clear and Concise**: Write messages that are easy to understand at a glance.
- **Use the Imperative Mood**: Start the commit message with a verb in the imperative form (e.g., "Add," "Fix," "Update").
- **Limit Line Length**: Keep the first line of the commit message under 50 characters. If you need to add a description, limit it to 72 characters per line.

#### 2. **Commit Message Structure**
A typical commit message should follow this structure:
```
<type>(<scope>): <subject>

<body>
```

- **Type**: Indicate the type of change (see types below).
- **Scope**: (Optional) Specify the area of the codebase affected (e.g., `user`, `auth`, `api`).
- **Subject**: A brief description of the change (50 characters or less).
- **Body**: (Optional) Detailed explanation of the changes (72 characters per line).

#### 3. **Commit Message Types**
Use the following types to categorize your commits:

- **feat**: A new feature for the user.
  - Example: `feat(user): add registration functionality`
  
- **fix**: A bug fix.
  - Example: `fix(auth): correct login error handling`
  
- **docs**: Documentation changes.
  - Example: `docs(readme): update installation instructions`
  
- **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semicolons, etc.).
  - Example: `style(css): format styles for better readability`
  
- **refactor**: A code change that neither fixes a bug nor adds a feature.
  - Example: `refactor(user): simplify user model logic`
  
- **perf**: A code change that improves performance.
  - Example: `perf(api): optimize data fetching for users`
  
- **test**: Adding missing tests or correcting existing tests.
  - Example: `test(user): add tests for user registration`
  
- **chore**: Changes to the build process or auxiliary tools and libraries.
  - Example: `chore(deps): update dependency versions`

#### 4. **Examples of Good Commit Messages**
- **Single-line Message**:
  ```
  feat(user): implement password reset functionality
  ```

- **Multi-line Message**:
  ```
  fix(api): correct error response for invalid requests

  Previously, the API returned a generic error message. Now it specifies the issue,
  improving clarity for users and developers.
  ```

#### 5. **Using Tools**
Consider using tools like:
- **Husky**: To enforce commit message guidelines before commits.
- **Commitlint**: To validate commit messages against the defined standard.


# GitHub Work Standardization

#### 1. **Repository Structure**
- **Naming Conventions**: Use descriptive names for repositories. For example, `project-name`, `client-app`, or `api-service`.
- **Branch Naming**: Use a clear and consistent naming convention for branches:
  - Use the format: `type/short-description`.
  - Examples:
    - `feat/add-login-functionality`
    - `fix/fix-bug-in-registration`
    - `chore/update-dependencies`

#### 2. **Branching Strategy**
- **Main Branch**: Use `main` or `master` as the main branch. This should always reflect the production-ready state of the application.
- **Feature Branches**: Create feature branches from `main` for new features or changes.
- **Bugfix Branches**: Create bugfix branches from `main` for bug fixes.
- **Release Branches**: For preparing a new release, create a branch like `release/v1.0.0`.

#### 3. **Pull Requests (PRs)**
- **Creating PRs**: 
  - Open a pull request when you are ready to merge your changes into the main branch.
  - Ensure the title follows the same format as commit messages (e.g., `feat(user): add user profile page`).
  
- **Descriptive PR Descriptions**: 
  - Provide a clear description of what the PR does, why it’s needed, and any relevant context.
  - Include any issue numbers being addressed (e.g., `Fixes #123`).

- **Assign Reviewers**: 
  - Assign at least one team member to review the pull request before merging.
  
- **Labeling**: 
  - Use labels to categorize PRs (e.g., `bug`, `enhancement`, `urgent`).

#### 4. **Code Review Process**
- **Review Guidelines**: 
  - Reviewers should focus on code quality, adherence to standards, and functionality.
  - Provide constructive feedback and ask clarifying questions.

- **Commenting on PRs**: 
  - Use inline comments for specific lines of code.
  - Summarize any larger concerns or suggestions in the PR description.

- **Approval Process**: 
  - Require at least one approval before merging.
  - Once approved, the author can merge the PR.

#### 5. **Merging Changes**
- **Merge Strategy**: 
  - Prefer using "Squash and Merge" to keep the commit history clean, or use "Rebase and Merge" if necessary.
  
- **Deleting Branches**: 
  - Delete the feature or bugfix branch after merging to keep the repository tidy.

#### 6. **Issues and Project Management**
- **Using Issues**: 
  - Create issues for bugs, new features, and tasks. Use descriptive titles and provide detailed descriptions.
  
- **Labels**: 
  - Use labels to categorize issues (e.g., `bug`, `enhancement`, `question`).

- **Milestones**: 
  - Use milestones to track progress towards larger goals or releases.

#### 7. **Documentation**
- **Wiki or README**: 
  - Maintain a `README.md` file that explains the project, setup instructions, and contribution guidelines.
  
- **Contributing Guidelines**: 
  - Create a `CONTRIBUTING.md` file to outline how to contribute to the project, including coding standards, testing instructions, and the pull request process.

#### 8. **Security Practices**
- **Code Secrets**: 
  - Do not store sensitive information (e.g., API keys, passwords) in the repository.
  
- **Branch Protection Rules**: 
  - Set branch protection rules to prevent direct pushes to the `main` branch and require PR reviews.



