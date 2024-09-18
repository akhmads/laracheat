# Enum

Create enum

```
php artisan make:enum ActiveStatus
```

Example code on /app/Enums/ActiveStatus.php

```php
namespace App\Enums;

enum ActiveStatus: string
{
    case active = 'active';
    case inactive = 'inactive';

    public function color(): string
    {
        return match($this)
        {
            self::active => 'badge-success text-white',
            self::inactive => 'badge-error text-white',
        };
    }

    public static function toSelect($placeholder = false): array
    {
        $array = [];
        $index = 0;
        if ($placeholder) {
            $array[$index]['id'] = '';
            $array[$index]['name'] = '-- Select --';
            $index++;
        }
        foreach (self::cases() as $key => $case) {
            $array[$index]['id'] = $case->value;
            $array[$index]['name'] = $case->value;
            $index++;
        }
        return $array;
    }
}
```

On your migration

```php
$table->enum('status', ['active','inactive'])->index()->default('active');
```

On your model

```php
use App\Enums\ActiveStatus;

class Post extends Model
{
    protected function casts(): array
    {
        return [
            'status' => ActiveStatus::class,
        ];
    }
}
```

On your form with Mary UI

```html
<x-select label="Status" :options="\App\Enums\ActiveStatus::toSelect(true)" wire:model="status" />
```

On your view

```html
@scope('cell_status', $post)
<x-badge :value="$post->status->value" class="text-xs uppercase {{ $post->status->color() }}" />
@endscope
```
