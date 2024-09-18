# Model Scope

On your model

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Builder;

class Contact extends Model
{
    public function scopeSelectable($query)
    {
        return $query->where('status','active')->orderBy('name','asc');
    }

    public function scopePopular(Builder $query): void
    {
        $query->where('votes', '>', 100);
    }
}
```

How to use

```php
use App\Models\Contact;

$contact = Contact::selectable()->popular()->get();
```
