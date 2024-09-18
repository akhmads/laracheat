# Mary UI Choice

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

    public function searchCategory(string $value = ''): void
    {
        $selectedOption = Category::where('id', $this->category_id)->get();
        $this->categorySearchable = Category::
            ->filterLike('name', $value)
            ->selectable()
            ->take(20)
            ->get()
            ->merge($selectedOption);
    }
}
```

On your view

```html
<x-choices label="Category" wire:model="category_id" :options="$categorySearchable" search-function="searchCategory" option-value="id" option-label="name" single searchable />
```
