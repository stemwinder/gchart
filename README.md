# gchart

GChart is a very simple library that allows you to easily create arrays that are compatible with the Google Charts library. I use it together with Laravel and I am too much of a noob to explain you how to use it otherwise.

## Installation

Put this in composer.json

```
require: "grumpydictator/gchart": "dev-master"
```

Update the providers-array in app/config/app.php  with this:

```php
'Grumpydictator\Gchart\GchartServiceProvider',
```

## Examples

This returns the data used to create the example chart at [Google's line chart example](https://developers.google.com/chart/interactive/docs/gallery/linechart):
```php
$chart = App::make('gchart');
$chart->addColumn('Year', 'string');
$chart->addColumn('Sales', 'number');
$chart->addColumn('Expenses', 'number');

// add data:
$chart->addRow('2004', 1000, 400);
$chart->addRow('2005', 1170, 460);
$chart->addRow('2006', 660, 1120);
$chart->addRow('2007', 1030, 540);

$chart->generate();

echo json_encode($chart->getData());
```

This is roughly the same chart, but it uses date objects for the date:

```php

$chart = App::make('gchart');
$chart->addColumn('Day', 'date');
$chart->addColumn('Pizza slices I ate', 'number');
$chart->addColumn('Beers I drank', 'number');

// add data:
$chart->addRow(new Carbon('2014-05-01'), 3, 1);
$chart->addRow(new Carbon('2014-05-02'), 4, 2);
$chart->addRow(new Carbon('2014-05-03'), 3, 2);
$chart->addRow(new Carbon('2014-05-04'), 6, 3);
$chart->addRow(new Carbon('2014-05-05'), 5, 0);
$chart->addRow(new Carbon('2014-05-06'), 4, 1);

$chart->generate();

echo json_encode($chart->getData());

```