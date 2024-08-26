## Transaction

```php
use Illuminate\Support\Facades\DB;
use Illuminate\Support\Facades\Log;

DB::beginTransaction();
try {

    // your sql here
    DB::commit();
}
catch (Exception $e)
{
    DB::rollBack();
    Log::error($e->getMessage());
}
```
