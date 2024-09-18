## Eloquent Relation

On your model

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsTo;
use Illuminate\Database\Eloquent\Relations\HasMany;

class Post extends Model
{
	public function author(): BelongsTo
	{
		return $this->belongsTo(User::class,'user_id','id')->withDefault();
	}

	public function comments(): HasMany
	{
		return $this->hasMany(Comment::class,'post_id','id');
	}
}
```

How to use one to many inverse

```php
use App\Models\Post;

$post = Post::find(1);

return $post->author->name;
```

How to use one to many

```php
use App\Models\Post;

$comments = Post::find(1)->comments;

foreach ($comments as $comment) {
    // ...
}
```
