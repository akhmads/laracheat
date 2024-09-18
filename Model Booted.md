# Model Booted

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Contact extends Model
{
    protected static function booted(): void
    {
        static::creating(function (Model $model) {
            $model->full_name = $model->first_name . ' ' . $model->last_name;
            $model->created_by = auth()->user()->id;
            $model->updated_by = auth()->user()->id;
        });

        static::updating(function (Model $model) {
            $model->full_name = $model->first_name . ' ' . $model->last_name;
            $model->updated_by = auth()->user()->id;
        });
    }
```
