## Authorization

Define gate in /app/Providers/AppServiceProvider.php

```php
use Illuminate\Support\Facades\Gate;

class AppServiceProvider extends ServiceProvider
{
    public function boot(): void
    {
        Gate::define('admin', function($user) {
            return $user->role == 'admin';
        });

        Gate::define('author', function($user) {
            return $user->role == 'author';
        });
	}
}
```

Authorizing Actions

```php
use Illuminate\Support\Facades\Gate;

class PostController extends Controller
{
    public function update(Request $request, Post $post): RedirectResponse
    {
        if (! Gate::allows('update-post', $post)) {
            abort(403);
        }

        // Update the post...

        return redirect('/posts');
    }
}
```

Authorize multiple actions at a time

```php
if (Gate::any(['update-post', 'delete-post'], $post)) {
    // The user can update or delete the post...
}

if (Gate::none(['update-post', 'delete-post'], $post)) {
    // The user can't update or delete the post...
}
```

Authorizing or Throwing Exceptions

```php
Gate::authorize('update-post', $post);
$this->authorize('update-post', $post);
```

Via Middleware

```php
Route::put('/post/{post}', function (Post $post) {
    // The current user may update the post...
})->middleware('auth','can:update-post');
```

Via Blade Templates

```php
@can('update-post')
    <!-- The current user can update the post... -->
@else
    <!-- ... -->
@endcan

@cannot('update-post')
    <!-- The current user cannot update the post... -->
@endcannot

@canany(['update-post', 'view-post', 'delete-post'])
    <!-- The current user can update, view, or delete the post... -->
@endcanany
```
