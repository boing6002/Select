# Select
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/c6799b0705d34fdab5cd100e7cfe6312)](https://www.codacy.com/app/laravel-enso/Select?utm_source=github.com&utm_medium=referral&utm_content=laravel-enso/Select&utm_campaign=badger)
[![StyleCI](https://styleci.io/repos/85489940/shield?branch=master)](https://styleci.io/repos/85489940)
[![Total Downloads](https://poser.pugx.org/laravel-enso/select/downloads)](https://packagist.org/packages/laravel-enso/select)
[![Latest Stable Version](https://poser.pugx.org/laravel-enso/select/version)](https://packagist.org/packages/laravel-enso/select)

[Bootstrap Select](https://silviomoreto.github.io/bootstrap-select/) data builder with server-side data fetching capability and a VueJS component

### Installation Steps

1. Add `LaravelEnso\Select\SelectServiceProvider::class` to `config/app.php`

2. Publish the VueJS components with `php artisan vendor:publish --tag=select-component`

3. Include the VueJS component in your `app.js`

4. Run `gulp` / `npm run dev`

5. Use the `SelectListBuilder` trait in your desired Controller

6. Define in routes/web.php a `getOptionsList` route for the desired Controller

6. Declare in your controller the `$selectSourceClass` variable as shown below:
	`protected $selectSourceClass = Model::class`
	where `Model::class` will be the Model from which the builder will extract the OptionsList.
	By default it will use the `name` field for the select list option label and the `id` for the key.
	If you need another field from the model you can customize it by adding the `protected $selectAttribute = 'customAtrribute'` variable.

6. In your blade add:

    ```
    <vue-select source="/routeToController"
        :name="inputName"
        :selected="selectedOption"
        :params="params"
        :pivot-params="pivotParams"
        multiple
        :custom-params="customParams">
    </vue-select>
    ```

7. Enjoy.

### Options

In order to work the component needs a data source. The data source can be either an ajax for server-side, OR a formatted array. In conclusion the component requires one of the two options `route` or `options` presented below:

	`source` - Only for server-side. The route suffix for your controller, getOptionsList will be added under the hood.
	`options` - Only where you don't need server-side. Options is an Object built with the 'buildSelectList' method from the 'SelectListBuilder' Trait.
	`name` - the name of the input (optional)
	`multiple` - multiple selectable options (optional). If ommited, the select acts as single select
	`selected` - the selected option. Can be a single value or an Array is the select is used as a multi-select (optional)
	`placeholder` - custom placeholder when no option in selected (optional)
	`params` - list of parameters from the same table. format: params: { 'fieldName': 'fieldValue' } (optional)
	`pivotParams` - list of parameters (ids) from pivot tables. format: pivotParams: { 'table': { id: value } } (optional)
	`customParams` - anything. Using customParams implies that you rewrite the 'getOptionsList' method from the SelectListBuilder Trait. You must use the static::buildSelectList method in order to format the query result in the expected format. (optional)

### Can publish
 - `php artisan vendor:publish --tag=select-component` - publishes the VueJS component
 - `php artisan vendor:publish --tag=update` - a common alias for when wanting to update the VueJS component, 
 once a newer version is released

### Contributions

are welcome
