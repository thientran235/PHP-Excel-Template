# PHPReport

PHP-Excel-Template is a class for building and exporting from a predefined template Excel. It's based on powerful [PHPSpreadsheet](https://github.com/PHPOffice/PhpSpreadsheet) library and includes exporting to popular formats such are HTML, Excel or PDF.

## Features

* Simple for using
* Many ways to customize your input data
* Build reports based on predefined templates
* Export to HTML, Excel (xlsx and xls) and PDF


## Installation

Install [composer](https://getcomposer.org), and run `composer update` to install
the required `PHPSpreadsheet` dependencies

## Usage and examples

Basicly, there are two way to build a report.

### Building it "from scratch"

PHP-Excel-Template does all the work, your just provide it with your data, like this:
<pre>
$Template = new PHP_Excel_Template();
$Template->load(array(
            'id'   => 'product',
            'data' => array(
                        array( 'Some product', 23.99 ),
                        array( 'Other product', 5.25 ),
                        array( 'Third product', 0.20 )
                )
            )
        );

$Template->render();
</pre>

It's great for exporting tabular data. Input data can be further formatted, grouped and customized. See the wiki.

### Building it from template

Template is usually some excel file, already formatted and with placeholders for data. There are two types of placeholders: static and dynamic.
Static placeholders are, for example, some data like date, city or customer name. Dynamic placeholders are, for example, list of products with variable number of rows.

<pre>
include '../PHP-Excel-Template.php';
//which template to use
$template = 'template-1.xlsx';
//set absolute path to directory with template files
$templateDir = 'resources/';
//set config for report
$config = array(
	'template'    => $template,
	'templateDir' => $templateDir
);

//we get some products, e.g. from database
$products = array(
    array(
		'description'  => 'CPU Intel Core i3-10100 (6M Cache, 3.60 GHz up to 4.30 GHz, 4C8T, Socket 1200, Comet Lake-S)',
		'qty'          => 1,
		'price'        => '$139',
		'total'        => '$139',
	),
    array(
		'description'  => 'Mainboard GIGABYTE B460M D2V',
		'qty'          => 1,
		'price'        => '$86',
		'total'        => '$86',
	),
    array(
		'description'  => 'Ram Kingston HyperX Fury 16GB (1x16GB) DDR4 Bus 2666Mhz',
		'qty'          => 2,
		'price'        => '$56',
		'total'        => '$112',
	),
    array(
		'description'  => 'HDD Western Digital Caviar Blue 2TB 64MB Cache',
		'qty'          => 1,
		'price'        => '$56',
		'total'        => '$56',
	),
    array(
		'description'  => 'SSD Kingston SKC600 256GB SATA 3.0 (SKC600/256G)',
		'qty'          => 1,
		'price'        => '$49',
		'total'        => '$49',
	),
    array(
		'description'  => 'VGA GIGABYTE GeForce RTX 3070 VISION OC 8G (GV-N3070VISION OC-8GD)',
		'qty'          => 1,
		'price'        => '$1049',
		'total'        => '$1049',
	),
    array(
		'description'  => 'PSU Xigmatek Z-POWER 600 - 500W EN45945',
		'qty'          => 1,
		'price'        => '$41',
		'total'        => '$41',
	),
    array(
		'description'  => 'Case GAMEMAX Panda T802 - ARGB black',
		'qty'          => 1,
		'price'        => '$69',
		'total'        => '$69',
	),
    array(
		'description'  => 'Monitor LG 29WN600-W 29 inch Ultrawide',
		'qty'          => 1,
		'price'        => '$236',
		'total'        => '$236',
	)
);


$Template = new PHP_Excel_Template($config);
$Template->load(array(
			array(
				'id'   => 'i18n',
				'data' => array(
					'pcbuilder'    => 'PC Builder',
					'company'      => 'Company',
					'address'      => 'Address',
					'website'      => 'Website',
					'phone'        => 'Phone',
					'item'         => 'Item',
					'description'  => 'Product name',
					'qty'          => 'Quantity',
					'unitprice'    => 'Unit Price',
					'total'        => 'Total',
					'comment'      => 'Note',
				)
			),
			array(
				'id'   => 'inv',
				'data' => array(
					'date'         => date('Y-m-d'),
					'title'        => 'Ex Title',
					'slogan'       => 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
					'company'      => 'Ex Company',
					'address'      => '27 Colmore Row, Birmingham, England',
					'website'      => 'www.yourwebsite.com',
					'phone'        => '+123456789',
					'comment'      => 'Vestibulum sagittis orci ac odio dictum tincidunt. Donec ut metus leo. Class aptent taciti sociosqu ad litora torquent per conubia nostra.',
				),
				'format' => array(
					'date' => array( 'datetime' => 'd/m/Y' )
				)
			),
			array(
				'id'      =>'prod',
				'repeat'  => true,
				'data'    => $products,
				'minRows' => 9999
			),
			array(
				'id'=>'total',
				'data'=> array(
					'price' => '$2102'
				),
			)
		)
    );

$filename = 'pc-builder-' . rand();
echo $Template->render('excel', $filename);
exit();

</pre>

These reports are great for complex exports like invoices. See the wiki for more examples.
