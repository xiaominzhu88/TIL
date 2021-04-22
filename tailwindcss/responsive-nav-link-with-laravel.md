# Responsive nav-link with Laravel Jetstream

In one of my projects I had to define responsive nav link for mobile version which present with `tailwindCss` with jetstream.

🍒 This is one `x-jet-responsive-nav-link` in the file =>

**views/ navigation-menu.blade.php**

```jsx
<nav x-data="{ open: false }" class="bg-white border-b border-gray-100">

@can('manage-events', auth()->user()->currentTeam)
     <x-jet-responsive-nav-link href="{{ route('events') }}" :active="request()->routeIs('events')" >
        {{ __('menu.events') }}
     </x-jet-responsive-nav-link>
@endcan
</nav>

```

🍒 I defined a file =>

**views/vendor/jetstream/components/responsive-nav-link.blade.php**

which `controls` the tailwindcss class from the file above

```jsx
@props(['active'])

@php
$classes = ($active ?? false)
            ? 'inline-block w-auto px-1 pt-2 ml-4 pb-2  border-l-0 border-b-2 border-indigo-400 focus:border-indigo-700 text-base font-medium leading-5 text-gray-900 focus:outline-none transition duration-150 ease-in-out'
            : 'inline-block w-auto px-1 pt-2 ml-4 pb-2  border-transparent text-base font-medium leading-5 text-gray-500 hover:text-gray-700 border-b-2 hover:border-gray-300 focus:outline-none focus:text-gray-700 focus:border-gray-300 transition duration-150 ease-in-out';
@endphp

<a {{ $attributes->merge(['class' => $classes]) }}>
    {{ $slot }}
</a>
```

This is practical, I can add many `nav links` if I want, and they are all defined one time in one file 🤞
