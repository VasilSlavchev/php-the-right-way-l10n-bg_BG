---
layout: page
title: Шаблони за дизайн
---

# Образци за дизайн

Има множество начини да структурираш един код на проект за уеб приложение и можеш да вложиш колкото си искаш
мисъл в архитектурата на приложението. Но обикновено е хубаво да следваш утвърдени образци, които ще ти направят
кода по-удобен за управление и по-лесен за разбиране от другите.

* [Architectural pattern в Wikipedia (английски)](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Software design pattern в Wikipedia (английски)](https://en.wikipedia.org/wiki/Software_design_pattern)

## Образец "Фабрика" (Factory)

Един от най-често срещаните шаблони е образецът "фабрика". В този шаблон, един клас създава
обекта, който искате да ползвате. Следва пример за ползване на шаблона:

{% highlight php %}
<?php
class Automobile
{
    private $vehicle_make;
    private $vehicle_model;

    public function __construct($make, $model)
    {
        $this->vehicle_make = $make;
        $this->vehicle_model = $model;
    }

    public function get_make_and_model()
    {
        return $this->vehicle_make . ' ' . $this->vehicle_model;
    }
}

class AutomobileFactory
{
    public static function create($make, $model)
    {
        return new Automobile($make, $model);
    }
}

// Използваме фабриакта за да създадем обект Automobile
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->get_make_and_model()); // извежда "Bugatti Veyron"
{% endhighlight %}

Този код използва фабрика за да създаде обект от тип Automobile. Има поне две възможни ползи от изграждането на
кода ви по този начин. Първата е, ако трябва да смените, преименвате или замените класа Automobile, единственото място
където трябва промените е във фабриката, а не на всяко място в кода където се ползва класа Automobile. Втората възможна
полза е в това че създаването на обект може да е сложна задача и може да се пренесе работата в фабриката, вместо да
се повтаря кода за установяване при всяко създаване на обект.

Използването на шаблона "Фабрика" не винаги е нужно или умно. Примерния код показан по-горе е твърде прост и
фабриката в случая добавя ненужна сложност. Но когато правиш сравнително голям и сложен проект, може да си спестиш
доста мъки, ако ползваш фабрики.

* [Шаблон Фабрика в Wikipedia (английски)](https://en.wikipedia.org/wiki/Factory_pattern)

## Преден контролер (Front Controller)

Предният контролер представлява единствена точка за достъп до вашето уеб приложение (пр. index.php), което обработва
всички заявки. Този код е отговорен за зареждането на всички зависимости, обработката на заявката и изпращането на
на отговора обратно до браузъра. Предният контролер може да е полезен, защото насърчава разделянето на кода на модули
и предоставя централно място за закачане на код, който трябва да се изпълнява с всяка заявка (като например изчистване
на входните данни)

* [Front Controller pattern в Wikipedia (английски)](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Образец Модел-Изглед-Контролер (Model-View-Controller)

Шаблонът Модел-изглед-контролер (MVC) и неговите производни HMVC и MVVM, ти поззволяват да разбиеш кода на логически
обекти, които вършат точно определена работа. Моделите служа, каот слой за достъп, извличане и форматиране на данни
в цялото ви приложението. Контролерите обработват заявките, обработват данните получени от моделите и зареждат изгледите
за изпращане като отговор. Изгледите форматират изгодните данни по подходящ начин за визуализация и обикновено
биват форматирани като документни бланки (markup, xml и др. формати).

MVC е най-често срещаният архитектурен образец/шаблон използван в известните [PHP рамки](https://github.com/codeguy/php-the-right-way/wiki/Frameworks).

Научете повече за MVC и неговите подобни:

* [MVC (английски)](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC (английски)](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM (английски)](https://en.wikipedia.org/wiki/Model_View_ViewModel)
