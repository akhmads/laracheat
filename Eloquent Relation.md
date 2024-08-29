## Eloquent Relation

```php
use Illuminate\Database\Eloquent\Relations\BelongsTo;
use Illuminate\Database\Eloquent\Relations\HasMany;

public function user(): BelongsTo
{
	return $this->belongsTo(User::class,'user_id','id')->withDefault();
}

public function comments(): HasMany
{
	return $this->hasMany(Comment::class,'post_id','id');
}
```
