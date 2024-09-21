# Unique Rule

Migration

```php
return new class extends Migration
{
    public function up(): void
    {
        Schema::create('posts', function (Blueprint $table) {

            $table->string('slug', 50)->unique();

        });
    }
}
```

Create Validation

```php
public function save(): void
{
    $data = $this->validate([
        'slug' => 'required|unique:posts,slug',
    ]);
}
```

Update Validation

```php
public function save(): void
{
    $data = $this->validate([
        'slug' => 'required|unique:posts,slug,'.$post->id,
    ]);
}
```

Ignore ID

```php
use Illuminate\Validation\Rule;

public function save(): void
{
    $data = $this->validate([
        'slug' => Rule::unique('posts','slug')->ignore($post->id),
    ]);
}
```

Additional Clause

```php
use Illuminate\Validation\Rule;
use Illuminate\Database\Query\Builder;

public function save(): void
{
    $data = $this->validate([
        'slug' => Rule::unique('posts','slug')->where(fn (Builder $query) => $query->where('user_id', 1))
    ]);
}
```

Or

```php
use Illuminate\Validation\Rule;
use Illuminate\Database\Query\Builder;

public function save(): void
{
    $data = $this->validate([
        'slug' => Rule::exists('posts','slug')->where(function (Builder $query) {
            return $query->where('user_id', 1);
        }),
    ]);
}
```
