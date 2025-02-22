# silverstripe-dependentdropdownfield

A SilverStripe dropdown and list box field that has it's options populated via ajax, based on the value of the field it depends on.

## Requirements

SilverStripe 4

## Usage example

```php
// 1. Create a callable function that returns an array of options for the DependentDropdownField.
// When the value of the field it depends on changes, this function is called passing the
// updated value as the first parameter ($val)
$dataSource = function($val) {
	if ($val == 'one') {
		// return appropriate options array if the value is one.
	}
	if ($val == 'two') {
		// return appropriate options array if the value is two.
	}
};

//For Dropdown Field
$fields = FieldList::create(
	// 2. Add your first field to your field list,
	$fieldOne = DropdownField::create('FieldOne', 'Field One', ['one' => 'One', 'two' => 'Two']),
	// 3. Add your DependentDropdownField, setting the source as the callable function
	// you created and setting the field it depends on to the appropriate field
	DependentDropdownField::create('FieldTwo', 'Field Two', $dataSource)->setDepends($fieldOne)
);

//For Listbox Field
$fields = FieldList::create(
	// 2. Add your first field to your field list,
	$fieldOne = DropdownField::create('FieldOne', 'Field One', ['one' => 'One', 'two' => 'Two']),
	// 3. Add your DependentDropdownField, setting the source as the callable function
	// you created and setting the field it depends on to the appropriate field
	DependentListboxField::create('FieldTwo', 'Field Two', $dataSource)->setDepends($fieldOne)
);

```
