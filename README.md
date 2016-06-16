OpenShift Yii2 Advanced
=======================

Do you use the Yii2 Advanced template? Do you use OpenShift? Next time you create a new app on OpenShift, use this repo's git URL to instantly have Yii2 Advanced installed and setup out of the box with your new OpenShift app.

**Current Yii2 Version:** 2.0.8

**Link:** [Yii2 Advanced Application](https://github.com/yiisoft/yii2-app-advanced)

## Includes My OpenShift Yii2 Config

This comes with my [OpenShift-Yii2-Config](https://github.com/WadeShuler/OpenShift-Yii2-Config) repo. It allows you to push your project to OpenShift easily. Before your app starts back up, it: runs composer, runs Yii init (optional but on by default), creates symlink named `web` in the root of your project pointing to `/frontend/web`, creates a symlink named `admin` inside `/frontend/web` pointing to `/backend/web`, and optionally runs yii migrate for you on push to ensure your database is synced.

Don't want to run `yii migrate` or `yii init`, but would rather do it differently? You can easily turn those off inside the `/.openshift/action_hooks/deploy` file. Migrate is off by default to prevent accidental migrations. Init is necessary for the Yii2 appp to run, but you can turn it off if you have something else in mind.

## Additionally

On top of my OpenShift Yii2 action hooks, this comes with OpenShift's Environment Variables for the production database config. Inside the `/environments/prod/common/config/main-local.php`, you will find them. When yii init runs (automatically when pushed to your OpenShift app), it will already know how to connect to your OpenShift MySQL database.

If you turn off `yii init` in the OpenShift deploy action hook, the default database Environment Variables will not be used. The init copies files from the `environments` directory and puts them appropriately in their place. So use environments properly (how Yii meant for them to be used), or copy/move the file yourself into the appropriate place.

This of course comes with Yii2 Advanced. Please check the current Yii version in use (located at the top of this README)

## What this does not do

This does not create a default database for you. The development `main-local.php` file is stock, and the production `main-local.php` has the Environment Variables ready to go. There is no database and the `migrations` have been left alone from the stock Yii2 Advanced project. This is why migrate is off by default. You would need to create your own database for your development, and update the development `main-local.php` config file with your development database info (usually your localhost).

## How to set up a database?

### Option A:

Those who use Yii migrations: All you really need to do is create your database. You can then use yii migrations to create tables and set everything else up. Thus, when migrate is ran on your OpenShift server, it will build it from the start. You of course have to create a MySQL database on your OpenShift app. When your ready, don't forget to set the boolean for `YII_MIGRATE` to true, in the OpenShift deploy action hook.

### Option B:

Create your database locally. Create your OpenShift database. Manually import your database (Navicat or setup phpMyAdmin). From a baseline, then you could then use migrations. Or just manually update the database and skip using migrations all together. It's up to you.
