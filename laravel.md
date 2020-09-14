# Laravel

php artisan make:model -m Models/TrainingType - Создастся модель и миграция

php artisan migrate - запускаются миграции

php artisan make:seeder TrainingTypesTableSeeder - для заполнения данных в таблицу БД. Появится файл database/seeds/TrainingTypesTableSeeder.php

Далее в database/seeds/DatabaseSeeder.php нужно добавить:

$this-&gt;call\(TrainingTypesTableSeeder::class\);

А остальные просто закоментируй чтобы повторно не вызвались

И после php artisan db:seed

