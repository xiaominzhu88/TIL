# Laravel Livewire CRUD

- Install Laravel Livewire

```jsx
composer require livewire/livewire
```

Create Laravel Livewire component views

```bash
views
  livewire
    contact
      component.blade.php
      create.blade.php
      update.blade.php
```

- define a route into route file for returning a view

```jsx
Route::view('contact', 'admin.contact');
```
