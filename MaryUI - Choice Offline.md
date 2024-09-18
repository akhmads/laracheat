# MaryUI Choice Offline

On your volt component

```php
use Illuminate\Support\Collection;
use App\Models\Category;

new class extends Component {

    public $category_id;
    public Collection $categorySearchable;

    public function mount(): void
    {
        $this->searchCategory();
    }

    public function searchCategory(): void
    {
        $this->categorySearchable = Category::orderBy('name')->get();
    }
}
```

On your view

```html
<x-choices-offline label="Category" wire:model="category_id" :options="$categorySearchable" option-value="id" option-label="name" single searchable />
```
