# Trait

Artisan command

```
php artisan make:trait Trait/HasFilter
```

Example code

```php
namespace App\Traits;

use Illuminate\Support\Facades\DB;

trait HasFilter
{
    public function scopeFilterLike($query, $column, $keyword)
    {
        if ( ! empty($keyword)) {
            $keyword = strtolower($keyword);
            return $query->where(DB::raw("LOWER($column)"), "like", "%".$keyword."%");
        }

        return $query;
    }

    public function scopeOrFilterLike($query, $column, $keyword)
    {
        if ( ! empty($keyword)) {
            $keyword = strtolower($keyword);
            return $query->orWhere(DB::raw("LOWER($column)"), "like", "%".$keyword."%");
        }

        return $query;
    }
}
```

On your model

```php

use App\Traits\HasFilter;

class Post extends Model
{
    use HasFilter;
}
```

How to use

```php
use App\Models\Post;

$post = Post::filterLike('title', 'laravel')->orFilterLike('body', 'laravel')->get();
```
