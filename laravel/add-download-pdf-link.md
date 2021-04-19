# Add PDF download link at ....blade.php

To generate a link to a physical file or directory, but don't want to run through Laravel's application (e.g. through index.php), use URL::asset().

```jsx
URL::asset('assets/pdf/file.pdf');
```

This assumes a physical PDF file has been created on server which you want to link to.

If the PDF file is dynamic and generated/retrieved through the Laravel application, then use

```jsx
URL::to();
// or
URL::route();
// or similar
```

For Example in one of my project, I had to add a download link at index.blade.php, what I did is added this PDF file into public folder (public/download/Handbook.pdf),
and added this line:

```jsx
<a href="{{ URL::to('download/Handbook.pdf')}}" target="_blank">
	Handbook
	<i class="fas fa-book"></i>
</a>
// using fontawesome icon
```
