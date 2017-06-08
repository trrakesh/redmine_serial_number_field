# Redmine Serial Number Field

[![Build Status](https://travis-ci.org/matsukei/redmine_serial_number_field.svg?branch=master)](https://travis-ci.org/matsukei/redmine_serial_number_field)

[日本語 »](https://github.com/matsukei/redmine_serial_number_field/blob/master/README.md)

It is a plugin that provides custom fields that automatically add sequential numbers to Redmine.

## Features

* "Automatic serial number" is available as a format for custom fields for issues.
  * After creating a new custom field, you can not edit the "Regular expression".
  * Every user who can create a issue has automatic number assignment authority.
* Automatically assign sequential numbers of specified formats on a project basis at issue registration or update.
  * It works not only for single issues but also for bulk operation.
  * Custom field items are displayed when viewing issues. However, it will not be displayed when registering or updating.
* Basic options for custom fields are also available, such as issue filter criteria and search target.

### Notes

#### When you change tracker or project of numbered issue

* If the changed tracker does not have the same custom field, the sequential number assigned will be deleted.
* If the tracker after change has the same custom field, the sequential numbers numbered will not change (there is a risk of duplication).

#### When you set permissions for custom fields in workflow

* Setting a custom field for automatic number assignment to read only will not work properly.

## Usage

1. Create a new custom field for the issue.
2. Change the item "Format" to "Automatic serial number".
3. Specify the serial number format in the item "Regular expression".
4. If you wish to use it as a filter or search condition, please check as appropriate.
5. Specify the tracker and project you want to number automatically.
6. Done!
  * If you create a new ticket it will be automatically numbered.
  * Issues already created will be numbered as they are updated.

![usage.png](https://github.com/matsukei/redmine_serial_number_field/blob/master/doc/images/usage.en.png)

## Supported versions

* Redmine 3.2.x or higher

## Format specifications

|Column used in year format |Year format|fiscal year|Serial number format| result                 |
|---------------------------|-----------|-----------|--------------------|------------------------|
|created_on                 |`yy`       |No         |000                 |2015-03-01 => '15001'   |
|created_on                 |`yyyy`     |No         |0000                |2015-03-01 => '20150001'|
|created_on                 |`YY`       |Yes        |000                 |2015-03-01 => '14001'   |
|created_on                 |`YYYY`     |Yes        |0000                |2015-03-01 => '20140001'|

* OK
  * `{000000}` #=> `000001`
  * `ABC-{yy}-{00}` #=> `ABC-15-01`
* NG
  * When the end is not the serial number format
    * e.g. `ABC-{000}-{yy}`
  * When format not including year format or serial number format is included.
    * e.g. `{abc}-{yy}-{000}`

## Install

1. git clone or copy an unarchived plugin to `plugins/redmine_serial_number_field` on your Redmine path.
2. `$ cd your_redmine_path/`
3. `$ bundle install`
4. Redmineを再起動してください

## License

[The MIT License](https://opensource.org/licenses/MIT)