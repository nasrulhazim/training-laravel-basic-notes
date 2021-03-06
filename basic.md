# Web Development with Laravel

Basic: bit.ly/training-laravel-basic-v4
Telegram: t.me/laravel_malaysia
Laracasts: www.laracasts.com

## Tools & Environment

- [ ] Code Editor | IDE
	- [ ] Sublime Text 3
	- [ ] PHPStorm
	- [ ] Atom
	- [ ] Visual Studio Code
- [ ] SQL Editor
	- [ ] Sequel Pro (Mac only)
	- [ ] SQLYog Community
	- [ ] HeidiSQL
- [ ] Development Environment
	- [ ] Windows: Laragon
	- [ ] MacOS: Valet
	- [ ] Linux: LAMP Stack

# 101

- [ ] Create project
	- [x] `laravel new project-name`
		- [ ] php artisan serve - run laravel project using php web server.
	- [ ] Create database
	- [ ] Setup `.env` 
		- [ ] APP_URL 
		- [ ] database
		- [ ] email
			- [ ] Development
				- [ ] mailtrap.io
				- [ ] log
			- [ ] Production: gmail, yahoo, etc.
	- [ ] Run migration - `php artisan migrate`
	- [ ] Run auth scaffolding - `php artisan make:auth`
	- [ ] Test app with `php artisan serve`
		- [ ] Landing 
		- [ ] Login
		- [ ] Logout
		- [ ] Register
		- [ ] Reset Password

# 102

- [ ] Create a page
	- [ ] Route
		- [ ] Web
			- [ ] get
			- [ ] post
			- [ ] put
			- [ ] delete
			- [ ] resource
	- [ ] Controller
		- [ ] `php artisan make:controller ...`
			- [ ] -r or --resource - index, create, store, show, edit, update, destroy
			- [ ] --api - index, store, show, update, destroy
	- [ ] View
		- [ ] `view()` helper
			- [ ] File extension `.blade.php`
			- [ ] dot as directory separator - `view('pages.index')` means to load view from `resources/views/pages/index.blade.php` 
		- [ ] Blade Directives
			- [ ] @extends
			- [ ] @guest ... @else ... @endguest
			- [ ] @auth ... @else ... @endauth
			- [ ] @if ... @endif
			- [ ] @foreach ... @endforeach
			- [ ] @forelse ... @empty ... @endforelse
			- [ ] @section ... @endsection 
			- [ ] @isset($variable_name) ... @endisset
			- [ ] @component('path.to.component')
			- [ ] @include('path.to.component')
			- [ ] @includeWhen(auth()->user(), 'path.to.component')

## Tinker

- [ ] Database
	- [ ] Factory - create users using tinker 

```
$ php artisan tinker
>>> factory(\App\User::class, 100)->create();
```

## Model

- [ ] Model - get all users

```
$users = \App\User::all();
return view('users.index', compact('users'));
```

### Pagination

```
$users = \App\User::paginate($length = 25);
return view('users.index', compact('users'));
```

```
$users->links();
```

- [ ] Blade - generate table for user listing

```
@foreach($users as $user)
	<tr>
		<td>{{ $user->name }}</td>
		<td>{{ $user->email }}</td>
	</tr>
@endforeach
```

```
@forelse($users as $user)
	<tr>
		<td>{{ $user->name }}</td>
		<td>{{ $user->email }}</td>
	</tr>
@empty
	<tr>
		<td colspan="2">No users found</td>
	</tr>
@endforelse
```

## Forms

```
@csrf
@method('PUT')
@method('DELETE')
```

```php
Route::resource('uri', Controller);
```

```
php artisan route:list
```

## Validation

```php
$this->validate($request, [
	'email' => 'required'
]);
```

```
@isset($errors)
	$errors->first('name');
@endisset
```

## Database

### Factory

```
factory(\App\User::class)->create();
factory(\App\User::class)->make();
factory(\App\User::class, 100)->create();
factory(\App\User::class, 100)->make();
```

### Migration

```
php artisan make:migration migrate_name --create=table_names
php artisan make:migration alter_table --table=table_names
```

### Seed

Development: Seeder + Factory
Reference Data: Negeri, Postcode


## Data

- [x] Model / Eloquent
- [x] Migration

```
php artisan make:model Models/Department -m
php artisan migrate
```

- [ ] Factory
- [ ] Seeder

```
php artisan make:seeder DepartmentSeeder
php artisan db:seed
php artisan db:seed --class=DepartmentSeeder
php artisan migrate:fresh --seed
```

## Naming Conventions

### Database

Table name in plural except for pivot

```
users
departments
```

#### Foreign Key(FK)

FK name used is `table_name_in_singular_id`. For instance:

```
department_id
user_id
```

### Models

Reorganise models to be under `app/Models`.

Creating modals will be like:

```
php artisan make:model Models/Department
php artisan make:model Models/Employee
```

### Classes / File names

In studly case format - StudlyCase

### Views

Directory name in kebab case - `kebab-case`.

```
user
hr-payroll
hr-leave
hr-claim
```
